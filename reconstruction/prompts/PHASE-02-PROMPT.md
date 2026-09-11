# Phase 02 Prompt — Database

Execute only `reconstruction/02-DATABASE.md`.

Read `docs/07-DATABASE-SCHEMA.md`, `docs/08-DATA-FLOW.md`, `docs/14-BUSINESS-LOGIC.md`, and `reconstruction/manifests/DATABASE-MANIFEST.md` first.

Implement MongoDB/Mongoose connection utilities, request context, `orgScopePlugin`, record-cap accounting, Counter, Plan, Organization, User, Customer, Supplier, Repair, SparePartUsage, and Payment models with verified indexes/hooks/virtuals/tenant behavior.

Do not build API routes yet. Validate model loading, indexes/schema constraints where practical, tenant tagging/scoping behavior, repair ID generation, and record-count side effects. Report unknowns rather than inventing fields.