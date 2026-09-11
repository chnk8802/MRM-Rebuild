# Phase 07 Prompt — Integrations and Cross-Cutting Wiring

Execute only `reconstruction/07-INTEGRATIONS.md`.

Read `docs/08-DATA-FLOW.md`, `docs/15-STATE-MANAGEMENT.md`, `docs/24-THIRD-PARTY-SERVICES.md`, and all reconstruction manifests.

Wire frontend service modules to backend endpoints; verify React Query invalidation/refetch behavior; connect repair/spare-part/payment relationships; connect dashboard/report data; connect organization/plan selection; and ensure shared validators are consumed by both applications.

Do not add unverified SaaS services. Validate end-to-end flows for login, tenant selection, repair lifecycle, customer/supplier CRUD, spare-part usage, payments, reports, and logout.