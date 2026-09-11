# State Management

## Verified global state
The client uses React Context for global application state.

### Authentication context
Source: `apps/client/src/context/AuthContext.jsx`

State:
- `user`
- `organization`
- `loading`
- `selectedOrgId`

Startup behavior:
1. Request `GET /auth/profile` through the shared Axios instance.
2. If authenticated, store the returned user.
3. For non-superadmins, fetch the current organization through `organizationService.getMyOrganization()`.
4. On failure, clear user and organization state.
5. Mark auth loading complete.

Login behavior:
- POST `/auth/login` with email/password.
- Store returned user.
- Non-superadmins then fetch their organization.

Logout behavior:
- POST `/auth/logout`.
- Clear user and organization.
- Clear selected organization.
- Redirect browser to `/login`.

### Selected organization state
Superadmin tenant selection is stored in local storage under the shared `ORG_STORAGE_KEY` constant. The Axios request interceptor reads that value and sends it as `x-org-id` on requests.

This state is security-sensitive because backend request context uses `x-org-id` for superadmin tenant scoping.

### Theme context
A separate `ThemeContext.jsx` exists and is responsible for theme state. The exact theme persistence behavior should be preserved from source during implementation.

## Server/cache state
The frontend depends on `@tanstack/react-query`. Page-level data fetching should use the existing query/mutation patterns found in the source rather than moving server data into global context.

## Form state
Forms use `react-hook-form` with Zod-based validation through `@hookform/resolvers` and the shared `@repo/validators` package.

## Reconstruction requirements
- Keep auth state and theme state separate.
- Do not store the JWT manually in React state; authentication works with cookie credentials and optionally bearer tokens at the backend.
- Preserve selected organization local-storage behavior for superadmins.
- Preserve React Query as the server-state layer.
- Preserve React Hook Form + shared Zod validators for form state/validation.
