# Security

## Verified security mechanisms
- Helmet is enabled on the Express app.
- Authentication accepts JWT from `token` cookie or `Authorization: Bearer ...`.
- JWTs are verified with `JWT_SECRET`.
- User existence is rechecked on protected requests.
- Hierarchical RBAC is enforced server-side.
- Tenant context is established after authentication and injected into Mongoose queries/aggregations by `orgScopePlugin`.
- Passwords are excluded from normal User query output through `select: false`.

## Critical trust boundaries
### Tenant isolation
The Mongoose org-scoping plugin is security-critical. Rebuild tests must prove one organization's users cannot read, mutate or delete another organization's scoped records.

### Superadmin tenant selection
Superadmin may supply `x-org-id`. This header is privileged context and must never be honored for ordinary roles.

### Authentication transport
The original middleware supports both cookie and Bearer token transport. Cookie security attributes must be verified from auth controller/token helper code before final deployment.

### Secrets
Never commit `JWT_SECRET`, MongoDB credentials, production cookies/tokens or other secrets. `.env.example` must contain placeholders only.

## Risks requiring explicit review
- CORS currently accepts any origin callback with credentials enabled; production reconstruction should document whether exact parity or tightened origin allowlisting is desired.
- `PATCH /api/users/:id/restore` is protected by authentication but, in the verified route, has no explicit RBAC middleware. Treat this as a known behavior/security review item rather than silently assuming intended authorization.
- Soft-delete and permanent-delete privileges need endpoint-level tests.

## Required security acceptance tests
- Missing/invalid/expired JWT rejected.
- Deleted/nonexistent user token rejected.
- Role escalation impossible through client parameters.
- Tenant header ignored for non-superadmin.
- Cross-tenant CRUD denied by data scoping.
- Password fields never serialized in normal API responses.
- Validation rejects malformed IDs and payloads.
