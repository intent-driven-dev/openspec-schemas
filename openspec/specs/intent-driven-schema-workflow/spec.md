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

### Requirement: Intent-driven schema SHALL persist durable decisions as top-level ADRs
The `intent-driven` schema SHALL require the ADR artifact to distill durable architectural decisions from design into immutable ADR files under the target repository's top-level `adr/` folder.

#### Scenario: ADRs are written outside OpenSpec changes
- **GIVEN** a project activates `schema: intent-driven`
- **WHEN** the `adr` artifact is created
- **THEN** the schema instructions MUST direct ADR files to `<repo>/adr/NNNN-kebab-title.md`
- **AND** `<repo>/adr/` MUST mean a top-level folder beside `openspec/`
- **AND** ADR files MUST NOT be written under `openspec/changes/<change>/`.

#### Scenario: ADR artifact completion checks repository-level output
- **GIVEN** the affected schema is `intent-driven`
- **WHEN** `openspec/schemas/intent-driven/schema.yaml` defines the `adr` artifact
- **THEN** the artifact `generates` value MUST resolve to `<repo>/adr/*.md` from the change directory
- **AND** the value MUST match the known-good relative path pattern `../../../adr/*.md`.

#### Scenario: Change-local proposal does not complete ADR artifact
- **GIVEN** a project uses the `intent-driven` schema
- **WHEN** a change contains `proposal.md` but no generated ADR file under the repository-level `adr/` folder
- **THEN** the `adr` artifact MUST NOT be considered complete
- **AND** downstream task readiness MUST remain blocked until the ADR artifact completion check observes the intended ADR output location.

#### Scenario: Existing ADRs remain immutable
- **GIVEN** a current architectural decision needs to be changed
- **WHEN** the `adr` artifact records the new decision
- **THEN** the schema instructions MUST require a new ADR file
- **AND** the new ADR MAY supersede a prior ADR using status text and a `Supersedes:` field
- **AND** the prior ADR file MUST remain unchanged.

#### Scenario: Design reads currently in-force ADRs
- **GIVEN** a project has existing ADR files under `<repo>/adr/`
- **WHEN** the `design` artifact is created
- **THEN** the schema instructions require the contributor to identify currently in-force ADRs by walking supersession links
- **AND** only currently in-force ADRs constrain the design.

### Requirement: Intent-driven schema SHALL validate cleanly
Changes adding or modifying `openspec/schemas/intent-driven/` SHALL pass OpenSpec schema validation before completion.

#### Scenario: Schema validation passes
- **WHEN** implementation changes files under `openspec/schemas/intent-driven/`
- **THEN** `openspec schema validate intent-driven` passes before the change is considered complete.
