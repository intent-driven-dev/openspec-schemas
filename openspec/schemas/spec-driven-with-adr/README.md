# Spec-Driven With ADR OpenSpec Schema

`spec-driven-with-adr` is for changes that need the standard proposal-to-tasks
OpenSpec flow plus durable Architecture Decision Records.

Key references:
- Article: https://intent-driven.dev/blog/2026/04/29/spec-driven-development-with-adr/

[![Spec-Driven Development with ADR](https://img.youtube.com/vi/y5oemaPsmOA/hqdefault.jpg)](https://youtu.be/y5oemaPsmOA)

- Good fit: architectural changes, platform decisions, cross-module work, new
  service boundaries, technology choices, or changes where future contributors
  need a persistent decision trail.
- Not a good fit: small tactical fixes, content-only edits, simple UI changes,
  or work where `specs -> tasks` is enough.

## Install (copy/paste)

Use the root `README.md` single-line install command with:
- `SCHEMA="spec-driven-with-adr"`

## Activate

Set this in `openspec/config.yaml`:

```yaml
schema: spec-driven-with-adr
```

## Stage Gates

Artifact order:
`proposal -> specs -> design -> adr -> tasks`

Gate expectations:
- `specs` must be based on the capabilities identified in `proposal.md`.
- `design` must account for the proposal, specs, and currently in-force ADRs.
- `adr` records durable decisions after design and before task planning.
- `tasks` are planned only after proposal, specs, design, and ADR artifacts are
  complete.

## ADR Persistence

ADR files are generated under the target repository's top-level `adr/` folder,
not only inside the OpenSpec change folder. Accepted ADRs are immutable. If a
future decision changes a prior ADR, create a new ADR that supersedes the old
one and leave the original file unchanged.

## Note

- For ADR skills please refer to: [Intent-Driven-Template Skills](https://github.com/intent-driven-dev/intent-driven-template/tree/main/.agents/skills/architectural-decision-records).
- This skill takes care of choosing the ADR style/template used by this schema.

## Pending

- Package schema and associated skills together.

For more schemas, refer to https://github.com/intent-driven-dev/openspec-schemas.
