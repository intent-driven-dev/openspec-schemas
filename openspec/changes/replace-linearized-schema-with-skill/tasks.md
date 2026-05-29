## 1. Remove Linearized Schema Package

- [ ] 1.1 Delete the packaged schema directory at `openspec/schemas/linearized/`.
- [ ] 1.2 Remove canonical spec coverage that requires the repository to package, activate, or validate the `linearized` schema.
- [ ] 1.3 Update `openspec/specs/custom-schema-packaging/spec.md` so the root schema catalog no longer requires a `linearized` entry.
- [ ] 1.4 Update `README.md` to remove the `Linearized` schema catalog section, activation guidance, validation command, and schema README reference.

## 2. Copy Linearized Skill Unchanged

- [ ] 2.1 Recursively copy `/Users/harikrishnan/polarizer/projects/sdd/openspec/Linear/linear-integration/.codex/skills/openspec-linearized` to `.codex/skills/openspec-linearized/`.
- [ ] 2.2 Verify the copied skill contains `SKILL.md`, `agents/openai.yaml`, and `references/lifecycle.md`.
- [ ] 2.3 Make no edits inside `.codex/skills/openspec-linearized/` after copying.
- [ ] 2.4 Confirm the copied skill directory is byte-for-byte identical to the source directory.

## 3. Verify and Wrap Up

- [ ] 3.1 Search live docs and specs for stale `linearized` schema references, including `openspec/schemas/linearized`, `schema: linearized`, and `openspec schema validate linearized`.
- [ ] 3.2 Run targeted OpenSpec checks for this change, including `openspec validate replace-linearized-schema-with-skill --strict`.
- [ ] 3.3 Run schema review for any remaining schema packages modified during implementation.
- [ ] 3.4 Prepare reviewer notes summarizing the schema removal, unchanged skill copy, and verification commands.
