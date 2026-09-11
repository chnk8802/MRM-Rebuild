# Phase 04 — Authentication and Authorization

## Goal
Recreate JWT session handling, user context, hierarchical RBAC and frontend auth state.

## Server
- Login issues JWT according to source behavior.
- Protected requests accept `token` cookie first, then Bearer token.
- JWT verification reloads the user from MongoDB.
- Missing/deleted user invalidates the request.
- Establish request context with user role and organization.
- For superadmin only, allow selected organization via `x-org-id`.
- Implement role hierarchy: guest 1, staff 2, manager 3, admin 4, superadmin 5.

## Client
- Auth context loads current profile.
- Login/logout mutate auth state.
- ProtectedRoute redirects unauthenticated users to `/login` and underprivileged users to `/unauthorized`.
- Navigation visibility matches authorization rules but never replaces server enforcement.

## Security acceptance
- Invalid JWT -> 401.
- Insufficient role -> 403.
- Normal user cannot switch org with `x-org-id`.
- Superadmin selected-org context scopes tenant data.
- Protected-route refresh restores session state correctly.
- Document and test the source route anomaly for user restore before deciding parity vs correction.
