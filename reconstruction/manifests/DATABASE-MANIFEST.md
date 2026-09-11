# Database Manifest

This manifest maps verified Mongoose models from the source application to reconstruction responsibilities.

| Model | Source file | Key relationships / responsibility | Tenant scoped | Reconstruction status |
|---|---|---|---|---|
| Counter | `apps/server/models/counter.model.js` | Sequence generation, including per-org repair IDs | Context-dependent | Inventory only |
| Customer | `apps/server/models/customer.model.js` | Customer records referenced by repairs | Yes (expected from source structure; full schema pending) | Schema pending |
| Organization | `apps/server/models/organization.model.js` | Tenant identity, subscription plan, caps, active/deleted state | Platform-level | Core schema verified |
| Payment | `apps/server/models/payment.model.js` | Repair/customer payment records and outstanding balance workflows | Pending full verification | Schema pending |
| Plan | `apps/server/models/plan.model.js` | Subscription plan definition used by organizations | Platform-level | Schema pending |
| Repair | `apps/server/models/repair.model.js` | Main repair order, customer, technician, status, charges, pickup, payment tracking | Yes | Core schema verified |
| SparePartUsage | `apps/server/models/sparePartUsage.model.js` | Parts consumed by repairs | Pending full verification | Schema pending |
| Supplier | `apps/server/models/supplier.model.js` | Supplier management | Pending full verification | Schema pending |
| User | `apps/server/models/user.model.js` | Authentication identity, role, tenant membership, technician relationship | Yes except superadmin | Core schema verified |

## Verified reconstruction invariants

1. Do not implement the database as single-tenant. Organization scoping is structural.
2. A non-superadmin `User` requires an `orgId`; a superadmin does not.
3. `Organization.subscription.planId` is required.
4. Organization subscriptions track record counts/cap override/expiry state.
5. Repair IDs are generated per organization using `Counter` and formatted `REP-####`.
6. `Repair` has separate repair status, payment status, pickup state, amount paid, and completion/pickup timestamps.
7. Repair/customer/supplier source routes reveal soft-delete, restore, and permanent-delete semantics that must be reflected in data behavior.
8. Shared enums/validation values come from `packages/validators`; do not duplicate guessed constants independently in frontend and backend.

## Required next extraction

For every model, capture:

- complete field list and types
- required/default/enum/min/max/trim/select rules
- indexes and uniqueness constraints
- virtuals
- hooks
- plugins
- tenant-scoping behavior
- references/population targets
- soft-delete behavior
- derived totals and rounding rules
- which API operations mutate the model

The reconstruction implementation must not begin until these invariants are represented in executable schemas and their acceptance tests.
