## 1. Remove Linearized Schema Package

- [x] 1.1 Delete the packaged schema directory at `openspec/schemas/linearized/`.
- [x] 1.2 Remove canonical spec coverage that requires the repository to package, activate, or validate the `linearized` schema.
- [x] 1.3 Update `openspec/specs/custom-schema-packaging/spec.md` so the root schema catalog no longer requires a `linearized` entry.
- [x] 1.4 Update `README.md` to remove the `Linearized` schema catalog section, activation guidance, validation command, and schema README reference.

## 2. Copy Linearized Skill Unchanged

- [x] 2.1 Recursively copy `/Users/harikrishnan/polarizer/projects/sdd/openspec/Linear/linear-integration/.codex/skills/openspec-linearized` to `.codex/skills/openspec-linearized/`.
- [x] 2.2 Verify the copied skill contains `SKILL.md`, `agents/openai.yaml`, and `references/lifecycle.md`.
- [x] 2.3 Make no edits inside `.codex/skills/openspec-linearized/` after copying.
- [x] 2.4 Confirm the copied skill directory is byte-for-byte identical to the source directory.

## 3. Verify and Wrap Up

- [x] 3.1 Search live docs and specs for stale `linearized` schema references, excluding archived history, this change, and the unchanged copied skill.
- [x] 3.2 Run targeted OpenSpec checks for this change, including `openspec validate replace-linearized-schema-with-skill --type change --strict`.
- [x] 3.3 Confirm no remaining schema packages were modified that require schema review.
- [x] 3.4 Review final changes and verification output.
