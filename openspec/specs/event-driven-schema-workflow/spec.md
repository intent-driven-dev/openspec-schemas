## Purpose

Define the `event-driven` schema workflow, gating rules, and template guidance for event-centric system development.

## Requirements

### Requirement: Event-driven schema SHALL enforce workflow order and stage dependencies
The `event-driven` schema SHALL enforce artifact creation order `event-storming -> event-modeling -> specs -> design -> asyncapi -> tasks` and SHALL keep `tasks` blocked until `asyncapi` is complete.

#### Scenario: Workflow proceeds in strict event-driven order
- **GIVEN** a project activates `schema: event-driven` in `openspec/config.yaml`
- **WHEN** a new change is created
- **THEN** artifact creation proceeds only in this order: `event-storming` -> `event-modeling` -> `specs` -> `design` -> `asyncapi` -> `tasks`

#### Scenario: Tasks remain blocked until asyncapi is done
- **GIVEN** the `event-driven` schema defines apply readiness
- **WHEN** dependency status is evaluated
- **THEN** `tasks` remains blocked until `asyncapi` is complete

### Requirement: Event-driven schema SHALL require validated AsyncAPI before tasks
For changes using `event-driven`, `tasks` SHALL be creatable only after `specs` and `design` are complete and AsyncAPI validation succeeds with `asyncapi-cli validate asyncapi.yaml`.

#### Scenario: Tasks allowed only after AsyncAPI validation succeeds
- **GIVEN** `specs` and `design` are completed for a change using `event-driven`
- **WHEN** `asyncapi.yaml` is authored
- **THEN** `tasks` can be created only after AsyncAPI validation succeeds with `asyncapi-cli validate asyncapi.yaml`

#### Scenario: AsyncAPI validation failure blocks tasks
- **GIVEN** `asyncapi-cli` validation reports an error
- **WHEN** artifact completion is checked
- **THEN** the `asyncapi` stage is not done and `tasks` remains blocked

### Requirement: Event-driven templates SHALL guide discovery and post-apply verification
The `event-driven` schema templates SHALL include Mermaid-based Event Storming and Event Modeling structure, and post-apply verification for schema changes under `openspec/schemas/event-driven/` SHALL require `openspec schema review event-driven` before change completion.

#### Scenario: Contributors use Mermaid guidance in discovery artifacts
- **GIVEN** a contributor creates `event-storming` and `event-modeling` artifacts
- **WHEN** they follow schema templates
- **THEN** the templates include Mermaid-based structure for events, commands, actors, automation arrows, and timeline swim lanes

#### Scenario: Post-apply verification is required for event-driven schema changes
- **GIVEN** implementation is complete for schema files under `openspec/schemas/event-driven/`
- **WHEN** post-apply verification is run
- **THEN** `openspec schema review event-driven` is required before considering the change complete
