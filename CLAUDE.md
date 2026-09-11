# Claude Entry Point

This repository is an AI-independent reconstruction specification for MRM.

Read `AGENTS.md` first. Then read `docs/00-START-HERE.md` and `reconstruction/00-MASTER-REBUILD-GUIDE.md`.

Use `reconstruction/prompts/MASTER-PROMPT.md` plus exactly one numbered phase prompt at a time.

Critical rule: `chnk8802/mrm` is historical reference-only. Never modify it. All implementation belongs in the rebuild project.

Prefer specification fidelity over modernization. Preserve React/Vite, Express, MongoDB/Mongoose, shared validators, tenant scoping, hierarchical RBAC, cookie-capable JWT auth, soft-delete behavior, and transactional payment rules unless the reconstruction docs explicitly say otherwise.
