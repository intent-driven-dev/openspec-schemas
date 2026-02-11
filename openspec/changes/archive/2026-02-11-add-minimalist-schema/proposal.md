## Why

This repository is intended to host reusable custom OpenSpec schemas, but it does not yet provide a first usable schema package. We need a minimal schema and repo structure that teams and coding agents can copy into local OpenSpec setups immediately.

## What Changes

- Add the first custom schema, `minimalist`, focused on lightweight work that can skip proposal/design and go directly from specs to tasks.
- Define clear usage guidance for when `minimalist` is and is not appropriate (INVEST-friendly, small, low-risk work).
- Add install/activation documentation so coding agents can use a single copy-paste install line from the root README and set `schema: <name>` in `openspec/config.yaml`.
- Establish a scalable repository layout with one folder per custom schema.
- Add a repository-root `README.md` that explains the purpose of this repo and provides an agent quick start that points users to individual schema READMEs.

## Capabilities

### New Capabilities
- `custom-schema-packaging`: Define the repository packaging and documentation pattern for distributing project-local OpenSpec schemas.
- `minimalist-schema-workflow`: Define and document a `specs -> tasks` workflow schema intended for already well-scoped, small changes.

### Modified Capabilities
- None.

## Impact

- Affects `openspec/schemas/` structure and schema files/templates.
- Adds repository-level documentation in `README.md`.
- Defines activation guidance for downstream repositories via `openspec/config.yaml`.
- Influences how future schema additions are organized and documented in this repository.
