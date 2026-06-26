# Agent Install Guide

Use this flow when installing any schema from this repository into an existing OpenSpec project.

## Prerequisites

1. Run `openspec --version` in the target project. Confirm OpenSpec is installed and the CLI version is at least `1.0.0`.
2. If `openspec --version` fails, reports a version below `1.0.0`, or `openspec/config.yaml` is missing, stop and tell the user to install or upgrade OpenSpec and run `openspec init` first. Do not continue until these prerequisites are met.

## Step 1 — Clone This Repository

```bash
git clone https://github.com/intent-driven-dev/openspec-schemas.git /tmp/openspec-schemas
```

## Step 2 — Select a Schema

**If the user already named a schema**, check that it exists in the clone:

```bash
ls /tmp/openspec-schemas/openspec/schemas/<schema-name>
```

If the directory exists, proceed with that schema. If it does not exist, fall through to the enumeration path below.

**If no schema was named** (or the named schema was not found), list what is available and ask the user to pick exactly one:

```bash
ls /tmp/openspec-schemas/openspec/schemas/
```

Do not proceed with copy/activation until exactly one schema name is confirmed.

## Step 3 — Copy the Schema

Copy the chosen schema directory (referred to as `<schema-name>` below) into the target project. Copy the full directory recursively to keep `schema.yaml`, the schema `README.md`, and all nested `templates/` files together. Choose one of these install locations:

**Option A — Project local (recommended):**

```bash
mkdir -p ./openspec/schemas
cp -R /tmp/openspec-schemas/openspec/schemas/<schema-name> ./openspec/schemas/<schema-name>
```

**Option B — User level (available across projects):**

```bash
cp -R /tmp/openspec-schemas/openspec/schemas/<schema-name> $HOME/.openspec/schemas/<schema-name>
```

## Step 4 — Activate the Schema

Update `openspec/config.yaml` in the target project to activate the installed schema:

```yaml
schema: <schema-name>
```

Also update the `rules` keys to match the artifact IDs in the schema's `schema.yaml` (`artifacts[].id`). For example:

- `intent-driven` uses `proposal`, `specs`, `design`, `adr`, and `tasks` → set those as `rules` keys
- Check `openspec/schemas/<schema-name>/schema.yaml` (`artifacts[].id`) for the exact IDs of your chosen schema

## Step 5 — Validate

Run:

```bash
openspec schema validate
```

Expected success output (example for `intent-driven`):

```text
Validation Results:
✓ intent-driven
```

Replace `intent-driven` with the schema name you installed. If validation fails, report the error output to the user.
