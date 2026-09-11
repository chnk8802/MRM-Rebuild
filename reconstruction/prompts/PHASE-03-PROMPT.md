# Phase 03 Prompt — Backend

Execute only `reconstruction/03-BACKEND.md`.

Read `docs/10-API-REFERENCE.md`, `docs/13-BACKEND-ARCHITECTURE.md`, `docs/14-BUSINESS-LOGIC.md`, `docs/21-ERROR-HANDLING.md`, `reconstruction/manifests/API-MANIFEST.md`, and `FEATURE-TO-FILE-MAP.md`.

Implement Express app/server composition, central error handling, controllers, services/utilities, and all non-auth domain routes for organizations/plans, users/technicians, customers, suppliers, repairs, spare-part usage, payments, and reports. Preserve route-level minimum roles and transaction boundaries.

Do not implement frontend pages. Validate route registration, representative success/error paths, pagination/filter behavior, payment atomicity, and tenant isolation.