# Authentication and Authorization

## Authentication transport
The backend `protect` middleware accepts a JWT from either:
1. the `token` cookie, or
2. an `Authorization: Bearer <token>` header.

The token is verified with `JWT_SECRET`. The decoded payload must contain a user id (`decoded.id`). The middleware reloads that user from MongoDB and rejects requests when the user no longer exists.

Verified failure responses include:
- 401: `Not authorized, no token`
- 401: `User no longer exists`
- 401: `Not authorized, token failed`

## Request context and tenant selection
After authentication, `req.user` is populated. The middleware then creates an AsyncLocalStorage-style request context containing `orgId` and `role`.

For ordinary users, organization context always comes from `user.orgId`.

For a `superadmin`, the middleware accepts an optional `x-org-id` request header. This allows a superadmin to operate inside a selected tenant. When no organization is selected, superadmin queries may intentionally run without an organization filter where the scoped model permits that behavior.

This behavior is reconstruction-critical. Do not replace it with a frontend-only organization selector or ad-hoc query filters.

## Role hierarchy
The backend defines exact numeric role levels:

| Role | Level |
|---|---:|
| guest | 1 |
| staff | 2 |
| manager | 3 |
| admin | 4 |
| superadmin | 5 |

`authorize('manager')` means manager **or above**, not manager-only. Multiple role arguments are treated as alternative minimum thresholds.

Authorization failures return HTTP 403 with a message indicating the required role(s) or above.

## Verified auth endpoints
Base path: `/api/auth`

| Method | Path | Auth | Purpose |
|---|---|---|---|
| POST | `/register` | Public | Register user |
| POST | `/login` | Public | Log in |
| POST | `/logout` | Public route handler | Log out / clear auth state |
| GET | `/profile` | Protected | Get current profile |
| PATCH | `/profile` | Protected | Update current profile |
| PATCH | `/profile/password` | Protected | Change own password |

## Frontend route protection
The React application mirrors the hierarchical role model through `ProtectedRoute` and `usePermission()`.

Unauthenticated users are redirected to `/login`. Insufficient-role users are redirected to `/unauthorized`. `blockRoles` can override the hierarchy for explicit exceptions; current code uses this to prevent `superadmin` from using organization-admin user-create/edit screens.

## Reconstruction requirements
- Preserve both cookie and Bearer-token authentication unless deliberately migrating the protocol.
- Preserve the `x-org-id` superadmin tenant-selection behavior.
- Keep backend authorization authoritative. Frontend route hiding is not a security boundary.
- Preserve role hierarchy and exception logic.
- Load the authenticated user from storage after JWT verification rather than trusting role/org claims in the JWT alone.
- Add tests for absent token, invalid token, deleted user, each role threshold, and superadmin tenant selection.
