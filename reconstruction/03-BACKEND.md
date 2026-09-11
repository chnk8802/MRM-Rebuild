# Phase 03 — Backend API

## Goal
Recreate the Express API surface and controller/service boundaries after the database layer is stable.

## Implement
- Express app middleware: Helmet, CORS, JSON/urlencoded parsing, cookie parsing and centralized error handling.
- Route modules for auth, users, technicians, customers, suppliers, repairs, spare-part usage, payments, reports, organizations and platform routes.
- Controllers and supporting services/utilities.
- Shared Zod request/query validation.
- Transaction helper for multi-model financial updates.

## Source-of-truth files
Use `docs/10-API-REFERENCE.md` and `reconstruction/manifests/API-MANIFEST.md`. Where they are incomplete, inspect the corresponding source controller before implementing.

## Critical behavior
- Preserve exact minimum roles per endpoint.
- Preserve soft-delete/restore/permanent-delete distinctions.
- Preserve pagination/filter/sort semantics discovered in controllers.
- Financial writes that touch multiple models must be transactional.
- Do not trust client-provided organization scope for normal users.

## Acceptance criteria
- Every manifest endpoint exists.
- Route-level RBAC tests pass.
- Error status semantics match documented source behavior.
- No controller bypasses tenant scoping accidentally.
- API response shapes are documented and verified before frontend integration.
