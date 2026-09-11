# MRM Rebuild

This repository is the independent reconstruction workspace for the MRM application.

## Source of truth

The original repository `chnk8802/mrm` is a **read-only reference** for this project. It must never be modified as part of the reconstruction effort.

All generated documentation, reconstruction specifications, prompts, manifests, configuration examples, and rebuilt application code belong in this repository: `chnk8802/MRM-Rebuild`.

## Primary goal

Create a self-contained reconstruction package detailed enough that the MRM application can be rebuilt from an empty directory using an AI assistant, including lower-capability or free-plan models, without depending on access to the original repository once the reconstruction package is complete.

## Documentation principles

1. Prefer explicit instructions over assumptions.
2. Record exact file paths, dependencies, routes, schemas, APIs, states, validation rules, and acceptance criteria.
3. Separate observed facts from inferred behavior.
4. Never copy secrets or production credentials.
5. Every reconstruction phase must be small enough to execute independently.
6. Every phase must include verification steps and acceptance criteria.
7. The original MRM repository is read-only.

## Repository areas

- `docs/` — detailed documentation of how the original application works.
- `reconstruction/` — ordered instructions for rebuilding the application from scratch.
- `reconstruction/prompts/` — AI-ready prompts for individual reconstruction phases.
- `reconstruction/manifests/` — machine-readable/human-readable indexes of files, features, APIs, routes, components, data models, and dependencies.
- `specifications/` — detailed behavior specifications for pages, components, APIs, database entities, and workflows.

Start with [`docs/00-START-HERE.md`](docs/00-START-HERE.md) and [`reconstruction/00-MASTER-REBUILD-GUIDE.md`](reconstruction/00-MASTER-REBUILD-GUIDE.md).
