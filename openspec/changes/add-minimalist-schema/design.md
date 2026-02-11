## Context

This repository is being established as a catalog of reusable, project-local OpenSpec schemas. The first schema, `minimalist`, is intentionally narrow: it should support well-scoped small changes by skipping proposal/design artifacts and proceeding directly through specs and tasks. The repository also needs repeatable packaging guidance so coding agents can install any schema by copying one folder.

## Goals / Non-Goals

**Goals:**
- Define a consistent per-schema folder contract that can scale to multiple custom schemas.
- Provide installation and activation instructions targeted at coding-agent workflows.
- Define `minimalist` as a disciplined workflow with explicit fit boundaries.

**Non-Goals:**
- Creating a universal schema that covers complex architectural or cross-cutting changes.
- Replacing or modifying upstream OpenSpec packaged schemas.
- Adding automation tooling for publishing or remote distribution in this change.

## Decisions

1. One folder per schema under a repository-level schema collection directory.
   - Rationale: Keeps each schema self-contained (`schema.yaml`, templates, and docs) and easy to copy.
   - Alternative considered: Flat files at repo root. Rejected because it does not scale or communicate boundaries well.

2. `minimalist` schema artifact chain is `specs -> tasks` only.
   - Rationale: For INVEST-friendly work, proposal/design overhead slows delivery and is often redundant.
   - Alternative considered: Keep proposal as lightweight stub. Rejected to preserve the schema's explicit minimalism.

3. Fit guidance is documentation-first, not hard-gated by tooling.
   - Rationale: Teams need judgment flexibility; strict automated guards are brittle.
   - Alternative considered: Enforce scope checks in scripts. Rejected for now due to complexity and false positives.

4. Coding-agent installation path is copy-based and local-first.
   - Rationale: Matches current OpenSpec local schema model and works without package infrastructure.
   - Alternative considered: Centralized installer command. Deferred until schema set stabilizes.

## Risks / Trade-offs

- [Risk] `minimalist` is used for complex changes and skips needed design work.
  - Mitigation: Document clear "good fit / not a fit" examples and escalation guidance.
- [Risk] Schema folder structure drifts as more schemas are added.
  - Mitigation: Standardize per-schema README sections and template layout from the first schema onward.
- [Risk] Copy-based installation can lead to stale local schema versions.
  - Mitigation: Include simple update guidance in README and keep schema version notes.

## Migration Plan

1. Add `minimalist` schema folder with `schema.yaml`, templates, and README guidance.
2. Add repository-level documentation describing folder-per-schema conventions.
3. Validate schema structure and template resolution with OpenSpec CLI.

Rollback: remove the local `minimalist` schema folder and related documentation updates if needed.

## Open Questions

- No open questions for this change.
- Version metadata for schema folders is intentionally deferred for now.
- A repository-root `README.md` with agent quick-start guidance is in scope and will direct users to each schema README.
