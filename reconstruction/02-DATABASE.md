# Phase 02 — Database

## Goal
Recreate MongoDB/Mongoose persistence, tenant scoping, subscription limits and source-verified schemas.

## Build order
1. Database connection/config.
2. Request context utility.
3. Organization and Plan models.
4. Counter model.
5. `orgScopePlugin` with query, aggregate and create-time scoping.
6. Record-cap counting behavior.
7. User, Customer, Supplier, Repair, SparePartUsage and Payment models.
8. Indexes, virtuals and soft-delete fields.
9. Plan seeding.

## Critical invariants
- Non-superadmin tenant data is scoped by `orgId`.
- Superadmin with no selected org may perform platform-level operations where source permits.
- Scoped new documents receive the request-context org automatically.
- Cap-counting models update `organization.subscription.recordCount` on creation/permanent deletion.
- Repair IDs are unique within an org and generated as `REP-####`.
- User email uniqueness respects source soft-delete behavior.
- Monetary fields preserve rounding semantics.

## Acceptance criteria
- All models initialize and indexes build.
- Tenant A queries cannot return Tenant B data.
- Aggregations are scoped too.
- Creation without org context fails for normal users.
- Repair sequence is independent per organization.
- Database manifest is fully reconciled with source before phase signoff.
