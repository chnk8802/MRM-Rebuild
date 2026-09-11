# Master Reconstruction Prompt

Use this prompt in a fresh AI conversation when rebuilding MRM.

---

You are reconstructing the MRM mobile-repair management application from the specification repository currently available to you.

## Source of truth
Treat the files in this repository as the reconstruction specification. Read these first:
1. `AGENTS.md`
2. `docs/00-START-HERE.md`
3. `reconstruction/00-MASTER-REBUILD-GUIDE.md`
4. the numbered reconstruction phase file you are executing
5. relevant manifests under `reconstruction/manifests/`

## Critical safety rule
The historical repository `chnk8802/mrm` is reference-only. Never modify it. All implementation work belongs in the new/rebuild project repository or local workspace.

## Fidelity rule
Reproduce verified behavior before proposing modernization. Do not silently replace:
- React/Vite with another frontend framework
- Express with another backend framework
- MongoDB/Mongoose with another persistence system
- shared `@repo/validators`
- hierarchical RBAC
- Mongoose tenant scoping
- cookie-capable JWT authentication
- soft-delete/restore semantics
- transactional payment behavior

## Execution rule
Work on exactly one reconstruction phase at a time. Do not jump ahead.

For the selected phase:
1. Read its phase file completely.
2. Read every linked documentation/manifests section.
3. List the exact files you will create/change.
4. Implement only that scope.
5. Run available build/lint/tests relevant to the phase.
6. Check every acceptance criterion.
7. Report created/changed files, commands run, results, and unresolved gaps.
8. Do not claim success if acceptance criteria fail.

## Handling uncertainty
If documentation marks something as unknown, do not fabricate it. Use a conservative implementation consistent with verified architecture and record the uncertainty for later validation.

## Completion format
Return:
- Phase completed
- Files created/changed
- Validation performed
- Acceptance criteria passed/failed
- Remaining blockers
- Recommended next phase

Start only when given a phase number or phase filename.
