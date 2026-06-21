# spec-driven-with-beads

OpenSpec custom schema that uses [Beads](https://github.com/gastownhall/beads) molecules for task tracking, execution, and durable knowledge retention across sessions.

## Workflow

```
proposal → specs → design → tasks+beads → apply (via molecule) → consolidate
```

## What makes this different

Other schemas end at `archive` — move files, done. This one uses Beads' **formula + molecule** system: one `bd pour` command creates the entire dependency graph as a Beads molecule.

| Phase | What happens |
|-------|-------------|
| `tasks` | Writes `tasks.md` + **pours a molecule** via `bd pour spec-driven-change --var name=<change>` — creates epic + 5 steps with auto-dependency chain |
| `apply` | Works through molecule steps: `bd ready` → `bd update --claim` → code → `bd close`. Dependencies enforced by the molecule |
| `consolidate` | Closes molecule, `bd compact`, **`bd remember`** learnings, `openspec archive`. Knowledge persists via `bd prime` |

## Molecule structure

```
bd-xyz (epic: Spec-driven Change: my-feature)
├── bd-xyz.1  proposal          (human)
├── bd-xyz.2  specs             (needs: proposal)
├── bd-xyz.3  design            (needs: specs)
├── bd-xyz.4  implement         (needs: design)
└── bd-xyz.5  consolidate       (human, needs: implement)
```

No manual `bd create` × N or `bd dep add` × N — the formula defines the graph.

## Requirements

- [Beads](https://github.com/gastownhall/beads) installed (`bd` on PATH)
- `bd init` run in your project
- OpenSpec installed (`npm install -g @fission-ai/openspec`)

## Install

```bash
npm install -g spec-driven-with-beads
```

This copies the schema into OpenSpec's global schemas.

## Usage

In `openspec/config.yaml`:

```yaml
schema: spec-driven-with-beads
```

Then standard OpenSpec commands, but with Beads molecule awareness:
- `/opsx:propose "my feature"`
- `/opsx:apply` — driven by molecule step order
- `/opsx:consolidate` — remember, compact, archive
- `bd label list --label change:my-feature` — find past changes
- `bd list --label status:consolidated` — search consolidated work

## Links

- [OpenSpec](https://github.com/Fission-AI/OpenSpec)
- [Beads](https://github.com/gastownhall/beads)
- [Beads Formula docs](https://gastownhall.github.io/beads/workflows/formulas)
- [Beads Molecule docs](https://gastownhall.github.io/beads/workflows/molecules)
- [Community schema catalog](https://github.com/intent-driven-dev/openspec-schemas)
