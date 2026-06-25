## Context

The packaged `behaviour-driven` schema already establishes a feature-file-first workflow with commit checkpoints, Cucumber.js acceptance tests, HTML reports, and bounded acceptance attempts. Recent use exposed a weak spot after the failing acceptance checkpoint: once the suite is red, the schema does not say clearly enough that coverage is frozen, implementation should progress by business scenario slices, and each slice should keep running the full acceptance suite.

`features/` is executable behaviour documentation. `acceptance-tests/` is runtime and test glue that proves that documentation against the system.

## Goals / Non-Goals

**Goals:**
- Preserve existing feature files as canonical executable behaviour documents and update them semantically when behaviour changes.
- Commit full failing acceptance coverage before implementation begins.
- Keep acceptance coverage stable while implementation proceeds.
- Make implementation progress observable by passing business scenarios.
- Require full-suite acceptance runs for each implementation slice.

**Non-Goals:**
- Introduce a new acceptance runner or replace Cucumber.js.
- Change OpenSpec CLI behavior.
- Mandate a universal feature-file naming taxonomy for every downstream project.

## Decisions

1. Treat `features/` as canonical executable behaviour documentation.
   - Rationale: the feature files are the human-readable and machine-executable expression of the OpenSpec behaviour delta.
   - Rejected alternative: regenerate whole feature files on each change. That risks losing curated scenario wording and encourages duplicate feature files.

2. Treat `acceptance-tests/` as runtime/test glue.
   - Rationale: step definitions, fixtures, helpers, and runner configuration should support the feature files without redefining accepted behaviour.
   - Rejected alternative: track progress by pending or completed step definitions. Step definitions are plumbing; passing business scenarios are the actual progress signal.

3. Use recorded not-yet-implemented scenarios as the only expected reds during scenario-slice implementation.
   - Rationale: this keeps the full suite valuable while still allowing incremental implementation.
   - Rejected alternative: select scenarios by default change-id tags. Tags can be useful locally, but defaulting to tag selection hides cross-scenario regressions.

## Risks / Trade-offs

- More upfront acceptance work -> Mitigation: keep feature extraction and failing acceptance coverage as explicit gates with commit checkpoints.
- Full-suite runs may be slower than tag-scoped runs -> Mitigation: allow teams to optimize locally while preserving full-suite semantics in the packaged baseline.
- Legitimate behaviour corrections may be delayed by the freeze -> Mitigation: allow deliberate OpenSpec artifact updates before changing committed feature or acceptance coverage.

## Migration Plan

Update the packaged schema guidance, task template, README, and canonical spec. No data migration is required.

## Open Questions

- None.
