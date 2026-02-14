## 1. Implement the Change

- [x] 1.1 Decide where the new OpenCode skill should live in this repo (`.opencode/skills/<skill-name>/SKILL.md` vs `.codex/skills/<skill-name>/SKILL.md`) and align with existing conventions.

- [x] 1.2 Create the new skill for OpenCode users to author schemas in this repo.
  - Include `openspec schema init <name>` and `openspec schema fork <source> [name]` as the primary entry points.
  - Explain how to fork from:
    - a schema in this repo (e.g., `minimalist`, `event-driven`)
    - a built-in upstream schema available in the CLI (e.g., `spec-driven`, `tdd`)
  - Include schema validation guidance: `openspec schema validate <schema-name>`.
  - Mention `openspec schema which <schema-name>` for debugging schema resolution.
  - Avoid relying on `openspec schema review` (this CLI version does not expose it).

- [x] 1.3 Update the existing authoring guide skill (or replace it) so it no longer implies manual copying as the primary approach.
  - Ensure it explicitly prefers `openspec schema init` / `openspec schema fork`.
  - Keep references to upstream `spec-driven` as the canonical baseline.

- [x] 1.4 Add `CONTRIBUTING.md`.
  - Tool split:
    - OpenCode users: point to the repo skill as the guided workflow.
    - Other tools: provide raw copy/paste commands for `openspec schema init` and `openspec schema fork`.
  - Include:
    - repo layout expectations (`openspec/schemas/<schema-name>/schema.yaml` + `templates/`)
    - how to validate (`openspec schema validate <schema-name>`) for each changed schema under `openspec/schemas/`
    - PR checklist (schema validates, templates exist, schema README updated/added if appropriate)

- [x] 1.5 Add/update any repo docs that should link to `CONTRIBUTING.md` (e.g., `README.md`), if needed.

- [x] 1.6 Run a quick smoke check of instructions by executing:
  - `openspec schemas --json`
  - `openspec schema init --help`
  - `openspec schema fork --help`

- [x] 1.7 Validate schemas if any files under `openspec/schemas/` were modified:
  - `openspec schema validate minimalist`
  - `openspec schema validate event-driven`
  - plus any new schema names introduced

## 2. Verify and Wrap Up

- [x] 2.1 Validate acceptance criteria from `openspec/changes/schema-authoring-skill-contributing/specs/schema-authoring-skill-and-contributing.md`.

- [x] 2.2 Ensure all commands in `CONTRIBUTING.md` are consistent with this repo's CLI version (especially `openspec schema validate` vs `schema review`).

- [x] 2.3 Prepare concise reviewer notes:
  - What skill was added/updated
  - What changed in `CONTRIBUTING.md`
  - How contributors should validate schemas before PR
