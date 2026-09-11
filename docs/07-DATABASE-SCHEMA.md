# Database Schema

> Source of truth: read-only inspection of `chnk8802/mrm`. This file records verified schema behavior only. It must be expanded as remaining models are inspected.

## Database technology

The backend uses MongoDB through Mongoose. Verified model files currently include:

- `Counter`
- `Customer`
- `Organization`
- `Payment`
- `Plan`
- `Repair`
- `SparePartUsage`
- `Supplier`
- `User`

The application is multi-tenant. Organization-scoped documents use an `orgScopePlugin`, and non-superadmin users are tied to an `Organization` through `orgId`.

## User

Verified source: `apps/server/models/user.model.js`.

Fields:

- `name: String`, required, trimmed, max 20
- `email: String`, required, trimmed, lowercased
- `password: String`, required, excluded from normal query selection
- `role: String`, required, enum from shared `ROLES`
- `phone: String`, required, trimmed, max 20
- `address.street`
- `address.city`
- `address.state`
- `address.postalCode`
- `address.country`
- `avatar: String`, default `https://i.pravatar.cc`
- `isActive: Boolean`, default `true`
- `isDeleted: Boolean`, default `false`, normally excluded from selection
- `orgId: ObjectId -> Organization`; required unless role is `superadmin`
- timestamps enabled

Indexes:

- unique partial index on `email` while `isDeleted: false`
- `role`
- `isActive`
- text index on `name`, `email`, `phone`
- `createdAt desc`
- `orgId`

Virtuals:

- `fullAddress` concatenates populated address parts.

Tenant behavior:

- Uses `orgScopePlugin` with `addField: false` and `countsTowardCap: true`.
- Superadmin users may exist without an organization.

## Organization

Verified source: `apps/server/models/organization.model.js`.

Fields:

- `name: String`, required, trimmed, max 100
- `contactEmail: String`, lowercased, max 100
- `contactPhone: String`, max 20
- `subscription.planId: ObjectId -> Plan`, required
- `subscription.capsOverride: Boolean`, default `false`
- `subscription.recordCount: Number`, default `0`, min `0`
- `subscription.expiresAt: Date`
- `isActive: Boolean`, default `true`
- `isDeleted: Boolean`, default `false`, normally excluded from selection
- timestamps enabled

Indexes:

- `name`
- compound index on `isActive`, `isDeleted`

Reconstruction implication: tenant lifecycle and subscription record caps are first-class platform concerns and must not be replaced with a flat single-tenant design.

## Repair

Verified source: `apps/server/models/repair.model.js`.

Fields:

- `repairId: String`
- `status: String`, enum `STATUS_OPTIONS`, default `received`
- `paymentStatus: String`, enum `PAYMENT_STATUS`, default `unpaid`
- `customer: ObjectId -> Customer`, required
- `technician: ObjectId -> User`
- `deviceModel: String`, required
- `imei: String`
- `problem: String`, required
- `accessories: String`
- `serviceCharge: Number`, rounded helper, required, min 0
- `discount: Number`, rounded helper, default 0, min 0
- `dueDate: Date`
- `completedAt: Date`
- `isPickedUp: Boolean`, default false
- `pickedUpAt: Date`
- `sparePartUsage: [ObjectId -> SparePartUsage]`
- `notes: String`
- `amountPaid: Number`, default 0
- `isDeleted: Boolean`, default false, normally excluded
- timestamps enabled

Lifecycle behavior:

- Before first save, if no `repairId` exists, the model obtains a sequence from `Counter` using a key scoped to the current organization: `repairId:<orgId>`.
- IDs are formatted `REP-0001`, `REP-0002`, etc.
- When status changes to `completed`, `completedAt` is automatically set.

Indexes:

- `customer`
- `technician`
- `status`
- compound `isDeleted + status`
- `createdAt desc`
- text index on `deviceModel`, `imei`, `problem`
- unique compound `orgId + repairId`

Tenant behavior:

- Uses `orgScopePlugin` with `countsTowardCap: true`.

## Cross-model implications

The verified schema already establishes these domain relationships:

```text
Plan <- Organization <- User
                  \-> Repair -> Customer
                            \-> User (technician)
                            \-> SparePartUsage[]
```

Payments, suppliers, customers, plans, spare-part usage, and counters still require full field-by-field extraction into this document.
