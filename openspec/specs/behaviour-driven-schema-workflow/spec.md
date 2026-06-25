# behaviour-driven-schema-workflow Specification

## Purpose

Define the packaged `behaviour-driven` schema as an opinionated BDD baseline
that turns OpenSpec Markdown behaviour specs into root-level Gherkin feature
files, failing acceptance tests, granular implementation work, and passing
acceptance verification.

## Requirements

### Requirement: Behaviour-driven schema SHALL drive a feature-file acceptance workflow
The `behaviour-driven` schema MUST produce a task workflow that turns spec markdown into root-level feature files, failing acceptance tests, and application implementation steps so that behaviour changes are driven by executable Gherkin tests.

Affected schema:
- `behaviour-driven` (`openspec/schemas/behaviour-driven/`)

#### Scenario: New behaviour change follows the feature-file-first order
- **GIVEN** a new change uses the `behaviour-driven` schema
- **WHEN** the task list is generated
- **THEN** the first implementation gate derives feature files from the spec markdown and places them under `features/`
- **AND** if a corresponding feature already exists, that feature file is updated in place during the extraction gate
- **AND** that extraction gate installs `gherkin-lint` with `npm install gherkin-lint`
- **AND** extracted features are linted once from `acceptance-tests/` against the root-level feature files before they are committed
- **AND** feature extraction is committed only after lint reports zero errors
- **AND** the next gate adds failing step definitions in a root-level `acceptance-tests/` Node project
- **AND** the next gate implements the application
- **AND** the final implementation gate makes the Gherkin tests pass.

#### Scenario: Existing behaviour updates the matching feature file
- **GIVEN** a change modifies an existing feature
- **WHEN** the task list is generated
- **THEN** it identifies which `features/*.feature` file needs to be updated
- **AND** it updates that feature file during the extraction gate before any new implementation work
- **AND** it does not default to creating a brand-new feature file for an existing capability.

### Requirement: Behaviour-driven tasks SHALL be generated from a gate contract
The `behaviour-driven` schema MUST treat the task template as a reusable contract with mandatory gates and placeholders, not as a fixed procedure to copy verbatim.

Affected schema:
- `behaviour-driven` (`openspec/schemas/behaviour-driven/`)

#### Scenario: Generated tasks preserve required gates without copying placeholders
- **GIVEN** proposal, specs, and design artifacts are complete
- **WHEN** `tasks.md` is generated
- **THEN** the generated checklist keeps the required feature extraction, failing acceptance-test, granular implementation, and verification sections
- **AND** every `<...>` placeholder from the template is replaced with change-specific detail
- **AND** the generated checklist does not present the template as a verbatim procedure to follow exactly
- **AND** each tracked task uses checkbox syntax `- [ ] X.Y Task description`.

#### Scenario: Generated tasks are granular by affected subsystem
- **GIVEN** a behaviour change affects implementation code
- **WHEN** `tasks.md` is generated
- **THEN** implementation work is expanded into concrete tasks for each affected subsystem
- **AND** relevant API handlers, domain services, persistence, CLI/UI surfaces, adapters, configuration, docs, fixtures, and test helpers are named when they are in scope
- **AND** the implementation gate is not consolidated into a single broad catch-all task.

### Requirement: Behaviour-driven commit gates SHALL be mandatory
The `behaviour-driven` schema MUST require git commit checkpoints before crossing the BDD gates so feature extraction, failing acceptance coverage, and passing implementation are auditable.

Affected schema:
- `behaviour-driven` (`openspec/schemas/behaviour-driven/`)

#### Scenario: Commit checkpoints separate the BDD gates
- **GIVEN** a generated task list is applied
- **WHEN** the contributor completes feature extraction
- **THEN** they commit the feature extraction work before starting failing acceptance-test setup
- **AND** after the failing acceptance tests are added and confirmed to fail for the expected behaviour, they commit that setup before implementation
- **AND** after implementation makes the acceptance tests pass, they commit the passing implementation before final verification.

#### Scenario: Apply pauses when a required commit cannot be made
- **GIVEN** a contributor reaches a commit checkpoint
- **WHEN** git commit is unavailable, unsafe, or blocked by policy
- **THEN** the apply guidance requires the contributor to pause before crossing into the next gate.

### Requirement: Behaviour-driven acceptance-test project SHALL follow Node and JavaScript hygiene
The `behaviour-driven` schema MUST require the root-level `acceptance-tests/` Node project to follow JavaScript coding standards and keep dependency directories out of git.

Affected schema:
- `behaviour-driven` (`openspec/schemas/behaviour-driven/`)

#### Scenario: Acceptance-test project ignores node_modules
- **WHEN** the acceptance-test Node project is scaffolded or updated
- **THEN** `node_modules/` under `acceptance-tests/` is ignored by git
- **AND** generated task guidance does not ask contributors to commit installed dependency directories.

#### Scenario: Acceptance-test JavaScript has lintable coding standards
- **WHEN** failing acceptance-test setup is generated
- **THEN** the task list includes JavaScript coding-standard tooling or package scripts for acceptance-test code
- **AND** step definitions, helpers, and fixtures are checked by that JavaScript linting task.

### Requirement: Behaviour-driven acceptance tests SHALL generate HTML reports
The `behaviour-driven` schema MUST require acceptance-test runs to produce an HTML report so contributors can inspect how the executable scenarios ran.

