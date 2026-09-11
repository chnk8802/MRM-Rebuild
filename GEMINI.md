# Gemini Entry Point

This repository is the reconstruction specification for the MRM application.

Start with:
1. `AGENTS.md`
2. `docs/00-START-HERE.md`
3. `reconstruction/00-MASTER-REBUILD-GUIDE.md`
4. `reconstruction/prompts/MASTER-PROMPT.md`
5. exactly one `PHASE-XX-PROMPT.md`

Never modify the historical `chnk8802/mrm` repository. It is reference-only. Write implementation only to the rebuild project.

Do not substitute frameworks or simplify away tenant isolation, RBAC, shared validation, soft deletion, payment transactions, organization selection, or other verified behaviors.

At the end of every phase, report files changed, validation run, passed/failed acceptance criteria, unresolved gaps, and the recommended next phase.
