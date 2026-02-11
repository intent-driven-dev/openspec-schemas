## ADDED Requirements

### Requirement: Repository SHALL package each custom schema in a self-contained folder
The repository SHALL organize custom OpenSpec schemas as one folder per schema, where each folder contains all files required for a user or coding agent to install that schema into a target project.

#### Scenario: Installable schema folder exists
- **WHEN** a user selects a schema from this repository
- **THEN** that schema is available as a single folder that can be copied into `openspec/schemas/<schema-name>/` in the target project

### Requirement: Each schema SHALL include usage and installation guidance
Each custom schema folder SHALL include documentation that explains intended use, unsuitable use cases, install steps, and activation steps through `openspec/config.yaml`.

#### Scenario: Coding agent installs schema from repository docs
- **WHEN** a coding agent reads a schema folder README
- **THEN** it can install the schema by copying the folder to the target project's local OpenSpec schemas directory and can instruct the user to set `schema: <schema-name>` in `openspec/config.yaml`

### Requirement: Repository root SHALL provide catalog and agent quick-start guidance
The repository root SHALL include a `README.md` that explains the purpose of this schema collection and directs users and coding agents to evaluate each schema folder README before selecting and installing a schema.

#### Scenario: Agent discovers schema options from repo root
- **WHEN** a coding agent opens the repository root `README.md`
- **THEN** it can understand the repository purpose and follow quick-start guidance to inspect schema-specific README files before installation

### Requirement: Schema changes SHALL be validated with OpenSpec CLI
Any new schema or schema modification in this repository SHALL be verified by running `openspec schema validate <schema-name>` before considering the change complete.

#### Scenario: Schema passes structural validation
- **WHEN** a contributor finishes creating or editing a schema
- **THEN** they run `openspec schema validate <schema-name>` and confirm the command reports successful validation
