## Purpose

Define the packaged `spec-driven-with-adr` OpenSpec schema and its ADR-enabled proposal-to-tasks workflow.
## Requirements
### Requirement: Repository SHALL package a spec-driven schema with ADR support
The repository SHALL provide a reusable `spec-driven-with-adr` OpenSpec schema package for teams that need proposal, specification, design, architecture decision record, and task-planning stages.

#### Scenario: Self-contained schema folder is available
- **WHEN** the `spec-driven-with-adr` schema is added
- **THEN** it is available as a self-contained folder at `openspec/schemas/spec-driven-with-adr/`
- **AND** the folder contains `schema.yaml`, a schema `README.md`, and all required templates.

#### Scenario: Imported schema is renamed
- **WHEN** the schema is imported from `/Users/harikrishnan/polarizer/projects/sdd/openspec/product-catalog/openspec/schemas/spec-driven-custom`
- **THEN** its `schema.yaml` uses `name: spec-driven-with-adr`
- **AND** every referenced template exists within the new schema folder.

### Requirement: Schema SHALL enforce proposal-to-tasks workflow with ADRs
The `spec-driven-with-adr` schema SHALL expose the artifacts `proposal`, `specs`, `design`, `adr`, and `tasks`, SHALL require those artifacts to be completed in dependency order before apply readiness, and SHALL use a change-local ADR review manifest as the completion marker for each change.

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

#### Scenario: ADR artifact uses a change-local completion marker
- **GIVEN** the affected schema is `spec-driven-with-adr`
- **WHEN** `openspec/schemas/spec-driven-with-adr/schema.yaml` defines the `adr` artifact
- **THEN** the artifact `generates` value MUST be `adr.md`
- **AND** the artifact completion check MUST be scoped to `openspec/changes/<change>/adr.md`
- **AND** existing files under the repository-level `adr/` folder MUST NOT satisfy completion for a new change.

#### Scenario: ADR artifact records durable ADR manifest entries
- **GIVEN** the affected schema is `spec-driven-with-adr`
- **WHEN** the `adr` artifact is created
- **THEN** the change-local `adr.md` artifact MUST act as a concise manifest, not a duplicate full ADR
- **AND** it MUST state that ADR review was completed for the change
- **AND** it MUST list existing in-force ADRs reviewed for the change
- **AND** if the change introduces any new durable architectural decision, a corresponding repository-level ADR file MUST be created under `<repo>/adr/`
- **AND** the change-local `adr.md` artifact MUST reference every repository-level ADR file created for the change
- **AND** it MUST NOT duplicate the full context, decision, or consequences content from any repository-level ADR file
- **AND** when no new repository-level ADR is needed, it MUST explicitly state that no major durable architectural decisions were introduced.

#### Scenario: ADR artifact preserves repository-level decision history
- **GIVEN** a project activates `schema: spec-driven-with-adr`
- **WHEN** the `adr` artifact is created
- **THEN** the schema instructions MUST direct ADR files to `<repo>/adr/NNNN-kebab-title.md`
- **AND** `<repo>/adr/` MUST mean a top-level folder beside `openspec/`, not a folder inside `openspec/`
- **AND** accepted ADR immutability and supersession rules MUST remain intact.

#### Scenario: Existing ADRs are context, not completion
- **GIVEN** a project uses the `spec-driven-with-adr` schema
- **AND** the repository-level `adr/` folder already contains one or more ADR markdown files from previous changes
- **WHEN** a new change has no `openspec/changes/<change>/adr.md`
- **THEN** the `adr` artifact MUST NOT be considered complete
- **AND** downstream task readiness MUST remain blocked until the change-local ADR review artifact exists.

### Requirement: Schema documentation SHALL explain usage, experimental status, and ADR persistence
The `spec-driven-with-adr` schema documentation SHALL explain intended use, unsuitable use cases, experimental status, OpenSpec PR provenance, activation, workflow order, change-local ADR review behavior, and repository-level ADR persistence behavior.

#### Scenario: Contributor evaluates schema fit
- **WHEN** a contributor reads `openspec/schemas/spec-driven-with-adr/README.md`
- **THEN** they can identify when to use `spec-driven-with-adr`
- **AND** they can identify unsuitable use cases.

#### Scenario: Contributor sees experimental provenance
- **WHEN** a contributor reads `openspec/schemas/spec-driven-with-adr/README.md`
- **THEN** it identifies the schema as experimental
- **AND** it references OpenSpec PR `https://github.com/Fission-AI/OpenSpec/pull/1020`.

#### Scenario: Contributor activates schema
- **WHEN** a contributor reads the schema README activation guidance
- **THEN** it tells them to set `schema: spec-driven-with-adr` in `openspec/config.yaml`.

#### Scenario: ADR persistence is documented
- **WHEN** a contributor reads the schema README
- **THEN** it explains that `openspec/changes/<change>/adr.md` is the per-change ADR review manifest used for OpenSpec artifact completion
- **AND** it explains that durable ADR files are generated under the target repository's top-level `adr/` folder rather than only inside the change folder.

### Requirement: Root README SHALL catalog the spec-driven-with-adr schema
The repository root `README.md` SHALL list `spec-driven-with-adr` as an available schema and point readers to its schema README.

#### Scenario: Human discovers the schema from the root catalog
- **WHEN** a human user opens the repository root `README.md`
- **THEN** they can find `spec-driven-with-adr` in the schema catalog
- **AND** they can find a reference to `openspec/schemas/spec-driven-with-adr/README.md`.

### Requirement: Schema changes SHALL be validated
Changes adding or modifying `openspec/schemas/spec-driven-with-adr/` SHALL pass OpenSpec schema validation before completion.

#### Scenario: Schema validation passes
- **WHEN** implementation changes files under `openspec/schemas/spec-driven-with-adr/`
- **THEN** `openspec schema validate spec-driven-with-adr` passes before the change is considered complete.

#### Scenario: ADR completion marker change is validated
- **WHEN** implementation changes the `adr` artifact completion marker
- **THEN** `openspec schema validate spec-driven-with-adr` passes before the change is considered complete.
