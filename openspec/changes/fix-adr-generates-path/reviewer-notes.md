## Reviewer Notes

- Updated `openspec/schemas/intent-driven/schema.yaml` so the `adr` artifact generates `../../../adr/*.md`.
- Updated `openspec/schemas/spec-driven-with-adr/schema.yaml` so the `adr` artifact generates `../../../adr/*.md`.
- This ties ADR artifact completion to repository-level `adr/*.md` files relative to the change directory, so a change-local `proposal.md` no longer satisfies the ADR artifact glob.
- `openspec schema review <name>` is not supported by the installed CLI; it exits with `unknown command 'review'`.
- Equivalent schema validation passed with `openspec schema validate intent-driven`.
- Equivalent schema validation passed with `openspec schema validate spec-driven-with-adr`.
- Strict change validation passed with `openspec validate fix-adr-generates-path --type change --strict`.
