# Start Here — MRM Reconstruction Documentation

## Purpose

This documentation records the existing MRM system in enough detail to support a clean-room-style reconstruction in `MRM-Rebuild`.

## Repository boundary

- Original reference: `chnk8802/mrm` — READ ONLY.
- Reconstruction target: `chnk8802/MRM-Rebuild` — all new work goes here.

## Current observed repository facts

Status: **Observed from the original repository root**.

The original MRM repository is organized as a monorepo. Its root currently contains:

- `.gitignore`
- `apps/`
- `packages/`
- `package.json`
- `package-lock.json`
- `turbo.json`

The presence of `turbo.json` together with workspace-style `apps/` and `packages/` directories indicates a Turbo-based monorepo organization. The exact applications, packages, frameworks, dependencies, data stores, and deployment architecture will be documented only after inspecting their source files.

## Documentation status legend

Every substantial document should use these evidence states:

- **Observed** — directly verified in source/configuration.
- **Inferred** — strongly derived from observed implementation but not explicitly declared.
- **Unknown** — cannot be established from repository evidence yet.
- **External** — requires information outside the GitHub repository.

## Planned documentation set

The documentation pass will cover project overview, product requirements, feature inventory, technology stack, architecture, folder structure, database/data models, data flow, authentication, APIs, frontend architecture, UI/UX, backend architecture, business logic, state management, environment variables, local development, build/deployment, testing, security, error handling, observability, dependencies, third-party services, known issues, design decisions, glossary, and a rebuild checklist.

## How to use these documents

A human or AI rebuilding MRM should first read the project overview and architecture documents, then the manifests, then follow `reconstruction/00-MASTER-REBUILD-GUIDE.md` in order. Do not implement a later phase before its prerequisites and acceptance criteria are satisfied.

## Documentation quality requirement

The objective is not merely to describe source code. The documentation must explain observable product behavior and connect it end-to-end: user action -> UI/component -> state/validation -> API/backend -> persistence/integration -> result/error -> verification.
