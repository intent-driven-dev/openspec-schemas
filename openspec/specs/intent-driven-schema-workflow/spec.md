# intent-driven-schema-workflow Specification

## Purpose
TBD - created by archiving change add-intent-driven-schema. Update Purpose after archive.
## Requirements
### Requirement: Repository SHALL package the intent-driven schema
The repository SHALL provide a reusable `intent-driven` OpenSpec schema package for teams that want proposal-led intent capture, Gherkin-style behaviour specs inside OpenSpec Markdown wrappers, technical design, durable architecture decision records, and implementation tasks.

#### Scenario: Self-contained intent-driven schema folder is available
- **WHEN** the `intent-driven` schema is added
- **THEN** it is available as a self-contained folder at `openspec/schemas/intent-driven/`
- **AND** the folder contains `schema.yaml`, a schema `README.md`, and all templates referenced by the schema.

#### Scenario: Intent-driven schema can be activated
- **WHEN** a contributor reads the `intent-driven` schema README
- **THEN** it tells them to set `schema: intent-driven` in `openspec/config.yaml`
- **AND** it explains when the schema is suitable and unsuitable.

### Requirement: Intent-driven schema SHALL enforce proposal-to-tasks workflow with ADRs
The `intent-driven` schema SHALL expose the artifacts `proposal`, `specs`, `design`, `adr`, and `tasks`, SHALL generate behaviour specs as OpenSpec Markdown delta files, and SHALL require those artifacts to be completed in dependency order before apply readiness.

#### Scenario: Workflow proceeds in dependency order
- **GIVEN** a project activates `schema: intent-driven`
- **WHEN** a new OpenSpec change is created
- **THEN** artifact creation proceeds in this order: `proposal -> specs -> design -> adr -> tasks`.

#### Scenario: Specs generate OpenSpec mergeable Markdown by capability
- **GIVEN** a proposal lists new or modified capabilities
- **WHEN** the `specs` artifact is created
- **THEN** each listed capability is specified at `specs/<capability>/spec.md`
- **AND** each spec file uses OpenSpec delta headers so archive can merge it into `openspec/specs/<capability>/spec.md`.

#### Scenario: Tasks are required for apply readiness
- **GIVEN** the schema defines apply readiness
- **WHEN** `tasks` is incomplete
- **THEN** the change is not ready to apply.

#### Scenario: Tasks are blocked by predecessor artifacts
- **GIVEN** the schema defines task dependencies
- **WHEN** `proposal`, `specs`, `design`, or `adr` is incomplete
- **THEN** `tasks` remains blocked until all required predecessor artifacts are complete.

### Requirement: Intent-driven schema SHALL guide Gherkin-style authoring inside Markdown wrappers
The `intent-driven` schema SHALL make OpenSpec Markdown syntax the merge wrapper and SHALL guide contributors to write the requirement and scenario content in Gherkin style.

#### Scenario: OpenSpec wrapper remains explicit
- **WHEN** a contributor authors a behaviour spec
- **THEN** the schema guidance requires OpenSpec delta headers such as `## ADDED Requirements` and `## MODIFIED Requirements`
- **AND** requires requirement headers to use `### Requirement:`
- **AND** requires scenarios to use `#### Scenario:` so default OpenSpec validation and archive can process the spec.

#### Scenario: Scenario content uses Gherkin-style steps
- **WHEN** a contributor authors a behaviour spec
- **THEN** the schema guidance treats each requirement as the feature or business rule being specified
- **AND** requires scenarios to use `GIVEN`, `WHEN`, and `THEN` steps inside the Markdown scenario block
- **AND** allows `AND` and `BUT` for follow-on steps
- **AND** directs `Then` steps to express observable outcomes rather than implementation details.

### Requirement: Intent-driven schema SHALL persist durable decisions with per-change ADR review
The `intent-driven` schema SHALL require each change to complete ADR review through a change-local manifest at `openspec/changes/<change>/adr.md`, while preserving durable architectural decisions as immutable ADR files under the target repository's top-level `adr/` folder when a change introduces decisions worth carrying forward.

