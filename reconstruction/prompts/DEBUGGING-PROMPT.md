# Debugging Prompt

Use this in a fresh AI conversation when a reconstructed MRM phase is failing.

You are debugging a fidelity reconstruction of MRM. Do not redesign the architecture unless the specification proves the current design is wrong.

Read:
1. `AGENTS.md`
2. the reconstruction phase that introduced the failing behavior
3. `reconstruction/manifests/FEATURE-TO-FILE-MAP.md`
4. relevant API/database/component manifests
5. relevant docs for auth, business logic, state, errors, and security

Then:
- reproduce the failure
- identify the narrowest failing layer (UI, API service, route, middleware, controller, model, validator, tenant context, transaction, environment)
- compare actual behavior to documented behavior
- patch only the rebuild project
- run focused tests, then broader validation
- explicitly verify no cross-tenant or RBAC regression

Never modify the historical `chnk8802/mrm` repository.

Report root cause, files changed, tests run, result, and any unresolved specification ambiguity.