Affected schema:
- `behaviour-driven` (`openspec/schemas/behaviour-driven/`)

#### Scenario: Failing and passing acceptance runs produce an HTML report
- **WHEN** the generated task list runs acceptance tests
- **THEN** the acceptance runner is configured to write an HTML report path
- **AND** the failing-test checkpoint runs with HTML report output
- **AND** the passing implementation checkpoint records the HTML report from the final run.

### Requirement: Behaviour-driven acceptance execution SHALL be bounded
The `behaviour-driven` schema MUST make implementation acceptance execution a bounded loop using a user-selected attempt limit with a default of 3 attempts.

Affected schema:
- `behaviour-driven` (`openspec/schemas/behaviour-driven/`)

#### Scenario: Acceptance loop asks for an attempt limit
- **GIVEN** failing acceptance tests have been committed
- **WHEN** implementation work is being planned or verified
- **THEN** the generated task guidance asks the user how many acceptance-fix attempts to allow
- **AND** if the user does not choose a limit, the guidance records and uses the default of 3 attempts.

#### Scenario: Acceptance loop retries failed implementation up to the chosen limit
- **GIVEN** an acceptance-fix attempt limit has been recorded
- **WHEN** implementation work is being verified
- **THEN** the contributor runs the acceptance test suite with HTML report output
- **AND** if the suite passes, the contributor proceeds to completion
- **AND** if the suite fails, the contributor fixes implementation code and reruns the suite
- **AND** the generated task list limits this loop to the recorded attempt limit.

#### Scenario: Generated tasks record each acceptance attempt
- **GIVEN** an acceptance-fix attempt limit has been recorded
- **WHEN** `tasks.md` is generated
- **THEN** the generated checklist includes one checkbox per allowed acceptance attempt
- **AND** each attempt checkbox identifies its attempt number, total attempt limit, and HTML report path.

#### Scenario: Unused acceptance attempts are not marked as run
- **GIVEN** an acceptance attempt passes before the recorded attempt limit is reached
- **WHEN** the contributor updates `tasks.md`
- **THEN** only the attempts that actually ran are marked complete
- **AND** the remaining unrun attempt checkboxes are replaced with a completed "not needed" checkpoint that records which attempt passed.

#### Scenario: Acceptance loop exits after repeated failures
- **GIVEN** the final allowed acceptance attempt still fails
- **WHEN** the contributor reaches the loop limit
- **THEN** the task guidance requires stopping with an error saying there are still errors
- **AND** the error includes the HTML report path.

### Requirement: Behaviour-driven acceptance tests SHALL not be weakened after the failing-test checkpoint
The `behaviour-driven` schema MUST protect committed feature files and acceptance tests from being weakened merely to make implementation pass.

Affected schema:
- `behaviour-driven` (`openspec/schemas/behaviour-driven/`)

#### Scenario: Verification reviews acceptance-test integrity
- **GIVEN** failing acceptance tests have been committed
- **WHEN** implementation reaches final verification
- **THEN** the task list includes a review step confirming feature files and acceptance tests were not weakened after the failing-test checkpoint
- **AND** legitimate behaviour corrections require deliberate OpenSpec artifact updates rather than silent test weakening.

### Requirement: Behaviour-driven README SHALL position the schema as a demonstration baseline
The `behaviour-driven` README MUST describe the package as an opinionated demonstration-quality baseline with mandatory defaults, while noting the places teams commonly customize after forking or tuning.

Affected schema:
- `behaviour-driven` (`openspec/schemas/behaviour-driven/`)

#### Scenario: README documents the canonical flow and default tooling
- **WHEN** a contributor reads the schema README
- **THEN** it describes the canonical flow as OpenSpec markdown specs to root feature files to failing acceptance tests to implementation to passing acceptance tests
- **AND** it identifies root-level `features/*.feature`, a root-level `acceptance-tests/` Node project, mandatory `gherkin-lint`, JavaScript coding standards, HTML acceptance reports, and git checkpoint commits as the default workflow.

#### Scenario: README documents customization boundaries
- **WHEN** a team evaluates the schema for local use
- **THEN** the README explains that feature-file layout, acceptance runner, lint command, commit policy, and CI enforcement may need local tuning
- **AND** it does not present the packaged baseline as a universal prescription for every team.

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
- **AND** directs `THEN` steps to express observable outcomes rather than implementation details.

#### Scenario: Modified behaviours copy existing Markdown requirement content before editing
- **GIVEN** a change modifies an existing behaviour capability
- **WHEN** the contributor creates the change spec file
- **THEN** the schema guidance tells them to copy the full existing requirement block from `openspec/specs/<capability>/spec.md`
- **AND** edit the copied content so it represents the full desired behaviour after the change.

### Requirement: Behaviour-driven schema SHALL validate cleanly
Changes adding or modifying `openspec/schemas/behaviour-driven/` SHALL pass OpenSpec schema validation before completion.

#### Scenario: Schema validation passes
- **WHEN** implementation changes files under `openspec/schemas/behaviour-driven/`
- **THEN** `openspec schema validate behaviour-driven` passes before the change is considered complete.

#### Scenario: Strict change validation is included when behaviour specs change
- **WHEN** a behaviour-driven schema change also updates OpenSpec change artifacts
- **THEN** the verification plan includes `openspec validate <change-name> --type change --strict`
- **AND** the change is not complete until that validation passes.
