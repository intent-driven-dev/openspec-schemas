## 1. Create the event-driven schema package

- [x] 1.1 Create `openspec/schemas/event-driven/` with `schema.yaml`, `README.md`, and `templates/` directories.
- [x] 1.2 Define artifact sequence in `schema.yaml`: `event-storming` -> `event-modeling` -> `specs` -> `design` -> `asyncapi` -> `tasks`.
- [x] 1.3 Configure dependencies so each artifact depends on the prior stage and `tasks` requires `asyncapi`.

## 2. Author event-driven discovery templates

- [x] 2.1 Add `templates/event-storming.md` with guidance for events, commands, actors, aggregates, automations, and hotspot capture.
- [x] 2.2 Add `templates/event-modeling.md` with four swim lanes (Trigger -> Command -> Event -> Read Model) and Mermaid diagram scaffolding.
- [x] 2.3 Ensure template language keeps discovery and modeling outputs as inputs for later `specs`, `design`, and `asyncapi`.

## 3. Author specification and design templates

- [x] 3.1 Add `templates/specs/spec.md` using user-story and Given/When/Then acceptance criteria format.
- [x] 3.2 Add `templates/design.md` to capture stack decisions (broker, subject naming, payload/schema format) and security decisions before AsyncAPI authoring.
- [x] 3.3 Add `templates/asyncapi.yaml` guidance so AsyncAPI is authored as a technical specification derived from prior artifacts.

## 4. Enforce AsyncAPI validation gate and task planning

- [x] 4.1 Define `asyncapi` artifact completion guidance requiring `asyncapi-cli validate asyncapi.yaml`.
- [x] 4.2 Add `templates/tasks.md` that only plans implementation after reviewed `specs`, reviewed `design`, and validated `asyncapi`.
- [x] 4.3 Confirm `apply.requires` remains `tasks` while preserving the upstream `asyncapi` gate.

## 5. Verify and document schema usage

- [x] 5.1 Add `openspec/schemas/event-driven/README.md` with good-fit/not-fit, activation steps, and stage gate expectations.
- [x] 5.2 Update root documentation/catalog entries to include `event-driven` schema usage.
- [x] 5.3 Run `openspec schema review event-driven` and fix any issues before marking the change complete. (Used `openspec schema validate event-driven` because this CLI version has no `schema review` command.)
