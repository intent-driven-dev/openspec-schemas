## Context

`behaviour-driven` was removed because it existed as a direct schema implementation without proposal-backed canonical spec coverage. The replacement should be small, self-contained, and close to the standard `spec-driven` workflow while making the contents of mergeable Markdown specs read like Gherkin.

## Goals / Non-Goals

**Goals:**

- Package `behaviour-driven` as an installable schema folder with `schema.yaml`, README, and templates.
- Preserve proposal-led intent capture, design, task planning, and tracked apply behavior.
- Keep behaviour specs mergeable by OpenSpec archive as `spec.md` files.
- Make requirement/scenario content use Gherkin-style Given/When/Then language.
- Restore the root README catalog entry only after the schema package exists.

**Non-Goals:**

- Do not modify OpenSpec CLI behavior, archive behavior, or schema resolution.
- Do not add ADR support to `behaviour-driven`; that belongs to `intent-driven`.
- Do not introduce `.feature` files or packaged Gherkin linting in this schema.

## Decisions

1. Fork the built-in `spec-driven` schema and edit only the artifact contracts that differ.

   Rationale: the desired workflow still uses proposal, design, tasks, and apply tracking. Forking preserves known OpenSpec behavior and reduces custom surface area.

2. Use OpenSpec `specs/**/*.md` files as the wrapper and make scenario content Gherkin-style.

   Rationale: default OpenSpec archive only merges `spec.md` delta files. The wrapper keeps archive compatibility while the content still expresses behaviour with Given/When/Then scenarios.

3. Leave Gherkin linting outside the schema package.

   Rationale: the schema is responsible for OpenSpec workflow and mergeable spec shape. External projects can lint their own stricter Gherkin conventions independently.

4. Keep validation local to this repository's schema quality gates.

   Rationale: `openspec schema validate behaviour-driven` verifies the package without requiring OpenSpec CLI changes.

## Risks / Trade-offs

- Contributors may try to create `.feature` files -> Schema instructions explicitly say `spec.md` is the OpenSpec wrapper and the Gherkin style belongs inside Markdown requirement/scenario blocks.
- Contributors may confuse `behaviour-driven` with ADR workflows -> README fit guidance explicitly directs durable decision workflows to `intent-driven`.
- Schema validation may flag missing templates or invalid references -> Keep schema files self-contained and validate before archive.

## Migration Plan

1. Recreate the schema from the built-in `spec-driven` baseline.
2. Replace the specs artifact guidance with Gherkin-in-Markdown authoring instructions.
3. Add README and catalog documentation.
4. Validate and review the schema, then archive this change so canonical specs record the workflow.

Rollback is deleting `openspec/schemas/behaviour-driven/` and removing its root README catalog entry; no OpenSpec runtime files are modified.

## Open Questions

None.
