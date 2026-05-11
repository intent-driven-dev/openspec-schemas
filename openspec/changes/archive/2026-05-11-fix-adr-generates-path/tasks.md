## 1. Implement the Change

- [x] 1.1 Update `openspec/schemas/intent-driven/schema.yaml` so the `adr` artifact uses `generates: "../../../adr/*.md"`.
- [x] 1.2 Update `openspec/schemas/spec-driven-with-adr/schema.yaml` so the `adr` artifact uses `generates: "../../../adr/*.md"`.
- [x] 1.3 Confirm ADR artifact completion is tied to repository-level `adr/*.md` output, not the presence of `proposal.md` in the change directory.

## 2. Verify and Wrap Up

- [x] 2.1 Run `openspec schema review intent-driven`.
- [x] 2.2 Run `openspec schema review spec-driven-with-adr`.
- [x] 2.3 Validate acceptance criteria from both delta specs and prepare concise reviewer notes.
