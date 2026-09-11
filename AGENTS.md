# MRM Rebuild — AI Agent Instructions

## Non-negotiable repository boundary

`chnk8802/mrm` is the original MRM source repository and is READ-ONLY for this reconstruction project.

DO NOT create, edit, delete, rename, commit, merge, branch, open pull requests, modify issues, or perform any other mutation in `chnk8802/mrm`.

The only repository that may be modified for reconstruction work is:

`chnk8802/MRM-Rebuild`

If a task appears to require changing the original repository, stop and implement the equivalent work in `MRM-Rebuild` instead.

## Mission

Produce a self-contained, AI-independent reconstruction of MRM. The final repository must contain enough documentation, specifications, manifests, prompts, setup instructions, and eventually implementation code to rebuild the application without needing the original source repository.

## Evidence rules

When documenting the original application:

- Mark directly observed behavior/configuration as `Observed`.
- Mark conclusions derived from multiple code paths as `Inferred`.
- Mark missing information as `Unknown / requires verification`.
- Never invent environment values, credentials, API keys, database contents, external-service settings, or production infrastructure.
- Never include secrets from any source even if they become visible.

## Required reconstruction granularity

For each feature document, identify where applicable:

- purpose and user outcome
- entry points and routes
- exact source/rebuild file paths
- frontend components
- backend handlers/services
- data models/tables/collections
- API contracts
- authentication and authorization
- validation rules
- state transitions
- loading, empty, success, and error states
- third-party integrations
- environment variables
- edge cases
- responsive behavior
- dependencies
- implementation order
- verification procedure
- acceptance criteria

## Small-model compatibility

Reconstruction instructions must not assume a model remembers the whole project. Each implementation phase should contain sufficient local context, explicit prerequisites, exact files to touch, required interfaces, and tests/acceptance criteria.

## Canonical documentation

The canonical project knowledge lives under `docs/`, `reconstruction/`, and `specifications/`. Model-specific files such as `CLAUDE.md` and `GEMINI.md` must point back to these canonical sources rather than creating competing specifications.
