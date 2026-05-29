## Purpose

Define packaging and documentation conventions for reusable, project-local OpenSpec schemas.
## Requirements
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

### Requirement: Each schema SHALL include usage and activation guidance
Each custom schema folder SHALL include documentation that explains intended use, unsuitable use cases, and activation steps through `openspec/config.yaml`.

#### Scenario: Coding agent activates schema from schema README
- **WHEN** a coding agent reads a schema folder README
- **THEN** it can determine whether the schema fits and can instruct the user to set `schema: <schema-name>` in `openspec/config.yaml`

### Requirement: Repository root SHALL provide catalog and install guidance for humans and agents
The repository root SHALL include a `README.md` that explains the purpose of this schema collection, starts the main install section with an agent-oriented prompt that points to the raw root `README.md`, gives a self-install fallback for human readers, includes a dedicated agent-oriented install flow that removes ambiguity about prerequisites and copying the full schema folder, and lists only currently packaged schemas with canonical spec coverage.

#### Scenario: Human discovers schema options from repo root
- **WHEN** a human user opens the repository root `README.md`
- **THEN** they can find a self-install fallback that explains how to get the repository locally, where schema folders are copied, how a schema is activated in `openspec/config.yaml`, and how to validate the install

#### Scenario: Agent discovers deterministic install flow from repo root
- **WHEN** a coding agent opens the repository root `README.md`
- **THEN** it can find a top-level raw-README prompt handoff plus a dedicated agent-oriented install section that starts with prerequisite checks, explains the early-exit behavior, and tells it to clone the repo locally before copying the full schema directory recursively

#### Scenario: Human discovers the intent-driven schema from the root catalog
- **WHEN** a human user opens the repository root `README.md`
- **THEN** they can find `intent-driven` in the schema catalog
- **AND** they can find a reference to `openspec/schemas/intent-driven/README.md`.

#### Scenario: Agent can install the intent-driven schema from catalog guidance
- **WHEN** a coding agent follows the repository install guidance for `intent-driven`
- **THEN** it can copy the full `openspec/schemas/intent-driven/` folder into a target project's `openspec/schemas/intent-driven/`
- **AND** activate it with `schema: intent-driven`.

### Requirement: Schema changes SHALL be validated with OpenSpec CLI
Any new schema or schema modification in this repository SHALL be verified by running `openspec schema validate <schema-name>` before considering the change complete.

#### Scenario: Schema passes structural validation
- **WHEN** a contributor finishes creating or editing a schema
- **THEN** they run `openspec schema validate <schema-name>` and confirm the command reports successful validation
