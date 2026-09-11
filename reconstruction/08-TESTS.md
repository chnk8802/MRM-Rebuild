# Phase 08 — Tests

## Goal
Build automated evidence that the reconstruction matches verified source behavior.

## Required suites
- Shared validator unit tests.
- Role hierarchy and ProtectedRoute tests.
- Authentication middleware tests.
- Tenant-scoping model tests.
- Record-cap accounting tests.
- CRUD/soft-delete/restore/permanent-delete API tests.
- Repair lifecycle tests.
- Spare-part usage tests.
- Payment transaction tests.
- Report query tests.
- Frontend page/service integration tests.
- End-to-end happy paths by role.

## Mandatory adversarial tests
- Cross-tenant read/update/delete attempts.
- Forged `x-org-id` from non-superadmin.
- Overpayment attempts.
- Payment transaction failure rollback.
- Access to manager/admin/superadmin endpoints from lower roles.
- Access to soft-deleted records.
- Invalid ObjectIds and malformed Zod payloads.

## Acceptance criteria
- No critical path depends only on manual testing.
- Every API manifest row has at least authorization and happy-path coverage.
- Financial and tenant-isolation suites are green before deployment work begins.
