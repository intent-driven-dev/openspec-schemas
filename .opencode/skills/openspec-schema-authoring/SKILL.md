---
name: openspec-schema-authoring
description: Create or customize OpenSpec workflow schemas in this repository using `openspec schema init` and `openspec schema fork`.
license: MIT
compatibility: Requires openspec CLI.
metadata:
  author: openspec-schemas
  version: "1.0"
---

Use this skill when you want to add or customize an OpenSpec workflow schema in this repository.

**Goal**: produce a copyable schema folder under `openspec/schemas/<schema-name>/` containing `schema.yaml` and `templates/`.

**Steps**

1. **Choose whether you're starting fresh or forking**

   If you want a brand-new workflow schema, use `init`.
   If you want to customize an existing workflow (recommended), use `fork`.

2. **Discover available schema sources**

   List schemas available to fork (both this repo and upstream packages):
   ```bash
   openspec schemas --json
   ```

3. **Option A: Create a new schema from scratch (init)**

   Create a new project-local schema folder:
   ```bash
   openspec schema init <schema-name>
   ```

   Common flags:
   - `--description "..."` to describe the workflow
   - `--artifacts "proposal,specs,design,tasks"` to set the artifact IDs (comma-separated)
   - `--default` to set the schema as the project default
   - `--no-default` to skip the interactive prompt to set as default

   Result (expected): `openspec/schemas/<schema-name>/schema.yaml` and `openspec/schemas/<schema-name>/templates/`.

4. **Option B: Customize an existing workflow (fork)**

   Copy an existing schema into this repo so you can edit it:
   ```bash
   openspec schema fork <source> [new-schema-name]
   ```

   Sources can be:
   - A schema already in this repo (e.g., `minimalist`, `event-driven`)
   - A built-in upstream schema provided by the CLI (e.g., `spec-driven`, `tdd`)

   Result (expected): a new folder under `openspec/schemas/<new-schema-name>/` containing `schema.yaml` + `templates/`.

5. **Edit schema internals (minimal expectations)**

   When updating `openspec/schemas/<schema-name>/schema.yaml` and templates, ensure:
   - `artifacts[].id` matches the intended workflow sequence
   - `artifacts[].requires` matches dependencies
   - `artifacts[].generates` matches output paths that templates will create
   - Template files exist under `openspec/schemas/<schema-name>/templates/` for each artifact

6. **Validate the schema locally (required quality gate)**

   Run validation for every schema you changed:
   ```bash
   openspec schema validate <schema-name>
   ```

   Note: some CLI versions mention `openspec schema review`, but this repo's workflow standardizes on `openspec schema validate`.

7. **Debug schema resolution (if validation or behavior is surprising)**

   Confirm which schema folder the CLI is using:
   ```bash
   openspec schema which <schema-name>
   ```

**Guardrails**
- Prefer `openspec schema fork` over manual copying.
- Keep schemas as copyable, repository-local folders under `openspec/schemas/`.
- Always run `openspec schema validate` before opening a PR.
