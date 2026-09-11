# Testing Strategy

## Goal
Prove functional parity, authorization correctness, tenant isolation and financial consistency before treating the reconstruction as complete.

## Required test layers
### Unit tests
Cover pure calculations, validation schemas, role-level comparison, payment remaining-balance calculations and helper utilities.

### Model/integration tests
Use a test MongoDB database and verify:
- org-scoped models automatically filter by request organization;
- new scoped documents receive `orgId`;
- cross-tenant reads/updates/deletes are blocked by scoping;
- record-count increments/decrements remain correct;
- repair IDs are sequential within an organization;
- soft-deleted records behave as expected.

### API tests
For every endpoint in `reconstruction/manifests/API-MANIFEST.md`, test:
- no token -> 401 where protected;
- insufficient role -> 403;
- permitted role -> expected status/shape;
- invalid payload -> validation failure;
- invalid/missing resource -> correct error;
- tenant A cannot access tenant B records.

### Financial workflow tests
Payment tests are mandatory because multiple models change in one transaction. Verify partial payment, exact settlement, rejected overpayment, full-and-final receivable settlement, full-and-final payable settlement, outstanding summary, and rollback on transaction failure.

### Frontend tests
At minimum verify route guards, role visibility, loading/error/empty states, form validation and service/API integration for each page group.

### End-to-end acceptance
Exercise the complete workflow: organization/plan setup -> admin/user -> customer -> repair -> technician/status -> spare part -> receivable/payable payment -> report.

## Completion gate
A phase is not complete merely because it compiles. Its acceptance checks must pass and any deviation from verified source behavior must be recorded in `docs/25-KNOWN-ISSUES.md` or `docs/26-DESIGN-DECISIONS.md`.
