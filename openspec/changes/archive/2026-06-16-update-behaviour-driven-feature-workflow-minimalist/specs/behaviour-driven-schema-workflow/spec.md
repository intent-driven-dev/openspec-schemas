## ADDED Requirements

### Requirement: Behaviour-driven schema drives feature-file acceptance workflow
The `behaviour-driven` schema MUST produce a task workflow that turns spec markdown into root-level feature files, failing acceptance tests, and application implementation steps so that behaviour changes are driven by executable Gherkin tests.

Affected schema:
- `behaviour-driven` (`openspec/schemas/behaviour-driven/`)

#### Scenario: New behaviour change follows the feature-file-first order
- **GIVEN** a new change uses the `behaviour-driven` schema
- **WHEN** the task list is generated
- **THEN** the first implementation step derives a feature file from the spec markdown and places it under `features/`
- **AND** if a corresponding feature already exists, that feature file is updated in place during the extraction step
- **AND** that extraction step installs `gherkin-lint` with `npm install gherkin-lint`
- **AND** the extracted feature is linted from `acceptance-tests/` against the root-level feature file before it is committed
- **AND** the commit only happens when lint reports zero errors
- **AND** the next step adds failing step definitions in a root-level `acceptance-tests/` Node project
- **AND** the next step implements the application
- **AND** the final step makes the Gherkin test pass
- **AND** the feature extraction, failing-test setup, and application steps are committed to git as separate logical checkpoints.

### Requirement: Behaviour-driven schema updates existing features in place
The `behaviour-driven` schema MUST identify the existing feature file for a modified capability during feature extraction so that updates to existing behaviour are applied to the right feature instead of creating a duplicate.

Affected schema:
- `behaviour-driven` (`openspec/schemas/behaviour-driven/`)

#### Scenario: Modified behaviour updates the matching feature file
- **GIVEN** a change modifies an existing feature
- **WHEN** the task list is generated
- **THEN** it identifies which `features/*.feature` file needs to be updated
- **AND** it updates that feature file during the extraction step before any new implementation work
- **AND** it does not default to creating a brand-new feature file for an existing capability.

### Requirement: Behaviour-driven schema changes are validated after apply
The `behaviour-driven` schema MUST include a post-apply change validation step so the updated package is verified before completion.

Affected schema:
- `behaviour-driven` (`openspec/schemas/behaviour-driven/`)

#### Scenario: Post-apply validation runs for schema changes
- **GIVEN** files under `openspec/schemas/behaviour-driven/` are changed
- **WHEN** the change is applied
- **THEN** the verification plan includes `openspec validate update-behaviour-driven-feature-workflow-minimalist --type change --strict`
- **AND** the change is not complete until that validation passes.

## MODIFIED Requirements

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
