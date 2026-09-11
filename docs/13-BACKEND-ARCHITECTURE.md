# Backend Architecture

## Runtime
- Node.js ES modules.
- Express application composition in `apps/server/app.js`.
- Server entrypoint in `apps/server/server.js`.
- MongoDB persistence via Mongoose.

## Layers
### Routes
Domain route modules define HTTP paths and RBAC requirements.

### Middleware
Verified middleware includes:
- `auth.middleware.js` for JWT authentication and request-context initialization.
- `rbac.middleware.js` for hierarchical role authorization.
- Express-level Helmet, CORS, JSON/urlencoded parsing, cookie parsing and centralized error handling.

### Controllers
Verified controllers exist for auth, customers, organizations, payments, plans, repairs, reports, spare-part usage, suppliers and users.

### Models
Mongoose schemas represent Counter, Customer, Organization, Payment, Plan, Repair, SparePartUsage, Supplier and User.

### Utilities/services
Cross-cutting logic includes organization scoping, request context, record-cap checks, transactions, payment filters, repair calculations, rounding and error helpers.

## Tenant-scoping mechanism
Authentication establishes `{ orgId, role }` request context. The `orgScopePlugin` automatically injects organization filters into normal queries and aggregation pipelines, auto-tags new documents, and optionally increments/decrements organization subscription record counts.

This mechanism is a core security boundary. Do not replace it with client-side filtering.

## Authorization
`authorize(minRole)` compares numeric role levels. A route requiring `manager` accepts manager, admin and superadmin unless an additional controller/UI rule blocks a role.

## Transactions
Payment flows use a transaction helper to atomically create payment records, update repair/spare-part payment state and update party outstanding balances.

## Reconstruction order
1. Environment and DB connection.
2. Request context and error helpers.
3. Base models and organization/plan models.
4. Org-scope plugin and cap logic.
5. Auth + RBAC.
6. Domain models.
7. Shared validators.
8. Controllers/services.
9. Routes.
10. Integration tests proving tenant isolation and payment atomicity.
