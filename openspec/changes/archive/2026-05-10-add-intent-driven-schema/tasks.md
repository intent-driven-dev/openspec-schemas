## 1. Recreate Schema Package

- [x] 1.1 Fork `behaviour-driven` into `openspec/schemas/intent-driven/`.
- [x] 1.2 Update `schema.yaml` metadata and workflow description for `intent-driven`.
- [x] 1.3 Add an `adr` artifact after `design` and before `tasks`.
- [x] 1.4 Add ADR persistence and supersession instructions from `spec-driven-with-adr`.
- [x] 1.5 Keep the `specs` artifact as `specs/**/*.md` from `spec.md` with Gherkin-in-Markdown guidance.
- [x] 1.6 Set task dependencies so `tasks` requires `specs` and `adr`.

## 2. Add Templates And Documentation

- [x] 2.1 Add `templates/adr.md`.
- [x] 2.2 Confirm the schema package does not include `.gherkin-lintrc` or `.feature` templates.
- [x] 2.3 Review `proposal.md`, `spec.md`, `design.md`, and `tasks.md` templates for consistency with the schema instructions.
- [x] 2.4 Add `openspec/schemas/intent-driven/README.md` with fit guidance, activation, workflow order, Markdown wrapper semantics, ADR persistence, and validation.
- [x] 2.5 Restore the root README catalog entry for `intent-driven`.

## 3. Verify

- [x] 3.1 Run `openspec schema validate intent-driven`.
- [x] 3.2 Run `openspec validate add-intent-driven-schema --type change --strict`.
- [x] 3.3 Confirm no packaged Gherkin lint config or `.feature` template exists in `openspec/schemas/intent-driven/`.
