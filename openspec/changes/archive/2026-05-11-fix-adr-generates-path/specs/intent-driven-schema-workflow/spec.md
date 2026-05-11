## MODIFIED Requirements

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
