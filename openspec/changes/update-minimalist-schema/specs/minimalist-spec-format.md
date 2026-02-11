## ADDED Requirements

### Requirement: User-story-based specification template in minimalist schema
The `openspec/schemas/minimalist/templates/specs/spec.md` template MUST guide authors to express requirements as user stories and acceptance criteria in Gherkin format.

Affected schema:
- `minimalist` (`openspec/schemas/minimalist/`)

#### Scenario: New spec follows user story and Gherkin acceptance criteria
- **WHEN** a contributor generates or edits a `specs` artifact using the minimalist schema
- **THEN** the template presents user-story phrasing (for example: As a <role>, I want <capability>, so that <benefit>) and acceptance criteria written with Gherkin structure (`Given/When/Then`)

### Requirement: Schema guidance remains coherent with updated spec template
Any supporting files under `openspec/schemas/minimalist/` that define artifact expectations MUST align with the user-story and Gherkin acceptance-criteria format so generated instructions and examples are consistent.

Affected schema:
- `minimalist` (`openspec/schemas/minimalist/`)

#### Scenario: Supporting schema content matches the new format
- **WHEN** instructions or metadata in `openspec/schemas/minimalist/` describe how to author spec artifacts
- **THEN** they consistently reference user stories and Gherkin acceptance criteria rather than generic requirement prose

#### Scenario: Post-apply schema review validates the updated schema
- **WHEN** implementation is complete and applied
- **THEN** running `openspec schema review minimalist` succeeds and confirms the schema remains valid after these format changes

## MODIFIED Requirements

### Requirement: Spec artifact authoring expectations
The minimalist schema's previous free-form requirement/scenario guidance is replaced with explicit user-story structure and Gherkin acceptance criteria for clearer, testable specification authoring.

#### Scenario: Existing contributors adapt to the revised structure
- **WHEN** an author updates an existing change spec under the minimalist workflow
- **THEN** the author can map prior requirement text into user stories plus `Given/When/Then` acceptance criteria without ambiguity

## REMOVED Requirements

### Requirement: No removals
This change does not remove a capability; it refines how spec content is structured and described.
