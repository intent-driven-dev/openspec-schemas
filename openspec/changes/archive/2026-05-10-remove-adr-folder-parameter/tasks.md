## 1. Implement the Change

- [x] 1.1 Remove the `folder: adr` parameter from the `adr` artifact in `openspec/schemas/spec-driven-with-adr/schema.yaml`.
- [x] 1.2 Strengthen the `adr` artifact instruction to direct agents to write ADR files under the target repository's top-level `adr/` folder outside `openspec/`.
- [x] 1.3 Ensure the instruction explicitly says ADR files are not written under `openspec/changes/<change>/`.
- [x] 1.4 Preserve existing ADR immutability, supersession, sequencing, and filename guidance.

## 2. Verify and Wrap Up

- [x] 2.1 Confirm `openspec/schemas/spec-driven-with-adr/schema.yaml` no longer uses the `folder` parameter for the `adr` artifact.
- [x] 2.2 Run `openspec schema validate spec-driven-with-adr` and confirm it passes.
- [x] 2.3 Validate the delta spec acceptance criteria for the affected schema.
- [x] 2.4 Prepare concise reviewer notes describing the folder-parameter removal and plain-text ADR path instruction.
