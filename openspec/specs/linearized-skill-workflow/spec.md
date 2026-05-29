# linearized-skill-workflow Specification

## Purpose

Define how this repository vendors the Linearized OpenSpec lifecycle overlay as a Codex skill after retiring the `linearized` OpenSpec schema package.

## Requirements

### Requirement: Repository SHALL vendor the Linearized skill unchanged
The repository SHALL provide the Linearized lifecycle overlay as a local Codex skill copied unchanged from `/Users/harikrishnan/polarizer/projects/sdd/openspec/Linear/linear-integration/.codex/skills/openspec-linearized`.

#### Scenario: Skill directory is copied
- **WHEN** the Linearized skill is vendored
- **THEN** the full source skill directory is copied to `.codex/skills/openspec-linearized/`
- **AND** the copied skill contains `SKILL.md`, `agents/openai.yaml`, and `references/lifecycle.md`
- **AND** the copied files are byte-for-byte identical to the source skill files
- **AND** no implementation edits are made inside the copied skill

### Requirement: Repository SHALL reference the Linearized skill instead of the removed schema
Repository documentation and live specs SHALL stop presenting Linearized behavior as a schema package and SHALL use the local skill as the supported integration location.

#### Scenario: Live references point away from the removed schema
- **GIVEN** the `linearized` schema package has been removed
- **WHEN** repository documentation and canonical specs are updated
- **THEN** live references no longer describe the removed schema directory as an available package
- **AND** live references no longer instruct users to validate the removed schema
- **AND** live references may describe `.codex/skills/openspec-linearized/` as the supported Linearized integration location

### Requirement: Linearized replacement SHALL be verified after implementation
Implementation verification SHALL cover both stale schema reference removal and unchanged skill copy integrity.

#### Scenario: Post-apply checks confirm schema removal and copy integrity
- **GIVEN** implementation is complete
- **WHEN** post-apply verification runs
- **THEN** stale removed-schema references are absent from live repository docs and specs outside archived change history, the active change, and the unchanged copied skill
- **AND** a recursive comparison confirms `.codex/skills/openspec-linearized/` matches the source skill directory
- **AND** any affected remaining schema packages pass the repository's schema review expectation
