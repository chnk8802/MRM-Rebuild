# Design Decisions

This file records architecture/design decisions that are directly visible in the source so a reconstruction AI does not unintentionally replace them with different patterns.

## Monorepo
Use npm workspaces with `apps/*` and `packages/*`, orchestrated by Turbo.

## Separate SPA and API
Frontend is a React/Vite SPA. Backend is a separate Express service. Do not collapse the application into Next.js or another full-stack framework during fidelity reconstruction.

## Shared validation package
Client and server both depend on `@repo/validators`. Shared constants and Zod schemas are part of the contract and should remain centralized.

## MongoDB/Mongoose
Persistence uses Mongoose schemas, hooks, indexes, virtuals, plugins, and transactions. Replacing MongoDB with SQL would change important behavior and is out of scope for a faithful rebuild.

## Automatic tenant scoping
Organization isolation is enforced partly at the Mongoose plugin layer via request context, not only inside controllers. This is deliberate defense-in-depth and must be preserved.

## Hierarchical RBAC
Role levels are numeric/hierarchical: guest < staff < manager < admin < superadmin. `authorize('manager')` means manager or above.

## Superadmin organization context
Superadmins are not tied to an `orgId`; they can select a tenant, persisted in localStorage, which Axios transmits using `x-org-id`.

## Cookie-capable authentication
The backend accepts the token from a `token` cookie first, with Bearer token fallback. The client sends credentials with Axios.

## Soft deletion
Several business entities use `isDeleted` and include restore/permanent-delete workflows rather than immediate destruction.

## Record-cap accounting
Tenant-scoped models can opt into `countsTowardCap`; their create/delete lifecycle automatically adjusts `Organization.subscription.recordCount`.

## Financial consistency via transactions
Payment creation and full-and-final settlement update multiple documents inside MongoDB transaction helpers. Preserve atomic behavior.

## UI component strategy
The frontend combines Tailwind CSS with Radix primitives/shadcn-style components and reusable common components such as page headers, filters, pickers, row actions, dialogs, and async selectors.

## Reconstruction priority
Fidelity beats modernization. Improvements may be proposed only after the verified behavior has been reproduced and validated.
