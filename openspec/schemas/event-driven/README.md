# Event-Driven OpenSpec Schema

`event-driven` is for systems that communicate through events and require a
clear discovery-to-spec workflow before implementation planning.

- Good fit: event-centric domains, asynchronous integrations, pub/sub systems,
  and teams that need a validated AsyncAPI contract before coding.
- Not a good fit: tiny low-risk changes where `specs -> tasks` is enough and
  no event architecture decisions are required.

## Install (copy/paste)

Use the root `README.md` single-line install command with:
- `SCHEMA="event-driven"`

## Activate

Set this in `openspec/config.yaml`:

```yaml
schema: event-driven
```

## Stage Gates

Artifact order:
`event-storming -> event-modeling -> specs -> design -> asyncapi -> tasks`

Gate expectations:
- `event-modeling` must use outputs from `event-storming`.
- `specs` and `design` must be completed before `asyncapi`.
- `tasks` are planned only after reviewed `specs`, reviewed `design`, and a
  validated AsyncAPI document (`asyncapi-cli validate asyncapi.yaml`).

## Mermaid Color Legend

Use explicit `classDef` and `class` assignments in Mermaid templates so color
semantics stay stable across renderers.

Event-storming standard baseline:
- Domain Event: orange (`event`)
- Command: blue (`command`)
- Actor/User: yellow (`actor`)
- Policy/Automation: violet family (`policy`)
- Read Model/Projection: green (`readModel`)

Event-driven schema mapping notes:
- `Trigger` in `event-modeling` is treated as the actor/user lane and should use
  the `actor` color mapping.
- Prefer `Read Model` node labels in event-modeling artifacts and
  `Read Model/Projection` labels in event-storming artifacts; both map to
  `readModel` (green).
