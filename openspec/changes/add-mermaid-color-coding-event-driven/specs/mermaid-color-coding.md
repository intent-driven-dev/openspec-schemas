## ADDED User Stories

### User Story: Color-coded Mermaid templates for event-driven schema
As a schema maintainer, I want Mermaid diagrams in the `event-driven` schema templates to use event-storming-standard color semantics, so that diagram semantics remain visually consistent across rendering environments.

#### Acceptance Criteria
- **Given** the `event-driven` schema templates contain Mermaid flow and sequence diagrams
- **When** a maintainer scaffolds or updates artifacts that include those diagrams
- **Then** the generated Mermaid blocks include explicit styling directives (for example `classDef` and class assignments) that map key concepts to stable colors.
- **And** the styling follows event-storming-standard semantics:
  - Domain Event: orange
  - Command: blue
  - Actor/User: yellow
  - Policy/Automation: pink or violet family
  - Read Model/Projection: green

### User Story: Documented color legend for event-driven Mermaid diagrams
As a contributor, I want a documented color legend for Mermaid nodes used by the `event-driven` schema, so that I can apply and review diagram styles consistently.

#### Acceptance Criteria
- **Given** the `event-driven` schema is used to author event-storming and event-modeling artifacts
- **When** a contributor reads template guidance
- **Then** they can find a clear mapping between diagram concepts (such as trigger, command, event, read model, actor, and automation) and their intended colors.
- **And** the guide calls out the event-storming-standard baseline and any schema-specific deviations.

### User Story: Post-apply schema review verification for event-driven updates
As a reviewer, I want schema-level verification after implementing Mermaid color-coding changes in `event-driven`, so that styling updates are validated before considering the change complete.

#### Acceptance Criteria
- **Given** implementation modifies files under `openspec/schemas/event-driven/`
- **When** the implementation tasks are completed
- **Then** the workflow includes running `openspec schema review event-driven` and treating a successful review as part of completion criteria.

## MODIFIED User Stories

None.

## REMOVED User Stories

None.
