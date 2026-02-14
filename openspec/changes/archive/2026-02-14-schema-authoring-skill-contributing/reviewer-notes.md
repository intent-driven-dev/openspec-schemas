# Reviewer Notes

## Summary

Added contributor-facing guidance for authoring workflow schemas via `openspec schema init` / `openspec schema fork`, and standardized validation on `openspec schema validate`.

- New OpenCode skill: `.opencode/skills/openspec-schema-authoring/SKILL.md`
- Updated existing authoring guide skill: `.codex/skills/openspec-schema-authoring-guide/SKILL.md`
- Added: `CONTRIBUTING.md`
- Linked from: `README.md`

## Key Decisions

- New OpenCode skill lives under `.opencode/skills/` (aligns with existing OpenCode skills in this repo).
- Prefer `openspec schema fork` (customize) and `openspec schema init` (new) over manual copying.
- Use `openspec schema validate` as the quality gate; mention that `openspec schema review` is not relied on in this repo.

## Verification

- Ran: `openspec schemas --json`
- Ran: `openspec schema init --help`
- Ran: `openspec schema fork --help`
- No files under `openspec/schemas/` were changed, so schema validation was not required in this run.
