## MODIFIED Requirements

### Requirement: Schema SHALL enforce proposal-to-tasks workflow with ADRs
The `spec-driven-with-adr` schema SHALL expose the artifacts `proposal`, `specs`, `design`, `adr`, and `tasks`, SHALL require those artifacts to be completed in dependency order before apply readiness, and SHALL use a change-local ADR review manifest as the completion marker for each change.

Affected schema:
- `spec-driven-with-adr` (`openspec/schemas/spec-driven-with-adr/`)

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
- **WHEN** the `adr` artifact identifies a durable architectural decision that is not already captured by an in-force ADR
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

Affected schema:
- `spec-driven-with-adr` (`openspec/schemas/spec-driven-with-adr/`)

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

### Requirement: Schema changes SHALL be validated
Changes adding or modifying `openspec/schemas/spec-driven-with-adr/` SHALL pass OpenSpec schema validation before completion.

Affected schema:
- `spec-driven-with-adr` (`openspec/schemas/spec-driven-with-adr/`)

#### Scenario: Schema validation passes
- **WHEN** implementation changes files under `openspec/schemas/spec-driven-with-adr/`
- **THEN** `openspec schema validate spec-driven-with-adr` passes before the change is considered complete.

#### Scenario: ADR completion marker change is validated
- **WHEN** implementation changes the `adr` artifact completion marker
- **THEN** `openspec schema validate spec-driven-with-adr` passes before the change is considered complete.

## REMOVED Requirements

### Requirement: Repository-level ADR glob as per-change completion marker
The schema no longer treats `../../../adr/*.md` as the `adr` artifact completion signal because repository-level ADRs persist across changes and can falsely satisfy new changes before their ADR review has been performed.

#### Removal Rationale
Repository-level ADR files remain the durable decision record, but pre-existing ADRs are historical inputs and cannot prove that a new change performed ADR review. New durable decisions MUST still be recorded under the repository-level `adr/` folder; per-change completion is tracked by a concise manifest at `openspec/changes/<change>/adr.md`.
