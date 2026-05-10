## 1. Recreate Schema Package

- [x] 1.1 Fork the built-in `spec-driven` schema into `openspec/schemas/behaviour-driven/`.
- [x] 1.2 Update `schema.yaml` metadata, artifact descriptions, and artifact dependencies for `behaviour-driven`.
- [x] 1.3 Keep the `specs` artifact as `specs/**/*.md` from `spec.md` for OpenSpec archive compatibility.
- [x] 1.4 Add Gherkin-in-Markdown authoring instructions to the `proposal`, `specs`, and `tasks` artifact guidance.
- [x] 1.5 Add `apply.tracks: tasks.md` and apply instructions aligned with the spec-driven baseline.

## 2. Add Templates And Documentation

- [x] 2.1 Confirm the schema package does not include `.gherkin-lintrc` or `.feature` templates.
- [x] 2.2 Update `templates/spec.md` with OpenSpec delta wrapper plus Gherkin-style scenario structure.
- [x] 2.3 Review `proposal.md`, `design.md`, and `tasks.md` templates for consistency with the schema instructions.
- [x] 2.4 Add `openspec/schemas/behaviour-driven/README.md` with fit guidance, activation, workflow order, Markdown wrapper semantics, and validation.
- [x] 2.5 Restore the root README catalog entry for `behaviour-driven`.

## 3. Verify

- [x] 3.1 Run `openspec schema validate behaviour-driven`.
- [x] 3.2 Run `openspec validate add-behaviour-driven-schema --type change --strict`.
- [x] 3.3 Confirm no packaged Gherkin lint config or `.feature` template exists in `openspec/schemas/behaviour-driven/`.
