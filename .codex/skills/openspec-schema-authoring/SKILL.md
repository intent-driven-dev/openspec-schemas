---
name: openspec-schema-authoring
description: Create or customize OpenSpec workflow schemas in this repository using `openspec schema init` and `openspec schema fork`. Use when the user wants to add, fork, or validate a schema under `openspec/schemas/`.
license: MIT
compatibility: Requires openspec CLI.
metadata:
  author: openspec
  version: "1.0"
  generatedBy: "1.0.0"
---

Create or customize an OpenSpec workflow schema in this repository.

**Goal**: produce a repository-local schema folder under `openspec/schemas/<schema-name>/` containing `schema.yaml` and `templates/`.

**Steps**

1. **Decide whether to initialize or fork**

   - Use `init` for a brand-new schema.
   - Use `fork` to customize an existing schema (preferred when starting from a known workflow).

2. **Discover available schemas to fork**

   ```bash
   openspec schemas --json
   ```

3. **Option A: Initialize a new schema**

   ```bash
   openspec schema init <schema-name>
   ```

   Common flags:
   - `--description "..."` to describe the workflow
   - `--artifacts "proposal,specs,design,tasks"` to set artifact IDs
   - `--default` to set as project default
   - `--no-default` to skip the interactive default prompt

   Expected result: `openspec/schemas/<schema-name>/schema.yaml` and `openspec/schemas/<schema-name>/templates/`.

4. **Option B: Fork an existing schema**

   ```bash
   openspec schema fork <source> [new-schema-name]
   ```

   Sources can be:
   - Repository-local schemas
   - Built-in upstream schemas provided by the CLI

   Expected result: `openspec/schemas/<new-schema-name>/schema.yaml` and `openspec/schemas/<new-schema-name>/templates/`.

5. **Edit schema internals**

   Ensure:
   - `artifacts[].id` matches intended workflow sequence
   - `artifacts[].requires` matches dependencies
   - `artifacts[].generates` matches artifact output paths
   - Template files exist in `openspec/schemas/<schema-name>/templates/` for each artifact

6. **Validate changed schemas (required)**

   ```bash
   openspec schema validate <schema-name>
   ```

7. **Debug schema resolution if behavior is unexpected**

   ```bash
   openspec schema which <schema-name>
   ```

**Done Criteria**
- Schema exists under `openspec/schemas/<schema-name>/`.
- `schema.yaml` and `templates/` are both present.
- `openspec schema validate <schema-name>` passes.

**Guardrails**
- Prefer `openspec schema fork` over manual copying.
- Keep schemas repository-local under `openspec/schemas/`.
- Do not skip validation before considering work complete.
