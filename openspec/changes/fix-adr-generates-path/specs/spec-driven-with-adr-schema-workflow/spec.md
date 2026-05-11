## MODIFIED Requirements

### Requirement: Schema SHALL enforce proposal-to-tasks workflow with ADRs
The `spec-driven-with-adr` schema SHALL expose the artifacts `proposal`, `specs`, `design`, `adr`, and `tasks`, SHALL require those artifacts to be completed in dependency order before apply readiness, and SHALL direct ADR output through plain instructions rather than artifact folder routing metadata.

#### Scenario: Workflow proceeds in dependency order
- **GIVEN** a project activates `schema: spec-driven-with-adr`
- **WHEN** a new OpenSpec change is created
- **THEN** artifact creation proceeds in this order: `proposal -> specs -> design -> adr -> tasks`.

#### Scenario: Tasks are required for apply readiness
- **GIVEN** the schema defines apply readiness
- **WHEN** `tasks` is incomplete
- **THEN** the change is not ready to apply.

#### Scenario: Tasks are blocked by predecessor artifacts
- **GIVEN** the schema defines task dependencies
- **WHEN** `proposal`, `specs`, `design`, or `adr` is incomplete
- **THEN** `tasks` remains blocked until all required predecessor artifacts are complete.

#### Scenario: ADR artifact uses plain path instruction
- **GIVEN** the affected schema is `spec-driven-with-adr`
- **WHEN** `openspec/schemas/spec-driven-with-adr/schema.yaml` defines the `adr` artifact
- **THEN** the artifact definition MUST NOT include the `folder` parameter
- **AND** the artifact instruction MUST strongly direct agents to create ADR files under the target repository's top-level `adr/` folder outside `openspec/`
- **AND** the artifact instruction MUST state that ADR files are not written under `openspec/changes/<change>/`.

#### Scenario: ADR artifact completion checks repository-level output
- **GIVEN** the affected schema is `spec-driven-with-adr`
- **WHEN** `openspec/schemas/spec-driven-with-adr/schema.yaml` defines the `adr` artifact
- **THEN** the artifact `generates` value MUST resolve to `<repo>/adr/*.md` from the change directory
- **AND** the value MUST match the known-good relative path pattern `../../../adr/*.md`.

#### Scenario: Change-local proposal does not complete ADR artifact
- **GIVEN** a project uses the `spec-driven-with-adr` schema
- **WHEN** a change contains `proposal.md` but no generated ADR file under the repository-level `adr/` folder
- **THEN** the `adr` artifact MUST NOT be considered complete
- **AND** downstream task readiness MUST remain blocked until the ADR artifact completion check observes the intended ADR output location.

#### Scenario: ADR artifact preserves repository-level decision history
- **GIVEN** a project activates `schema: spec-driven-with-adr`
- **WHEN** the `adr` artifact is created
- **THEN** the schema instructions MUST direct ADR files to `<repo>/adr/NNNN-kebab-title.md`
- **AND** `<repo>/adr/` MUST mean a top-level folder beside `openspec/`, not a folder inside `openspec/`
- **AND** accepted ADR immutability and supersession rules MUST remain intact.

### Requirement: Schema changes SHALL be validated
Changes adding or modifying `openspec/schemas/spec-driven-with-adr/` SHALL pass OpenSpec schema validation before completion.

#### Scenario: Schema validation passes
- **WHEN** implementation changes files under `openspec/schemas/spec-driven-with-adr/`
- **THEN** `openspec schema validate spec-driven-with-adr` passes before the change is considered complete.

#### Scenario: Schema quality gate passes
- **WHEN** implementation changes files under `openspec/schemas/spec-driven-with-adr/`
- **THEN** `openspec schema validate spec-driven-with-adr` passes before the change is considered complete.

#### Scenario: ADR folder parameter removal is validated
- **WHEN** implementation removes artifact folder routing metadata from the `adr` artifact
- **THEN** `openspec schema validate spec-driven-with-adr` passes before the change is considered complete.
