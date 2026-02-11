# Reviewer Notes

## Summary

Added a new repository skill: `openspec-schema-authoring-guide`.

- Skill file: `.codex/skills/openspec-schema-authoring-guide/SKILL.md`
- Reference baseline: `.codex/skills/openspec-schema-authoring-guide/references/schema-comparison.md`

## Key Decisions

- Treated upstream `spec-driven` as the primary canonical standard.
- Used installed OpenSpec schema files as local canonical mirror for repeatable analysis.
- Used `openspec/schemas/minimalist/README.md` only as a local packaging/positioning example.

## What This Enables

- Faster, consistent drafting of new custom schemas.
- Better schema decision support via explicit `spec-driven` vs `tdd` vs `minimalist` comparison.
- Clear quality gate reminder: run `openspec schema review <schema-name>` for each modified schema under `openspec/schemas/`.

## Verification

- No files under `openspec/schemas/` were modified in this implementation, so schema review command was not required in this run.
