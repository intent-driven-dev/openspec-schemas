# behaviour-driven-schema-workflow Specification

## Purpose
TBD - created by archiving change add-behaviour-driven-schema. Update Purpose after archive.
## Requirements
### Requirement: Repository SHALL package the behaviour-driven schema
The repository SHALL provide a reusable `behaviour-driven` OpenSpec schema package for teams that want proposal-led changes with observable behaviour captured as Gherkin-style scenarios inside OpenSpec-mergeable Markdown specs.

#### Scenario: Self-contained behaviour-driven schema folder is available
- **WHEN** the `behaviour-driven` schema is added
- **THEN** it is available as a self-contained folder at `openspec/schemas/behaviour-driven/`
- **AND** the folder contains `schema.yaml`, a schema `README.md`, and all templates referenced by the schema.

#### Scenario: Behaviour-driven schema can be activated
- **WHEN** a contributor reads the `behaviour-driven` schema README
- **THEN** it tells them to set `schema: behaviour-driven` in `openspec/config.yaml`
- **AND** it explains when the schema is suitable and unsuitable.

### Requirement: Behaviour-driven schema SHALL enforce proposal-to-tasks workflow with Gherkin-style specs
The `behaviour-driven` schema SHALL expose the artifacts `proposal`, `specs`, `design`, and `tasks`, SHALL generate behaviour specs as OpenSpec Markdown delta files, and SHALL require those artifacts to be completed in dependency order before apply readiness.

#### Scenario: Workflow proceeds in dependency order
- **GIVEN** a project activates `schema: behaviour-driven`
- **WHEN** a new OpenSpec change is created
- **THEN** artifact creation proceeds in this order: `proposal -> specs -> design -> tasks`.

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
- **WHEN** `proposal`, `specs`, or `design` is incomplete
- **THEN** `tasks` remains blocked until all required predecessor artifacts are complete.

### Requirement: Behaviour-driven schema SHALL guide Gherkin-style authoring inside Markdown wrappers
The `behaviour-driven` schema SHALL make OpenSpec Markdown syntax the merge wrapper and SHALL guide contributors to write the requirement and scenario content in Gherkin style.

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

#### Scenario: Modified behaviours copy existing Markdown requirement content before editing
- **GIVEN** a change modifies an existing behaviour capability
- **WHEN** the contributor creates the change spec file
- **THEN** the schema guidance tells them to copy the full existing requirement block from `openspec/specs/<capability>/spec.md`
- **AND** edit the copied content so it represents the full desired behaviour after the change.

### Requirement: Behaviour-driven schema SHALL validate cleanly
Changes adding or modifying `openspec/schemas/behaviour-driven/` SHALL pass OpenSpec schema validation before completion.

#### Scenario: Schema validation passes
- **WHEN** implementation changes files under `openspec/schemas/behaviour-driven/`
- **THEN** `openspec schema validate behaviour-driven` passes before the change is considered complete.

