# Dependencies and Shared Contracts

## Monorepo dependency model
The root project uses npm workspaces for `apps/*` and `packages/*`, orchestrated by Turbo.

The shared package `@repo/validators` is consumed by both the frontend and backend. This is not a convenience-only package: it is part of the application's contract layer and should be reconstructed early.

## Shared validator package
Verified exports include common helpers plus domain schemas for:
- authentication;
- users;
- organizations;
- customers;
- suppliers;
- repairs;
- spare-part usage;
- payments;
- reports.

Verified shared constants include domains for:
- users/roles;
- customers;
- repairs/statuses;
- payments;
- plans;
- organizations.

## Why this package matters
The backend imports validator constants directly into Mongoose schemas for enum constraints and uses Zod schemas in controllers for request validation. The frontend also depends on the same workspace package.

That means a rebuild must avoid duplicating independently-maintained role/status/payment enums in client and server code. The original architecture intentionally centralizes them.

Examples already verified from source include:
- User role enum used by Mongoose and frontend permission logic;
- Repair status and payment-status constants used by the Repair model;
- Payment method/type constants used by Payment model and controllers;
- customer type constants;
- plan/organization constants.

## Reconstruction order
1. Create workspace package `packages/validators`.
2. Restore constant exports.
3. Restore common validation helpers.
4. Restore all Zod schema modules.
5. Make both `apps/client` and `apps/server` depend on `@repo/validators` via workspace resolution.
6. Only then implement domain forms/controllers that rely on these contracts.

## Dependency families
### Client
React, React DOM, React Router, TanStack React Query, Axios, React Hook Form, Zod, Radix UI primitives, shadcn tooling, Tailwind CSS, Lucide, toast/date/UI helper libraries.

### Server
Express, Mongoose, JSON Web Token, bcryptjs, cookie-parser, CORS, Helmet, dotenv, Zod, and the shared validator workspace package.

### Root tooling
Turbo and npm workspaces.

## Reconstruction rule
Prefer the versions documented in `docs/04-TECH-STACK.md` when recreating package manifests. Where exact lockfile fidelity matters, derive pinned versions from the source package-lock rather than replacing dependencies with current latest releases.
