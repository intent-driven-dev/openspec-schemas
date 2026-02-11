# OpenSpec Schema Comparison Baseline

This baseline captures the current schema patterns available from the installed OpenSpec CLI and local repository docs.

## Canonical Standard: spec-driven

- Sequence: `proposal -> specs -> design -> tasks`
- Primary use: structured change planning before implementation
- Distinctive behavior:
  - Proposal defines capability contract for spec generation
  - Specs use delta operations (`ADDED`, `MODIFIED`, `REMOVED`, `RENAMED`)
  - Design captures technical decisions and tradeoffs
  - Tasks derive from both specs and design
- Apply gate: requires `tasks`
- Track file: `tasks.md`

## Alternate Upstream Pattern: tdd

- Sequence: `spec -> tests -> implementation -> docs`
- Primary use: test-first feature delivery
- Distinctive behavior:
  - Tests are authored before implementation
  - Implementation is explicitly guided by red/green workflow
  - Docs are generated after implementation
- Apply gate: requires `tests`
- Track file: none (`tracks: null`)

## Local Repository Example: minimalist

- Sequence: `specs -> tasks`
- Primary use: fast, low-risk, well-scoped changes
- Distinctive behavior:
  - Minimal artifact overhead
  - No proposal/design phase
- Apply gate: requires `tasks`
- Track file: `tasks.md`

Note: `minimalist` in this repository is a packaging and positioning example. Treat upstream `spec-driven` as canonical when deciding schema semantics.

## Custom Schema Design Heuristics

- Start from `spec-driven` semantics unless there is a strong reason to simplify.
- Remove artifacts only when you can preserve requirement clarity and apply safety.
- Add artifacts only when they encode meaningful quality gates (for example, security review or migration planning).
- Keep `requires` edges strict and acyclic.
- Make every template enforce the minimum structure needed for reliable downstream steps.
