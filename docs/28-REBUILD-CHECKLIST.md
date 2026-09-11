# Rebuild Checklist

Status legend: `[ ]` not verified, `[x]` documented/verified. A checked documentation item does not mean implementation code already exists.

## Repository and guardrails
- [x] Source `chnk8802/mrm` designated read-only.
- [x] Rebuild work isolated to `chnk8802/MRM-Rebuild`.
- [x] AI guardrails documented in `AGENTS.md`.

## Product and architecture
- [x] Project overview.
- [x] Product requirements baseline.
- [x] Feature inventory baseline.
- [x] Tech stack.
- [x] System architecture.
- [x] Folder structure baseline.
- [x] Data flow baseline.
- [x] Authentication/RBAC baseline.
- [x] Backend architecture baseline.
- [x] Frontend architecture baseline.
- [x] UI/UX architecture baseline.
- [ ] Page-by-page visual specification complete.
- [ ] Component-by-component specification complete.

## Data layer
- [x] Model inventory.
- [x] Multi-tenant org-scoping behavior.
- [x] Repair ID generation behavior.
- [x] Subscription record-count behavior.
- [ ] Every model field, enum, index and virtual fully reconciled.
- [ ] Plan seed values fully documented.

## API and business logic
- [x] API mount points documented.
- [x] Route/RBAC manifest baseline.
- [x] Payment business logic baseline.
- [x] Soft-delete/restore/permanent-delete behavior baseline.
- [ ] Every controller request schema documented.
- [ ] Every controller response shape documented.
- [ ] Every list filter/sort/pagination option documented.
- [ ] Repair state-transition rules fully documented.
- [ ] Reports calculations fully documented.
- [ ] Platform organization/plan endpoints fully documented.

## Frontend
- [x] Top-level route tree documented.
- [x] Page-group inventory documented.
- [x] API service-module inventory documented.
- [x] Authenticated shell component boundaries documented.
- [ ] Every page's API calls mapped.
- [ ] Every table column/filter/action mapped.
- [ ] Every form field/default/validation mapped.
- [ ] Dialog/toast/loading/empty/error states mapped.
- [ ] Responsive behavior mapped.

## Environment and operations
- [x] Required server env vars baseline.
- [x] Local development guide.
- [x] Testing strategy.
- [x] Security baseline.
- [x] Error handling baseline.
- [ ] Deployment source config fully extracted.
- [ ] Observability/logging behavior fully documented.
- [ ] Third-party service inventory finalized.

## Reconstruction execution package
- [x] Master rebuild guide.
- [x] Phase 01 Bootstrap.
- [x] Phase 02 Database.
- [x] Phase 03 Backend.
- [x] Phase 04 Auth.
- [x] Phase 05 Frontend Shell.
- [x] Phase 06 Features.
- [x] Phase 07 Integrations.
- [x] Phase 08 Tests.
- [x] Phase 09 Deployment.
- [x] Phase 10 Validation.
- [ ] MASTER-PROMPT.md finalized.
- [ ] Per-phase small-context AI prompts finalized.
- [ ] Debugging prompt finalized.
- [ ] Component manifest complete.
- [ ] Environment manifest complete.
- [ ] Feature-to-file map complete.
- [ ] Dependency map complete.

## Final completion gate
- [ ] All REQUIRED open items above resolved.
- [ ] Fresh clone can be rebuilt from docs without original repo.
- [ ] Automated parity tests pass.
- [ ] Tenant-isolation tests pass.
- [ ] Financial transaction tests pass.
- [ ] UI parity review complete.
- [ ] Known source anomalies explicitly accepted or corrected via design decision.
