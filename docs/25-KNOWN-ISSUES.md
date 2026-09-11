# Known Issues and Open Questions

This file records verified source quirks and areas still requiring extraction. Do not silently resolve these during reconstruction.

## Verified source quirks
- `PATCH /api/users/:id/restore` is protected by authentication but the verified route currently has no explicit `authorize(...)` middleware.
- CORS in `app.js` currently accepts any origin callback while credentials are enabled. Production hardening may intentionally differ, but parity vs correction must be decided explicitly.
- The root package declares a dependency named `nstall`; its purpose has not yet been validated and may be accidental or legacy.

## Incomplete extraction areas
- Exact Plan schema/constants/seed values.
- Full organization/platform route/controller behavior.
- Exact auth token issuance/cookie flags.
- Complete field-level schemas for Customer, Supplier, Payment, SparePartUsage and Plan in reconstruction docs.
- Full request/response shapes for every controller.
- Exact filters/sorting/pagination for all list APIs.
- Exact report calculations.
- Detailed repair controller transition rules.
- Detailed spare-part side effects on supplier balances.
- Page-by-page UI layout, table columns, filters, forms, dialogs and responsive behavior.
- Shared component inventory and design tokens.
- Deployment topology beyond source-level clues.
- Automated test coverage present in the original repo, if any.

## Rule
An item stays open until it is either extracted from source and documented, or explicitly categorized as unknowable from repository evidence.
