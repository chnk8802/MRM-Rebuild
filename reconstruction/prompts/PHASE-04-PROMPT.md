# Phase 04 Prompt — Authentication and Authorization

Execute only `reconstruction/04-AUTH.md`.

Read `docs/09-AUTHENTICATION.md`, `docs/20-SECURITY.md`, `docs/15-STATE-MANAGEMENT.md`, and the API/route manifests.

Implement JWT login/logout/profile flows, password hashing, cookie-capable token handling with Bearer fallback, `protect` middleware, hierarchical RBAC, request-context establishment, and superadmin `x-org-id` tenant selection behavior.

Preserve role levels: guest < staff < manager < admin < superadmin. Validate 401 vs 403 behavior, non-superadmin org context, superadmin selected-org context, logout cookie clearing, and frontend-compatible profile responses.