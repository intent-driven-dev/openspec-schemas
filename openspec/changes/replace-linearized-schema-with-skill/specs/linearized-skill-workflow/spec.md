## ADDED Requirements

### Requirement: Repository SHALL vendor the Linearized skill unchanged
The repository SHALL provide the Linearized lifecycle overlay as a local Codex skill copied unchanged from `/Users/harikrishnan/polarizer/projects/sdd/openspec/Linear/linear-integration/.codex/skills/openspec-linearized`.

#### Scenario: Skill directory is copied
- **WHEN** the change is implemented
- **THEN** the full source skill directory is copied to `.codex/skills/openspec-linearized/`
- **AND** the copied skill contains `SKILL.md`, `agents/openai.yaml`, and `references/lifecycle.md`
- **AND** the copied files are byte-for-byte identical to the source skill files
- **AND** no implementation edits are made inside the copied skill

### Requirement: Repository SHALL reference the Linearized skill instead of the removed schema
Repository documentation and live specs SHALL stop presenting Linearized behavior as a schema package and SHALL use the local skill as the supported integration location.

#### Scenario: Live references point away from the removed schema
- **GIVEN** the `linearized` schema package has been removed
- **WHEN** repository documentation and canonical specs are updated
- **THEN** live references no longer describe `openspec/schemas/linearized/` as an available package
- **AND** live references no longer instruct users to run `openspec schema validate linearized`
- **AND** live references may describe `.codex/skills/openspec-linearized/` as the supported Linearized integration location

### Requirement: Linearized replacement SHALL be verified after implementation
Implementation verification SHALL cover both stale schema reference removal and unchanged skill copy integrity.

#### Scenario: Post-apply checks confirm schema removal and copy integrity
- **GIVEN** implementation is complete
- **WHEN** post-apply verification runs
- **THEN** `rg -n "openspec/schemas/linearized|schema: linearized|openspec schema validate linearized" README.md openspec .codex` finds no live references outside archived change history or the new change itself
- **AND** a recursive comparison confirms `.codex/skills/openspec-linearized/` matches the source skill directory
- **AND** any affected remaining schema packages pass the repository's schema review expectation
