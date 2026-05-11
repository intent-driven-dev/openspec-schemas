## 1. Implement the Change

- [ ] 1.1 Update `openspec/schemas/intent-driven/schema.yaml` so the `adr` artifact uses `generates: "../../../adr/*.md"`.
- [ ] 1.2 Update `openspec/schemas/spec-driven-with-adr/schema.yaml` so the `adr` artifact uses `generates: "../../../adr/*.md"`.
- [ ] 1.3 Confirm ADR artifact completion is tied to repository-level `adr/*.md` output, not the presence of `proposal.md` in the change directory.

## 2. Verify and Wrap Up

- [ ] 2.1 Run `openspec schema review intent-driven`.
- [ ] 2.2 Run `openspec schema review spec-driven-with-adr`.
- [ ] 2.3 Validate acceptance criteria from both delta specs and prepare concise reviewer notes.
