# Phase 06 — Domain Features

## Goal
Implement user-facing domains in dependency order so each completed slice can be verified independently.

## Recommended order
1. Customers.
2. Suppliers.
3. Users and technicians.
4. Repairs.
5. Spare-part usage.
6. Payments.
7. Reports.
8. Organization/platform administration.
9. Settings/profile refinements.
10. Public website parity.

## Per-feature procedure
For each domain:
1. Confirm shared constants/Zod schemas.
2. Confirm model fields/indexes/soft-delete behavior.
3. Confirm API routes and minimum roles.
4. Extract controller filters, sorts, pagination, side effects and response shapes.
5. Implement client service calls.
6. Recreate list/create/details/edit screens that exist in source.
7. Add loading, error, empty and success states.
8. Verify role visibility and server authorization.
9. Add acceptance tests.

## Repair-specific requirements
Preserve technician assignment, status updates, pickup state, organization-scoped repair IDs, service charge/discount/payment state and spare-part linkage.

## Payment-specific requirements
Preserve receivable/payable distinction, eligible item rules, partial payments, overpayment rejection, outstanding summaries and full-and-final settlement.

## Acceptance criteria
Every frontend route maps to a working backend flow and all feature-to-file relationships are entered into the manifests before phase completion.
