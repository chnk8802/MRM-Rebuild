# Phase 07 — Integrations and Cross-Cutting Services

## Goal
Recreate non-page infrastructure and cross-domain behavior required for parity.

## Verified integrations/cross-cutting concerns
- MongoDB through Mongoose.
- JWT authentication.
- Cookie transport and Bearer-token fallback.
- React Query + Axios API access.
- Shared `@repo/validators` workspace package.
- Vercel client configuration exists in the source repository.
- Turbo/npm workspace orchestration.

## Cross-cutting backend utilities to reproduce
- Request context.
- Organization-scoping Mongoose plugin.
- Record-cap enforcement.
- Transactions.
- Rounded monetary fields/calculations.
- Payment eligibility filters.
- Repair balance calculations.
- Central error helpers.

## Platform/subscription work
- Reproduce Plan model/constants/seed data.
- Reproduce Organization subscription fields and caps.
- Verify organization creation/update behavior against controllers/platform routes before implementation.

## Acceptance criteria
- All cross-cutting helpers have direct tests.
- Integration failures are surfaced cleanly.
- Production configuration requirements are documented without storing secrets.
- Any deployment-provider-specific behavior is isolated from core business logic.
