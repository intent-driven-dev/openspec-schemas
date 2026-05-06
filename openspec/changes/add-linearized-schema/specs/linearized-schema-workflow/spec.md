## ADDED Requirements

### Requirement: Repository SHALL package the linearized schema
The repository SHALL provide a reusable `linearized` OpenSpec schema package for teams that coordinate work in Linear while keeping OpenSpec as the source of truth for project specifications.

#### Scenario: Linearized schema is forked from spec-driven
- **WHEN** the `linearized` schema is created
- **THEN** it is created by forking `spec-driven`
- **AND** the fork is updated only where needed for Linear setup, proposal binding, apply mirroring, archive guidance, templates, and documentation.

#### Scenario: Self-contained linearized schema folder is available
- **WHEN** the `linearized` schema is added
- **THEN** it is available as a self-contained folder at `openspec/schemas/linearized/`
- **AND** the folder contains `schema.yaml`, a schema `README.md`, and all templates referenced by the schema.

#### Scenario: Linearized schema can be activated
- **WHEN** a contributor reads the `linearized` schema README
- **THEN** it tells them to set `schema: linearized` in `openspec/config.yaml`
- **AND** it explains when the schema is suitable and unsuitable.

### Requirement: Linearized schema SHALL guide first-time Linear setup
The `linearized` schema SHALL instruct agents to load `openspec/linear.yaml` when present and to perform first-time Linear setup when the file is missing.

#### Scenario: First-time setup creates project-local Linear configuration
- **GIVEN** a project activates `schema: linearized`
- **AND** `openspec/linear.yaml` does not exist
- **WHEN** a contributor starts a new change
- **THEN** the schema instructions require the agent to verify Linear MCP connectivity when possible
- **AND** ask for the Linear team and project
- **AND** optionally ask for a Linear issue label filter
- **AND** write the selected setup to `openspec/linear.yaml`.

#### Scenario: Existing setup is loaded silently
- **GIVEN** `openspec/linear.yaml` exists
- **WHEN** a contributor starts a subsequent `linearized` change
- **THEN** the schema instructions require the agent to load the configured Linear team, project, and optional label filter without repeating first-time setup prompts.

### Requirement: Linearized proposal flow SHALL bind an OpenSpec change to a Linear story
The `linearized` proposal flow SHALL guide agents to select a Linear Backlog issue for the configured project context and record the selected story in proposal frontmatter.

#### Scenario: Proposal records Linear story metadata
- **GIVEN** Linear MCP is available
- **AND** a contributor starts a new `linearized` change
- **WHEN** the proposal artifact is created
- **THEN** the schema instructions require the agent to select a Linear Backlog issue for the configured project context
- **AND** transition the selected issue to Todo when possible
- **AND** add a Linear comment in at most two sentences summarizing that OpenSpec proposal discovery started and the story was linked
- **AND** record `linear_story_id` in `proposal.md` frontmatter.

#### Scenario: Proposal discovery starts from Linear story content
- **GIVEN** Linear MCP is available
- **AND** the agent selects a configured-project Linear story
- **WHEN** the proposal artifact is created
- **THEN** the schema instructions require the agent to read available story content as initial OpenSpec proposal input
- **AND** ask the contributor clarifying questions about business cases, scope, architecture, tech stack, constraints, integrations, risks, acceptance criteria, and affected capabilities
- **AND** avoid treating the Linear story content as an already-complete OpenSpec proposal.

#### Scenario: Proposal continues when Linear is unavailable after setup
- **GIVEN** `openspec/linear.yaml` exists
- **AND** Linear MCP is unavailable
- **WHEN** the proposal artifact is created
- **THEN** the schema instructions allow OpenSpec proposal creation to continue locally
- **AND** require Linear updates to be skipped silently.

### Requirement: Linearized schema SHALL define apply-time Linear mirroring
The `linearized` schema SHALL use `apply.instruction` with `apply.tracks: tasks.md` to guide best-effort Linear issue updates while implementation tasks are applied.

