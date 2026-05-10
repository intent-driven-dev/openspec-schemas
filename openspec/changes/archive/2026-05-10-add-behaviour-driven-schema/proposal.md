## Why

The previous `behaviour-driven` schema was implemented directly in `openspec/schemas/` without proposal-backed canonical spec coverage. Rebuilding it through OpenSpec gives the schema an auditable workflow contract before it is offered as an installable package again.

## What Changes

- Add a self-contained `behaviour-driven` schema under `openspec/schemas/behaviour-driven/`.
- Define a proposal-led workflow that captures behaviour in OpenSpec-mergeable `spec.md` delta files before design and task planning.
- Make the content inside the OpenSpec Markdown wrapper strongly Gherkin-style, using observable Given/When/Then scenarios.
- Add schema README documentation with fit guidance, activation instructions, workflow order, wrapper semantics, and validation steps.
- Restore the root README catalog entry for `behaviour-driven` after the schema package exists.

## Capabilities

### New Capabilities

- `behaviour-driven-schema-workflow`: Defines the packaged `behaviour-driven` schema, artifact order, Gherkin-in-Markdown spec guidance, README expectations, and validation gates.

### Modified Capabilities

- `custom-schema-packaging`: Restore `behaviour-driven` to the repository catalog once the proposal-backed schema package is implemented.

## Impact

- Adds files under `openspec/schemas/behaviour-driven/`.
- Updates the root `README.md` catalog.
- Does not modify OpenSpec CLI behavior or existing schema packages.
- Verification includes `openspec schema validate behaviour-driven` and strict change validation.
