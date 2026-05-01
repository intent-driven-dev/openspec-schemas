## 1. Add Schema Package

- [x] 1.1 Create `openspec/schemas/spec-driven-with-adr/` as a self-contained schema folder.
- [x] 1.2 Copy `schema.yaml` and templates from reference location.
- [x] 1.3 Rename the schema in `schema.yaml` to `spec-driven-with-adr` and confirm every referenced template exists in the new folder.

## 2. Document Usage and Catalog Entry

- [x] 2.1 Add `openspec/schemas/spec-driven-with-adr/README.md` with purpose, good-fit and non-fit guidance, activation instructions, workflow order, and ADR persistence behavior.
- [x] 2.2 Update the root `README.md` to list `spec-driven-with-adr` and link to its schema README.
- [x] 2.3 Confirm install guidance remains consistent with the repository's one-folder-per-schema packaging convention.

## 3. Verify Schema Quality

- [x] 3.1 Run `openspec schema validate spec-driven-with-adr` and resolve any schema or template resolution errors.
- [x] 3.2 Run `openspec schema validate spec-driven-with-adr` as the schema quality gate and confirm it passes.
- [x] 3.3 Validate acceptance criteria from the delta spec.

## 4. Wrap Up

- [x] 4.1 Remove temporary debugging code and notes.
- [x] 4.2 Prepare concise reviewer notes if requested.
