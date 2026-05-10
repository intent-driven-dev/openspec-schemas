# Intent-Driven OpenSpec Schema

`intent-driven` is the standard OpenSpec proposal-to-tasks workflow with
Gherkin behaviour specs and durable Architecture Decision Records.

It is for changes where contributor intent should be captured up front,
observable behaviour should be expressed as executable-style examples, and
long-lived architecture choices should be preserved for future changes.

- Good fit: product or platform changes with meaningful user/domain behaviour,
  architectural decisions, cross-module work, or features that benefit from
  Gherkin acceptance scenarios.
- Not a good fit: small tactical fixes, content-only edits, dependency bumps, or
  work where `specs -> tasks` is enough.

## Install (copy/paste)

Use the root `README.md` single-line install command with:
- `SCHEMA="intent-driven"`

## Activate

Set this in `openspec/config.yaml`:

```yaml
schema: intent-driven
```

## Stage Gates

Artifact order:
`proposal -> specs -> design -> adr -> tasks`

Gate expectations:
- `proposal` states why the change matters and lists the capabilities that need
  behaviour specs.
- `specs` creates one Gherkin feature file per capability at
  `specs/<capability>/spec.feature`.
- `design` explains the implementation approach and accounts for currently
  in-force ADRs.
- `adr` records durable architectural decisions after design and before task
  planning.
- `tasks` are planned only after proposal, Gherkin specs, design, and ADR
  artifacts are complete.

## Gherkin Specs

Feature files must be valid Gherkin and pass the schema lint config:

```bash
npx gherkin-lint -c openspec/schemas/intent-driven/.gherkin-lintrc \
  "openspec/specs/**/*.feature" \
  "openspec/changes/<change>/specs/**/*.feature"
```

Each feature file should contain one `Feature:`, optional `Rule:` groups, and
concrete `Scenario:` examples with observable `Given`, `When`, and `Then` steps.
Do not use Markdown requirement delta headers inside `.feature` files.

## ADR Persistence

ADR files are generated under the target repository's top-level `adr/` folder,
not only inside the OpenSpec change folder. Accepted ADRs are immutable. If a
future decision changes a prior ADR, create a new ADR that supersedes the old
one and leave the original file unchanged.

For more schemas, refer to https://github.com/intent-driven-dev/openspec-schemas.
