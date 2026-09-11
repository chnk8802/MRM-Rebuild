# File Manifest

Status: **In progress**

This manifest will become the authoritative inventory of files and directories required to understand and reconstruct MRM.

## Source repository root — observed

| Path | Type | Reconstruction significance |
| --- | --- | --- |
| `.gitignore` | file | Ignore rules and clues about generated/local artifacts |
| `apps/` | directory | Application workspaces; detailed inventory pending |
| `packages/` | directory | Shared/internal packages; detailed inventory pending |
| `package.json` | file | Root workspace scripts/dependencies; inspection pending |
| `package-lock.json` | file | Locked dependency graph; detailed dependency extraction pending |
| `turbo.json` | file | Turbo task/pipeline configuration; inspection pending |

## Manifest rules

For each significant source file, record:

- original path
- category
- owning application/package
- purpose
- imports/dependencies
- dependents where identifiable
- feature(s) served
- reconstruction destination
- reconstruction phase
- evidence status
- notes/gaps

Generated output, dependency directories, caches, and other non-source artifacts should be documented as such rather than treated as implementation source.