#### Scenario: Apply updates the Linear story when possible
- **GIVEN** a `linearized` change has `proposal.md` frontmatter with `linear_story_id`
- **AND** Linear MCP is available
- **WHEN** apply begins
- **THEN** the schema apply instructions require the agent to sync useful proposal content to the Linear story when possible
- **AND** transition Todo to In Progress when possible
- **AND** add a Linear comment in at most two sentences summarizing that implementation began from the OpenSpec change and tracked tasks are being applied
- **AND** work through tracked checkboxes in `tasks.md`.

#### Scenario: Apply remains local when Linear updates fail
- **GIVEN** a `linearized` change is ready to apply
- **AND** Linear MCP is unavailable or a Linear update fails
- **WHEN** apply runs
- **THEN** the schema apply instructions require implementation to continue from `tasks.md`
- **AND** require failed Linear updates to remain non-blocking.

### Requirement: Linearized tasks SHALL include verifiable archive-readiness guidance
The `linearized` task guidance SHALL require a final task group for implementation verification and archive readiness without making post-archive Linear resource sync part of `tasks.md`.

#### Scenario: Tasks avoid post-archive Linear resource sync checkboxes
- **WHEN** `tasks.md` is created for a `linearized` change
- **THEN** it includes implementation verification and archive-readiness checkboxes
- **AND** does not include post-archive Linear Project Document sync checkboxes
- **AND** does not include a checkbox to transition the Linear story to Done.

#### Scenario: Tasks include schema validation verification
- **WHEN** `tasks.md` is created for implementation that changes `openspec/schemas/linearized/`
- **THEN** it requires `openspec schema validate linearized` before the change is considered complete.

### Requirement: Linearized proposal SHALL preserve archive guidance for Linear Project Document mirrors
The `linearized` proposal template and schema documentation SHALL preserve optional archive-time guidance for mirroring canonical OpenSpec specs to Linear Project Documents.

#### Scenario: Proposal contains preserved archive guidance
- **WHEN** `proposal.md` is created for a `linearized` change
- **THEN** it contains schema-provided Linear archive guidance that agents preserve unless the schema changes
- **AND** the guidance states OpenSpec canonical specs are the source of truth
- **AND** the guidance states Linear Project Documents are mirrors.

#### Scenario: Archive sync mirrors canonical specs after OpenSpec archive
- **GIVEN** OpenSpec archive has merged changed delta specs into canonical files under `openspec/specs/`
- **AND** Linear MCP is available
- **WHEN** post-archive Linear sync runs
- **THEN** the schema guidance requires the agent to mirror changed canonical spec files into project-scoped Linear documents
- **AND** treat the Linear documents as mirrors rather than the source of truth.

#### Scenario: Existing Linear document is updated before creating a new one
- **GIVEN** a canonical spec is eligible for Linear Project Document sync
- **WHEN** post-archive sync runs
- **THEN** the schema guidance requires the agent to update a stored document ID or slug from `openspec/linear.yaml` when present
- **AND** otherwise look for an existing project document with the expected deterministic title
- **AND** create a new project-scoped document only when no existing document is found.

#### Scenario: Archive sync skips unsupported resource types
- **WHEN** post-archive Linear sync runs
- **THEN** the schema guidance targets Linear Project Documents only
- **AND** does not require creating or updating generic non-document Linear project resources.

#### Scenario: Linear story is completed only after archive
- **GIVEN** a `linearized` change has a bound Linear story
- **AND** OpenSpec archive succeeds for the associated change
- **WHEN** archive-time Linear updates run
- **THEN** the schema guidance allows the agent to transition the Linear story to Done when possible
- **AND** add a Linear comment in at most two sentences summarizing that archive completed and canonical specs or mirrors were handled
- **AND** forbids transitioning the story to Done before OpenSpec archive succeeds.

### Requirement: Linearized schema SHALL validate cleanly
Changes adding or modifying `openspec/schemas/linearized/` SHALL pass OpenSpec schema validation before completion.

#### Scenario: Linearized schema validation passes
- **WHEN** implementation changes files under `openspec/schemas/linearized/`
- **THEN** `openspec schema validate linearized` passes before the change is considered complete.
