# Master Rebuild Guide

## Objective

Rebuild MRM from an empty working directory using only the material contained in this repository plus explicitly documented external prerequisites.

This guide is intentionally designed for AI assistants with limited context windows. Work must be executed in small verified phases rather than asking a model to generate the whole application at once.

## Hard safety boundary

Never modify `chnk8802/mrm`. It is a read-only evidence source. All reconstruction implementation belongs to `chnk8802/MRM-Rebuild`.

## Reconstruction contract

For every phase:

1. Read the phase document and all listed prerequisites.
2. Read only the linked specifications/manifests necessary for that phase.
3. Create or modify only the files explicitly in scope.
4. Do not silently invent missing contracts or configuration.
5. Record unresolved information as a gap.
6. Run the specified verification steps.
7. Compare results with the acceptance criteria.
8. Do not continue to the next phase until the current phase passes.

## Planned phase order

### Phase 0 — Evidence and specification
Audit the original repository and complete architecture, feature, dependency, route, API, data, environment, integration, and UI inventories.

### Phase 1 — Bootstrap
Create the workspace, package management configuration, shared tooling, linting/formatting, TypeScript/build configuration, and base development commands matching the documented architecture.

### Phase 2 — Data layer
Recreate data models, schemas, migrations, persistence clients, seed/dev data strategy, and data-access contracts.

### Phase 3 — Backend foundation
Recreate backend application structure, configuration, shared middleware, services, APIs, validation, errors, and observability foundations.

### Phase 4 — Authentication and authorization
Implement identity, sessions/tokens, roles, permissions, protected routes, and security behavior.

### Phase 5 — Frontend shell
Implement application shell, routing, global styles/design tokens, layouts, shared components, state/query foundations, and global loading/error handling.

### Phase 6 — Product features
Implement features one at a time using feature specifications and feature-to-file mappings. Each feature must have independent acceptance criteria.

### Phase 7 — External integrations
Configure and implement all documented third-party services using placeholders and setup instructions rather than embedded secrets.

### Phase 8 — Tests and quality gates
Recreate unit/integration/end-to-end tests and establish build, lint, type-check, and test gates.

### Phase 9 — Deployment
Recreate documented deployment/build configuration and provide environment-specific setup instructions.

### Phase 10 — Final validation
Validate the reconstructed product against the documented feature inventory, route/API manifests, UI specifications, business rules, and rebuild checklist.

## Required output of the evidence phase

Before implementation begins, the repository should contain authoritative manifests for files, routes, components, APIs, database/data models, environment variables, dependencies, external integrations, and feature-to-file relationships.

## AI handoff pattern

When using a new AI conversation, provide the relevant phase prompt from `reconstruction/prompts/`, tell the model to obey `AGENTS.md`, and ask it to complete only that phase. The model should return a list of changed files, verification performed, acceptance criteria results, and unresolved gaps.

## Completion definition

The reconstruction is complete only when a developer or AI can start with this repository, follow the documented setup and phase sequence, supply only explicitly documented external credentials/resources, and produce an application whose documented behavior matches the original MRM system within the defined acceptance criteria.
