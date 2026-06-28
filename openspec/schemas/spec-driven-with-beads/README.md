# spec-driven-with-beads

OpenSpec workflow that uses Beads (`bd`) for task tracking and execution instead of flat task lists.

## Workflow

```
proposal → specs → design → tasks+beads → apply (via Beads) → archive
```

| Phase | Artifact | Beads interaction |
|-------|----------|-------------------|
| `propose` | `proposal.md` | None |
| `specs` | `specs/**/*.md` | None |
| `design` | `design.md` | None |
| `tasks` | `tasks.md` + seeds Beads | `bd create` for each task, `bd dep add` for dependencies |
| `apply` | (tracks via Beads) | `bd ready` → `bd update --claim` → code → `bd close` |
| `archive` | moves to archive | `bd compact` on closed issues |

## Why Beads?

- **Context efficiency** — agent queries `bd ready` for next task instead of re-reading tasks.md
- **Dependency tracking** — `bd dep add` makes blockers explicit
- **Persistence** — survive across sessions, no context loss
- **Progress visibility** — `bd stats`, `bd dep tree` show real status

## Requirements

- [Beads](https://github.com/gastownhall/beads) installed (`bd` on PATH)
- `bd init` run in the project
- Beads MCP server optional but recommended for richer integration

## Activation

In `openspec/config.yaml`:

```yaml
schema: spec-driven-with-beads
```
