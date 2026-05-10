## Why

The previous `intent-driven` schema was implemented directly in `openspec/schemas/` without proposal-backed canonical spec coverage. Rebuilding it through OpenSpec gives the schema an auditable workflow contract before it is offered as an installable package again.

## What Changes

- Add a self-contained `intent-driven` schema under `openspec/schemas/intent-driven/`.
- Base the workflow on `behaviour-driven` Gherkin-in-Markdown specs so default OpenSpec archive can merge `spec.md` files.
- Add an ADR stage between design and tasks for durable architectural decisions.
- Preserve ADR placement rules from `spec-driven-with-adr`: ADR files live under the target repository's top-level `adr/` folder, not inside `openspec/changes/`.
- Add schema README documentation with fit guidance, activation instructions, workflow order, Markdown wrapper semantics, ADR persistence, and validation steps.
- Restore the root README catalog entry for `intent-driven` after the schema package exists.

## Capabilities

### New Capabilities

- `intent-driven-schema-workflow`: Defines the packaged `intent-driven` schema, artifact order, Gherkin-in-Markdown spec guidance, ADR persistence rules, README expectations, and validation gates.

### Modified Capabilities

- `custom-schema-packaging`: Restore `intent-driven` to the repository catalog once the proposal-backed schema package is implemented.

## Impact

- Adds files under `openspec/schemas/intent-driven/`.
- Updates the root `README.md` catalog.
- Does not modify OpenSpec CLI behavior or existing schema packages.
- Verification includes `openspec schema validate intent-driven` and strict change validation.
