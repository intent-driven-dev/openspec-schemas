## Purpose

Provide guidance for understanding OpenSpec schema internals and authoring custom schemas in this repository.

## Requirements

### Requirement: OpenSpec Schema Reference Skill
The change MUST add a reusable Codex skill that provides detailed guidance for understanding OpenSpec schema structure and creating custom schemas in this repository.

#### Scenario: Discover schema anatomy
- **WHEN** a user asks for help understanding an OpenSpec workflow schema (for example `spec-driven`)
- **THEN** the skill explains key schema components, artifact sequencing, dependencies, validation rules, and how they map to artifact creation behavior in this repo

#### Scenario: Guide custom schema authoring
- **WHEN** a user asks to create or modify a custom schema in this repository
- **THEN** the skill provides step-by-step authoring guidance, including schema file layout, required fields, and practical examples aligned to repo conventions

#### Scenario: Enforce schema verification expectations
- **WHEN** schema files are added or changed under `openspec/schemas/`
- **THEN** the guidance includes a post-apply verification step requiring `openspec schema review <schema-name>` for each affected schema before completion

### Requirement: Schema-Creation Decision Support
The skill MUST help users choose appropriate workflow patterns for their use case rather than only describing syntax.

#### Scenario: Compare workflow tradeoffs
- **WHEN** a user is selecting between workflow styles (for example minimalist, spec-driven, or test-oriented flows)
- **THEN** the skill explains tradeoffs, artifact burden, and when each workflow is appropriate

#### Scenario: Drafting support for new schemas
- **WHEN** a user describes a desired workflow behavior
- **THEN** the skill translates that intent into a concrete schema drafting plan with ordered artifacts and dependency expectations
