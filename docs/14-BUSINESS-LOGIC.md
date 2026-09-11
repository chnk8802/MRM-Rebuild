# Business Logic

This document records reconstruction-critical rules verified from source. It will expand as controller/service analysis proceeds.

## Multi-tenant organization scoping
Most tenant-owned Mongoose models use a shared `orgScopePlugin`.

The plugin can automatically:
- add a required `orgId` field and index;
- inject `{ orgId: currentOrgId }` into reads, updates, counts, and deletes;
- prepend an organization `$match` stage to aggregation pipelines;
- stamp newly-created documents with the current request organization;
- reject scoped operations for ordinary users when organization context is missing.

Superadmins are exceptional: when request context contains no `orgId`, the plugin allows unscoped access instead of throwing. Combined with the authentication middleware's `x-org-id` support, this creates two modes for superadmins: cross-tenant/global and selected-tenant.

### Critical reconstruction invariant
Tenant isolation is enforced at the model layer, not only in controllers. A rebuild that merely adds `orgId` filters manually in selected endpoints is not equivalent and risks cross-tenant data exposure.

## Subscription record caps/accounting
Models can enable the plugin option `countsTowardCap`.

When enabled:
- creating a new document increments `Organization.subscription.recordCount`;
- deleting documents decrements the affected organizations' record counts;
- delete hooks snapshot affected tenant IDs before deletion so post-delete accounting still knows which organizations to update.

Verified examples using cap accounting include `User` and `Repair`.

This mechanism strongly implies subscription plans can constrain tenant record volume. The exact enforcement point/cap comparison must be derived from remaining service/controller code before reconstruction.

## Repair identifiers
A new Repair without `repairId` gets an organization-specific sequential identifier using the `Counter` model.

Counter key format:
`repairId:<orgId>` (or `repairId:global` when no org context exists)

Rendered repair ID format:
`REP-` + a sequence padded to four digits, e.g. `REP-0001`.

A unique compound index on `{ orgId, repairId }` protects uniqueness inside each tenant.

## Repair lifecycle side effects
When a Repair's `status` changes to `completed`, the model automatically sets `completedAt` to the current time.

Pickup state is modeled independently with `isPickedUp` and `pickedUpAt`.

Payment lifecycle is also independent via `paymentStatus`, `amountPaid`, service charge, discount, and related Payment records. Reconstruction must not collapse repair status, pickup status, and payment status into a single state machine.

## Deletion lifecycle
Customers, suppliers, users, and repairs include soft-delete concepts in the discovered source. Several route modules expose separate restore and permanent-delete operations. Permanent deletion is generally reserved for `superadmin`, while normal deletion is performed by lower administrative roles depending on resource.

A rebuild must distinguish:
1. active record;
2. soft-deleted record;
3. restored record;
4. permanently deleted record.

## Authorization semantics
RBAC uses a numeric hierarchy. `authorize('staff')` permits staff, manager, admin, and superadmin. `authorize('admin')` permits admin and superadmin.

Frontend restrictions are sometimes stricter/different for workflow reasons, so both API authorization and frontend route behavior must be documented separately.
