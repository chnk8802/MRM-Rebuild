# Glossary

**MRM** — Mobile Repair Management application represented by the original `chnk8802/mrm` source repository.

**Organization / tenant** — A business account whose data is isolated through `orgId` scoping.

**Superadmin** — Platform-level role. Not required to belong to an organization; may select an organization context.

**Admin** — Organization-level administrator with broad user/report/business-data permissions.

**Manager** — Mid-level role with access to payments, customers, suppliers, technicians, repair creation/editing, and reports where permitted.

**Staff** — Base authenticated operational role. Can access common repair workflows and selected CRUD operations.

**Guest** — Lowest RBAC level defined in backend hierarchy; not observed as a normal protected-app role in the verified route map.

**Request context** — Async server context containing `orgId` and role, established by authentication middleware and consumed by tenant-scoping logic.

**orgScopePlugin** — Mongoose plugin that automatically filters tenant-scoped queries/aggregations, tags new documents with `orgId`, and optionally maintains subscription record counts.

**Record cap** — Subscription-related maximum/usage concept tied to `Organization.subscription.recordCount` and plan/cap checks.

**Repair** — Core repair-order entity containing customer, device/problem, technician, service charge, status, payment state, pickup state, and spare-part references.

**Repair ID** — Human-facing per-organization sequential ID such as `REP-0001`.

**Spare Part Usage** — A part installed/used for a repair, optionally linked to a supplier, with quantity/cost/payment tracking.

**Receivable** — Money owed to the organization by a customer for repair work.

**Payable** — Money owed by the organization to a supplier for spare parts.

**Full and final payment** — Transaction that settles all currently outstanding eligible line items for a customer or supplier in one operation.

**Soft delete** — Marking an entity deleted with `isDeleted` while retaining the record for restore/permanent-delete workflows.

**Shared validators** — `packages/validators`, the workspace package exporting shared Zod schemas and constants to frontend and backend.

**Server state** — Remote API data managed primarily with TanStack React Query rather than React Context.
