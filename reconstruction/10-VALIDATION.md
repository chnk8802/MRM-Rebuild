# Phase 10 — Final Validation

## Goal
Prove that the reconstruction is complete enough to replace the reference implementation for documented behavior.

## Validation matrix
### Structure
- Workspace/package layout matches intended reconstruction architecture.
- All required environment variables are documented.
- All manifests are reconciled against source.

### Functional parity
- Every frontend route in `ROUTE-MANIFEST.md` is implemented.
- Every API endpoint in `API-MANIFEST.md` is implemented.
- Every model in `DATABASE-MANIFEST.md` is implemented.
- All documented role restrictions behave correctly.
- Soft-delete/restore/permanent-delete semantics match.
- Repair lifecycle and payment workflows match.

### Security
- Tenant-isolation tests pass.
- RBAC tests pass.
- Authentication/session tests pass.
- Known source anomalies are explicitly accepted or corrected through a recorded design decision.

### UX
- Loading/error/empty/success states exist.
- Desktop and mobile behavior has been compared with source implementation.
- Forms and validation messages are consistent with shared validators.

### Operations
- Fresh local setup works using docs only.
- Build/lint/test commands succeed.
- Production deployment procedure is documented and repeatable.

## Completion rule
Do not mark reconstruction complete while any item in `docs/28-REBUILD-CHECKLIST.md` marked REQUIRED is unresolved. Unknowns must be documented rather than guessed.
