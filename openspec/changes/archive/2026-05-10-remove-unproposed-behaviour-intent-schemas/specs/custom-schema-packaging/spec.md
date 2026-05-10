## MODIFIED Requirements

### Requirement: Repository SHALL package each custom schema in a self-contained folder
The repository SHALL organize custom OpenSpec schemas as one folder per schema, where each folder contains all files required for a user or coding agent to install that schema into a target project, and SHALL only retain schema folders that are backed by an OpenSpec change history and canonical spec coverage.

#### Scenario: Installable schema folder exists
- **WHEN** a user selects a schema from this repository
- **THEN** that schema is available as a single folder that can be copied into `openspec/schemas/<schema-name>/` in the target project

#### Scenario: Unproposed schema packages are removed before rebuild
- **GIVEN** a schema folder exists under `openspec/schemas/`
- **AND** the schema lacks proposal-backed canonical spec coverage under `openspec/specs/`
- **WHEN** maintainers decide to rebuild that schema through OpenSpec proposals
- **THEN** the unproposed schema folder is removed before the proposal-backed replacement is added
- **AND** repository catalog documentation no longer advertises that schema until the replacement is archived.

### Requirement: Repository root SHALL provide catalog and install guidance for humans and agents
The repository root SHALL include a `README.md` that explains the purpose of this schema collection, starts the main install section with an agent-oriented prompt that points to the raw root `README.md`, gives a self-install fallback for human readers, includes a dedicated agent-oriented install flow that removes ambiguity about prerequisites and copying the full schema folder, and lists only currently packaged schemas with canonical spec coverage.

#### Scenario: Human discovers schema options from repo root
- **WHEN** a human user opens the repository root `README.md`
- **THEN** they can find a self-install fallback that explains how to get the repository locally, where schema folders are copied, how a schema is activated in `openspec/config.yaml`, and how to validate the install

#### Scenario: Agent discovers deterministic install flow from repo root
- **WHEN** a coding agent opens the repository root `README.md`
- **THEN** it can find a top-level raw-README prompt handoff plus a dedicated agent-oriented install section that starts with prerequisite checks, explains the early-exit behavior, and tells it to clone the repo locally before copying the full schema directory recursively

#### Scenario: Catalog excludes schemas removed for proposal-backed rebuild
- **GIVEN** `behaviour-driven` and `intent-driven` are removed for proposal-backed rebuild
- **WHEN** a reader reviews the repository root `README.md`
- **THEN** neither schema is listed as an available schema until its replacement change is implemented and archived.

## ADDED Requirements

## REMOVED Requirements
