## MODIFIED Requirements

### Requirement: Behaviour-driven schema SHALL drive a feature-file acceptance workflow
The `behaviour-driven` schema MUST produce a task workflow that turns spec markdown into root-level feature files, committed failing acceptance tests, scenario-sliced application implementation, and full-suite acceptance verification so that behaviour changes are driven by executable Gherkin tests.

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
- **AND** the failing acceptance gate covers every in-scope business scenario from the OpenSpec delta before implementation begins
- **AND** the next gate implements the application in scenario slices
- **AND** each slice runs the full acceptance suite with HTML report output
- **AND** the final implementation gate makes the full Gherkin suite pass.

#### Scenario: Existing behaviour updates the matching feature file
- **GIVEN** a change modifies an existing feature
- **WHEN** the task list is generated
- **THEN** it identifies which `features/*.feature` file needs to be updated
- **AND** it updates that feature file during the extraction gate before any new implementation work
- **AND** it semantically patches matching feature, rule, scenario, examples, tag, and background content instead of overwriting unrelated scenarios
- **AND** it does not default to creating a brand-new feature file for an existing capability.

#### Scenario: Incremental changes merge feature files semantically
- **GIVEN** a change updates behaviour already represented in `features/*.feature`
- **WHEN** the feature extraction gate is applied
- **THEN** the generated task guidance requires contributors to preserve unrelated scenarios in the existing feature file
- **AND** matching scenarios are edited in place when their accepted behaviour changes
- **AND** new scenarios are added to the matching feature file when they extend the same capability
- **AND** scenarios that are explicitly removed in the spec delta are deleted from the matching feature file
- **AND** when a scenario is deleted from a feature file, the corresponding step definitions, fixtures, and helpers in `acceptance-tests/` are removed in sync so that feature files and acceptance tests remain coherent
- **AND** duplicate feature files or duplicate scenarios are rejected before the feature extraction commit.

### Requirement: Behaviour-driven tasks SHALL be generated from a gate contract
The `behaviour-driven` schema MUST treat the task template as a reusable contract with mandatory gates and placeholders, not as a fixed procedure to copy verbatim.

Affected schema:
- `behaviour-driven` (`openspec/schemas/behaviour-driven/`)

#### Scenario: Generated tasks preserve required gates without copying placeholders
- **GIVEN** proposal, specs, and design artifacts are complete
- **WHEN** `tasks.md` is generated
- **THEN** the generated checklist keeps the required feature extraction, failing acceptance-test, scenario-sliced implementation, and verification sections
- **AND** every `<...>` placeholder from the template is replaced with change-specific detail
- **AND** the generated checklist does not present the template as a verbatim procedure to follow exactly
- **AND** each tracked task uses checkbox syntax `- [ ] X.Y Task description`.

#### Scenario: Generated tasks are granular by affected subsystem
- **GIVEN** a behaviour change affects implementation code
- **WHEN** `tasks.md` is generated
- **THEN** implementation work is expanded into concrete tasks for each affected subsystem
- **AND** relevant API handlers, domain services, persistence, CLI/UI surfaces, adapters, configuration, docs, fixtures, and test helpers are named when they are in scope
- **AND** the implementation gate is not consolidated into a single broad catch-all task.

#### Scenario: Generated tasks measure progress by business scenarios
- **GIVEN** failing acceptance coverage has been committed
- **WHEN** implementation tasks are generated
- **THEN** each implementation slice identifies the business scenario or scenario group it intends to turn green
- **AND** the slice is considered complete only when those scenarios pass in the full acceptance suite
- **AND** task progress is not measured by step definitions being present, pending, or no longer undefined.

### Requirement: Behaviour-driven acceptance execution SHALL be bounded
The `behaviour-driven` schema MUST make implementation acceptance execution a bounded loop using a user-selected attempt limit with a default of 3 attempts, and MUST run the full acceptance suite for each scenario slice.

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
- **THEN** the contributor runs the full acceptance test suite with HTML report output
- **AND** if the suite passes, the contributor proceeds to completion
- **AND** if the suite fails only for scenarios listed as not-yet-implemented in the current task checklist for this slice, the contributor continues with the next planned scenario slice
- **AND** if the suite fails for any implemented scenario or regression, the contributor fixes implementation code and reruns the suite
- **AND** the generated task list limits this loop to the recorded attempt limit.

#### Scenario: Generated tasks record each acceptance attempt
- **GIVEN** an acceptance-fix attempt limit has been recorded
- **WHEN** `tasks.md` is generated
- **THEN** the generated checklist includes one checkbox per allowed acceptance attempt
- **AND** each attempt checkbox identifies its attempt number, total attempt limit, expected scenario-slice target, recorded not-yet-implemented scenarios, and HTML report path.

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

#### Scenario: Each slice runs the full acceptance suite
- **GIVEN** implementation is proceeding by scenario slices
- **WHEN** a contributor completes a slice
- **THEN** they run the full acceptance suite instead of only running the scenario or tag they just implemented
- **AND** all previously implemented scenarios must remain green
- **AND** the only acceptable red scenarios are those listed as not-yet-implemented in the current task checklist.

### Requirement: Behaviour-driven acceptance tests SHALL not be weakened after the failing-test checkpoint
The `behaviour-driven` schema MUST protect committed feature files and acceptance tests from being weakened merely to make implementation pass.

Affected schema:
- `behaviour-driven` (`openspec/schemas/behaviour-driven/`)

#### Scenario: Verification reviews acceptance-test integrity
- **GIVEN** failing acceptance tests have been committed
- **WHEN** implementation reaches final verification
- **THEN** the task list includes a review step confirming feature files and acceptance tests were not weakened after the failing-test checkpoint
- **AND** legitimate behaviour corrections require deliberate OpenSpec artifact updates rather than silent test weakening.

#### Scenario: Acceptance coverage is frozen during implementation
- **GIVEN** the failing acceptance-test checkpoint has been committed
- **WHEN** implementation work begins
- **THEN** generated task guidance treats `features/` and `acceptance-tests/` as off limits for ordinary implementation fixes
- **AND** step definitions, fixtures, helpers, or feature text are not changed merely to make failing scenarios pass
- **AND** any necessary correction to accepted behaviour requires updating the OpenSpec change artifacts before modifying committed feature or acceptance-test files
- **AND** the final verification gate reviews changes since the failing acceptance checkpoint.
