---
name: openspec-schema-authoring-guide
description: Understand OpenSpec schema internals (with spec-driven as the primary standard) and design custom schemas for this repository.
license: MIT
compatibility: Requires openspec CLI.
metadata:
  author: openspec-schemas
  version: "1.0"
---

Use this skill when the user wants to understand OpenSpec workflow schemas deeply, compare schema patterns, or create a new custom schema in this repo.

## Source Of Truth

1. Primary standard: upstream `spec-driven` schema
   - `https://github.com/Fission-AI/OpenSpec/tree/main/schemas/spec-driven`
   - Local canonical mirror (installed CLI):
     - `/Users/harikrishnan/.nvm/versions/node/v24.4.0/lib/node_modules/@fission-ai/openspec/schemas/spec-driven/schema.yaml`
     - `/Users/harikrishnan/.nvm/versions/node/v24.4.0/lib/node_modules/@fission-ai/openspec/schemas/spec-driven/templates/*.md`
2. Secondary comparison set: other upstream schemas (`tdd`, etc.)
3. Local example only (not canonical behavior source):
   - `openspec/schemas/minimalist/README.md`

If guidance conflicts, prioritize upstream `spec-driven` behavior.

## What To Extract

When analyzing a schema, always capture:

- `artifacts[].id` sequence and execution order
- `artifacts[].requires` dependency graph
- `artifacts[].generates` output contract
- Template expectations (`template` files)
- `apply.requires` and `apply.tracks` behavior
- Authoring constraints implied by instructions and templates

## Operating Procedure

1. Inspect schema definitions first:
```bash
openspec schemas --json
```
2. Deep-read `spec-driven` (`schema.yaml` + templates) and summarize:
- why each artifact exists
- what inputs it depends on
- what output shape it enforces
3. Compare with at least one alternate schema (typically `tdd`) to explain tradeoffs.
4. Read local `minimalist` README strictly to understand repo packaging/positioning style.
5. Propose custom schema design:
- artifact sequence
- dependency edges
- apply gate (`apply.requires`)
- template set and required sections
6. If implementing schema files under `openspec/schemas/`, include verification:
```bash
openspec schema review <schema-name>
```
for each affected schema.

## Custom Schema Drafting Checklist

- Name and one-sentence purpose
- Clear "good fit" / "not a good fit"
- Artifact list with explicit IDs and `requires`
- Minimal but strict templates for each artifact
- Apply contract (`requires`, optional `tracks`)
- Migration notes if replacing existing workflows
- Verification commands to run before completion

## Expected Output Style

When asked to help author a schema, produce:

1. A concise comparison table (`spec-driven` vs candidate flow)
2. A proposed `schema.yaml` skeleton
3. Template file skeletons
4. Tradeoff notes (complexity, rigor, speed)
5. Validation checklist (including `openspec schema review`)

## References

For a prebuilt comparison baseline, use:
- `.codex/skills/openspec-schema-authoring-guide/references/schema-comparison.md`
