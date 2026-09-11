# Phase 05 — Frontend Shell

## Goal
Recreate the application shell, routing, providers and shared UI foundations before domain screens.

## Implement
- React/Vite entrypoint and provider composition.
- React Query provider.
- Auth context.
- Router with public, unauthorized and protected app branches.
- `Layout`, `Sidebar`, `Topbar` component boundaries.
- Shared UI primitives from the verified Radix/shadcn/Tailwind stack.
- Toast/error feedback foundation.
- Axios instance and service-module pattern.

## Routes to establish
- `/`
- `/login`
- `/unauthorized`
- `/app`
- nested placeholders for all routes in `ROUTE-MANIFEST.md`.

## Acceptance criteria
- Public home renders unauthenticated.
- `/app` redirects unauthenticated users to login.
- Role-gated routes enforce the verified hierarchy.
- Layout persists while nested pages change.
- Sidebar/topbar can render role-appropriate navigation.
- API instance sends credentials as required by source behavior.
