## Context

`intent-driven` was removed because it existed as a direct schema implementation without proposal-backed canonical spec coverage. The replacement should combine the archived `behaviour-driven` Gherkin-in-Markdown spec model with ADR persistence from `spec-driven-with-adr`.

## Goals / Non-Goals

**Goals:**

- Package `intent-driven` as an installable schema folder with `schema.yaml`, README, and templates.
- Preserve proposal-led intent capture, Gherkin-style Markdown specs, design, ADRs, task planning, and tracked apply behavior.
- Keep behaviour specs mergeable by OpenSpec archive as `spec.md` files.
- Persist durable architecture decisions under the target repository's top-level `adr/` folder.
- Restore the root README catalog entry only after the schema package exists.

**Non-Goals:**

- Do not modify OpenSpec CLI behavior, archive behavior, or schema resolution.
- Do not introduce `.feature` files or packaged Gherkin linting in this schema.
- Do not write ADRs inside `openspec/changes/<change>/`.

## Decisions

1. Fork `behaviour-driven` and add an ADR artifact.

   Rationale: `behaviour-driven` already has the desired mergeable spec wrapper and Gherkin-style authoring guidance. Adding ADR support keeps intent-driven focused on durable decision capture.

2. Reuse ADR persistence rules from `spec-driven-with-adr`.

   Rationale: this repository already has an accepted ADR workflow: top-level `adr/`, immutable accepted ADRs, and supersession through new ADR files.

3. Keep tasks dependent on `specs` and `adr`.

   Rationale: implementation planning should happen only after behaviour, design, and durable decisions are settled.

## Risks / Trade-offs

- Contributors may skip ADRs for design decisions that should persist -> ADR instructions define the bar for durable decisions and say not to invent ADRs when nothing qualifies.
- Contributors may try to create `.feature` files -> Schema instructions explicitly say `spec.md` is the OpenSpec wrapper and Gherkin style belongs inside Markdown requirement/scenario blocks.
- ADR output is outside the change folder -> README and artifact instructions state the path contract explicitly.

## Migration Plan

1. Fork `behaviour-driven` to `intent-driven`.
2. Add ADR artifact instructions and template.
3. Update design and task dependencies around ADRs.
4. Add README and catalog documentation.
5. Validate the schema, then archive this change so canonical specs record the workflow.

Rollback is deleting `openspec/schemas/intent-driven/` and removing its root README catalog entry; no OpenSpec runtime files are modified.

## Open Questions

None.
