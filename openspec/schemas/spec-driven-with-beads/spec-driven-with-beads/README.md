# spec-driven-with-beads

OpenSpec custom schema that uses [Beads](https://github.com/gastownhall/beads) molecules for task tracking, execution, and durable knowledge retention across sessions.

## Workflow

```
proposal → specs → design → tasks+beads → apply (via molecule) → consolidate
```

## Molecule structure

```
bd-xyz (epic: Spec-driven Change: my-feature)
├── bd-xyz.1  proposal                (human, needs: —)
├── bd-xyz.2  specs                   (needs: proposal)
├── bd-xyz.3  design                  (needs: specs)
├── bd-xyz.4  implement               (needs: design)
├── bd-xyz.5  verify-specs-consolidate (auto-injected by spec-compliance aspect)
└── bd-xyz.6  consolidate             (human, needs: implement, verify-specs)
```

One `bd pour` creates the entire graph. No manual `bd create` × N.

## What makes this different

Other schemas end at `archive` — knowledge dies with the session. This one closes the learning loop via `bd remember` + `bd mol distill`.

### Key features

| Feature | Description | Default |
|---------|-------------|---------|
| Mandatory deps | `needs:` in formula — `bd ready` only shows unblocked steps | Always on |
| Spec-compliance aspect | Auto-injects "Verify specs pass" before consolidate | Always on |
| Bond points | Compose additional behavior without forking the schema | Opt-in |
| `bd pin` | Pin steps to specific agents for parallel work | Opt-in (bond) |
| Async gates | Human approval, timers, CI checks | Opt-in (bond) |
| `bd lint` | Structural validation in consolidate | Always on |
| `bd mol squash` | Compress completed molecule to lightweight digest | Always on |
| `bd mol distill` | Extract reusable formula from completed change | Agent discretion |
| `bd remember` | Persist learnings across sessions via `bd prime` | Always on |

### Bond points

The formula defines three bond points where optional formulas attach:

| Bond point | Position | Optional behavior |
|---|---|---|
| `parallel-execution` | After implement | Split implement into parallel sub-steps, one per capability, each pinned to a different agent. Uses `waits_for` (fan-in) to rejoin before consolidate |
| `async-gates` | Before implement | Add human approval gates, timer delays, or GitHub CI checks. Blocks step progression until conditions are met |

Bond nothing → sequential, no extra config. Bond a formula → unlock the feature.

## Requirements

- [Beads](https://github.com/gastownhall/beads) installed (`bd` on PATH)
- `bd init` run in your project
- OpenSpec installed (`npm install -g @fission-ai/openspec`)

## Install

```bash
npm install -g spec-driven-with-beads
```

## Usage

In `openspec/config.yaml`:

```yaml
schema: spec-driven-with-beads
```

Then:
- `/opsx:propose "my feature"`
- `/opsx:apply` — driven by molecule step order
- `/opsx:consolidate` — lint, squash, remember, distill, archive

## Links

- [OpenSpec](https://github.com/Fission-AI/OpenSpec)
- [Beads](https://github.com/gastownhall/beads)
- [Beads Formula docs](https://gastownhall.github.io/beads/workflows/formulas)
- [Beads Molecule docs](https://gastownhall.github.io/beads/workflows/molecules)
- [Beads Aspect docs](https://gastownhall.github.io/beads/workflows/formulas#aspects-cross-cutting)
- [Community schema catalog](https://github.com/intent-driven-dev/openspec-schemas)
