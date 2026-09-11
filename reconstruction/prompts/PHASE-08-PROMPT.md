# Phase 08 Prompt — Tests

Execute only `reconstruction/08-TESTS.md`.

Read `docs/19-TESTING-STRATEGY.md`, `docs/20-SECURITY.md`, `docs/21-ERROR-HANDLING.md`, and `docs/28-REBUILD-CHECKLIST.md`.

Add/complete automated tests for shared validators, models, tenant scoping, auth/RBAC, API routes, payment transactions, repair lifecycle rules, and critical frontend flows. Include negative tests for cross-tenant leakage and role violations.

Run lint/build/tests. Do not mark the phase complete if tenant isolation, payment atomicity, auth flows, or role restrictions lack coverage. Report commands and failures exactly.