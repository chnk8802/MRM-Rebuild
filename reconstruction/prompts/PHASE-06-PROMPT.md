# Phase 06 Prompt — Feature Pages

Execute only `reconstruction/06-FEATURES.md`.

Read `docs/03-FEATURE-INVENTORY.md`, `docs/10-API-REFERENCE.md`, `docs/12-UI-UX-SPECIFICATION.md`, `reconstruction/manifests/FEATURE-TO-FILE-MAP.md`, `ROUTE-MANIFEST.md`, and `COMPONENT-MANIFEST.md`.

Implement the route-level frontend features: Dashboard, repairs, payments, customers, suppliers, technicians, users, reports, settings/profile, and superadmin organizations. Use the verified API service module boundaries and shared common components.

For every page preserve loading, error, empty, create/edit/detail/list states; route permissions; form validation; pagination/filtering; destructive confirmations; and responsive behavior. Do not invent backend capabilities not present in the API manifest. Validate every registered route at each supported role level.