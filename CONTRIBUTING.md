# Contributing

This repo contains OpenSpec workflow schemas (folders under `openspec/schemas/`). Contributions typically add a new schema or refine an existing one.

## Prerequisites

- OpenSpec CLI installed and available as `openspec`

## Repo Layout

- Schemas live in `openspec/schemas/<schema-name>/`
  - `schema.yaml`
  - `templates/` (markdown templates used by `openspec instructions ...`)

## How Schemas Are Used

In a project, schemas are selected in `openspec/config.yaml` (for example by setting a default schema name). In this repository, schemas must remain copyable as self-contained folders under `openspec/schemas/`.

## Create Or Customize A Schema

### If you are using OpenCode (recommended)

Use the repo skill:

- `openspec-schema-authoring`

It guides you through `openspec schema init` / `openspec schema fork`, validation, and repo layout expectations.

### If you are NOT using OpenCode

Discover available schema sources (repo + upstream):
```bash
openspec schemas --json
```

Create a new schema from scratch:
```bash
openspec schema init <schema-name> --description "..." --artifacts "proposal,specs,design,tasks"
```

Or customize an existing schema (recommended):
```bash
openspec schema fork <source> [new-schema-name]
```

## Validate Before You Open A PR

Run validation for each schema you changed under `openspec/schemas/`:
```bash
openspec schema validate <schema-name>
```

If you are debugging schema resolution (e.g., you are not sure which schema folder is being used):
```bash
openspec schema which <schema-name>
```

## PR Checklist

- `openspec schema validate <schema-name>` passes for every schema you changed
- `templates/` contains templates for every artifact declared in `schema.yaml`
- Schema README added/updated if appropriate
- Any repo docs that reference contributing are updated to point to this guide
