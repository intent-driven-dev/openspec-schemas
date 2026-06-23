## 1. Update ADR Artifact Contract

- [x] 1.1 Change the `intent-driven` `adr` artifact `generates` value from `../../../adr/*.md` to `adr.md`.
- [x] 1.2 Update the ADR artifact instructions so `openspec/changes/<change>/adr.md` is a concise per-change ADR review manifest and completion marker.
- [x] 1.3 Preserve repository-level durable ADR creation under `<repo>/adr/NNNN-kebab-title.md` whenever the change introduces a major durable architectural decision.
- [x] 1.4 Update the no-new-ADR path so the `adr` step completes by writing an `adr.md` manifest that states ADR review completed, lists reviewed ADR context, and records that no major durable architectural decisions were introduced.

## 2. Update Templates and Documentation

- [x] 2.1 Update `openspec/schemas/intent-driven/templates/adr.md` so it is a change-local ADR review manifest that references every durable repository-level ADR file created for the change without duplicating full ADR content, or explicitly says none were created because no major durable decisions were made.
- [x] 2.2 Update `openspec/schemas/intent-driven/README.md` to distinguish the change-local `adr.md` review artifact from persistent top-level ADR files.
- [x] 2.3 Update root or schema catalog documentation only if it currently describes repository-level ADR files as the artifact completion signal for `intent-driven`.

## 3. Verify

- [x] 3.1 Run `openspec validate align-intent-driven-adr-completion --type change --strict` and resolve any delta-spec issues.
- [x] 3.2 Run `openspec schema validate intent-driven` and resolve any schema validation issues.
- [x] 3.3 Validate the delta-spec acceptance criteria and prepare concise reviewer notes.
