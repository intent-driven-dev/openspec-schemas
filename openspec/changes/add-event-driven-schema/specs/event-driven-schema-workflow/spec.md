## ADDED User Stories

### User Story: Event-driven schema workflow
As a schema author, I want an `event-driven` OpenSpec schema with strict stage dependencies, so that teams can model EDA systems using an industry-standard discovery-to-spec flow before implementation.

#### Acceptance Criteria
- **Given** a project activates `schema: event-driven` in `openspec/config.yaml`
- **When** a new change is created
- **Then** artifact creation proceeds only in this order: `event-storming` -> `event-modeling` -> `specs` -> `design` -> `asyncapi` -> `tasks`
- **Given** the `event-driven` schema defines apply readiness
- **When** dependency status is evaluated
- **Then** `tasks` remains blocked until `asyncapi` is complete

### User Story: AsyncAPI-first implementation planning
As a delivery team, I want tasks to be generated only after a reviewed AsyncAPI 3 specification exists, so that implementation is grounded in a validated technical specification.

Affected schema:
- `event-driven` (`openspec/schemas/event-driven/`)

#### Acceptance Criteria
- **Given** `specs` and `design` are completed for a change using `event-driven`
- **When** `asyncapi.yaml` is authored
- **Then** `tasks` can be created only after AsyncAPI validation succeeds with `asyncapi-cli validate asyncapi.yaml`
- **Given** `asyncapi-cli` validation reports an error
- **When** artifact completion is checked
- **Then** the `asyncapi` stage is not done and `tasks` remains blocked

### User Story: Event-driven discovery guidance with Mermaid diagrams
As a product and engineering group, I want templates that guide Event Storming and Event Modeling using Mermaid diagrams, so that teams can collaboratively discover events and derive AsyncAPI content from shared visual models.

Affected schema:
- `event-driven` (`openspec/schemas/event-driven/`)

#### Acceptance Criteria
- **Given** a contributor creates `event-storming` and `event-modeling` artifacts
- **When** they follow schema templates
- **Then** the templates include Mermaid-based structure for events, commands, actors, automation arrows, and timeline swim lanes
- **Given** implementation is complete for schema files under `openspec/schemas/event-driven/`
- **When** post-apply verification is run
- **Then** `openspec schema review event-driven` is required before considering the change complete

## MODIFIED User Stories

## REMOVED User Stories
