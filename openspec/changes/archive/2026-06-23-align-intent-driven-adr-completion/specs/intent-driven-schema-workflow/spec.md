## MODIFIED Requirements

### Requirement: Intent-driven schema SHALL persist durable decisions with per-change ADR review
The `intent-driven` schema SHALL require each change to complete ADR review through a change-local manifest at `openspec/changes/<change>/adr.md`, while preserving durable architectural decisions as immutable ADR files under the target repository's top-level `adr/` folder when a change introduces decisions worth carrying forward.

Affected schema:
- `intent-driven` (`openspec/schemas/intent-driven/`)

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

Affected schema:
- `intent-driven` (`openspec/schemas/intent-driven/`)

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

Affected schema:
- `intent-driven` (`openspec/schemas/intent-driven/`)

#### Scenario: Schema validation passes
- **WHEN** implementation changes files under `openspec/schemas/intent-driven/`
- **THEN** `openspec schema validate intent-driven` passes before the change is considered complete.

## REMOVED Requirements

### Requirement: Repository-level ADR glob as per-change completion marker
The schema no longer treats `../../../adr/*.md` as the `adr` artifact completion signal because repository-level ADRs persist across changes and can falsely satisfy new changes before their ADR review has been performed.

#### Removal Rationale
Repository-level ADR files remain the durable decision record, but pre-existing ADRs are historical inputs and cannot prove that a new change performed ADR review. New durable decisions MUST still be recorded under the repository-level `adr/` folder; per-change completion is tracked by a concise manifest at `openspec/changes/<change>/adr.md`.