#### Scenario: ADR artifact uses a change-local completion marker
- **GIVEN** the affected schema is `intent-driven`
- **WHEN** `openspec/schemas/intent-driven/schema.yaml` defines the `adr` artifact
- **THEN** the artifact `generates` value MUST be `adr.md`
- **AND** the artifact completion check MUST be scoped to `openspec/changes/<change>/adr.md`
- **AND** existing files under the repository-level `adr/` folder MUST NOT satisfy completion for a new change.

#### Scenario: ADR artifact records durable ADR manifest entries
- **GIVEN** the affected schema is `intent-driven`
- **WHEN** the `adr` artifact is created
- **THEN** the change-local `adr.md` artifact MUST act as a concise manifest, not a duplicate full ADR
- **AND** it MUST state that ADR review was completed for the change
- **AND** it MUST list existing in-force ADRs reviewed for the change
- **AND** if the change introduces any new durable architectural decision, a corresponding repository-level ADR file MUST be created under `<repo>/adr/`
- **AND** the change-local `adr.md` artifact MUST reference every repository-level ADR file created for the change
- **AND** it MUST NOT duplicate the full context, decision, or consequences content from any repository-level ADR file
- **AND** when no new repository-level ADR is needed, it MUST explicitly state that no major durable architectural decisions were introduced.

#### Scenario: ADR artifact preserves repository-level decision history
- **GIVEN** a project activates `schema: intent-driven`
- **WHEN** the `adr` artifact identifies a durable architectural decision that is not already captured by an in-force ADR
- **THEN** the schema instructions MUST direct ADR files to `<repo>/adr/NNNN-kebab-title.md`
- **AND** `<repo>/adr/` MUST mean a top-level folder beside `openspec/`, not a folder inside `openspec/`
- **AND** accepted ADR immutability and supersession rules MUST remain intact.

#### Scenario: Existing ADRs are context, not completion
- **GIVEN** a project uses the `intent-driven` schema
- **AND** the repository-level `adr/` folder already contains one or more ADR markdown files from previous changes
- **WHEN** a new change has no `openspec/changes/<change>/adr.md`
- **THEN** the `adr` artifact MUST NOT be considered complete
- **AND** downstream task readiness MUST remain blocked until the change-local ADR review artifact exists.

#### Scenario: Design reads currently in-force ADRs
- **GIVEN** a project has existing ADR files under `<repo>/adr/`
- **WHEN** the `design` artifact is created
- **THEN** the schema instructions require the contributor to identify currently in-force ADRs by walking supersession links
- **AND** only currently in-force ADRs constrain the design.

### Requirement: Intent-driven schema documentation SHALL explain ADR review and persistence
The `intent-driven` schema documentation SHALL distinguish the per-change ADR review artifact from durable repository-level ADR files.

#### Scenario: ADR review manifest is documented
- **WHEN** a contributor reads `openspec/schemas/intent-driven/README.md`
- **THEN** it explains that `openspec/changes/<change>/adr.md` is the per-change ADR review manifest used for OpenSpec artifact completion
- **AND** it explains that existing repository-level ADR files are context for new changes, not completion evidence for those changes.

#### Scenario: ADR persistence remains documented
- **WHEN** a contributor reads `openspec/schemas/intent-driven/README.md`
- **THEN** it explains that durable ADR files are generated under the target repository's top-level `adr/` folder
- **AND** it explains that repository-level ADR files are created only when the change introduces a major durable architectural decision.

### Requirement: Intent-driven schema SHALL validate cleanly
Changes adding or modifying `openspec/schemas/intent-driven/` SHALL pass OpenSpec schema validation before completion.

#### Scenario: Schema validation passes
- **WHEN** implementation changes files under `openspec/schemas/intent-driven/`
- **THEN** `openspec schema validate intent-driven` passes before the change is considered complete.
