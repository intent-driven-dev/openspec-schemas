# Reviewer Notes

## Changed Files in `openspec/schemas/minimalist/`

- `openspec/schemas/minimalist/templates/specs/spec.md`
  - Reworked the spec template from generic requirement/scenario placeholders to explicit user-story sections and Gherkin-style acceptance criteria (`Given/When/Then`) to enforce the new authoring format.
- `openspec/schemas/minimalist/schema.yaml`
  - Updated the `specs` artifact description so schema metadata matches the new template expectations (user stories + Gherkin acceptance criteria).
- `openspec/schemas/minimalist/README.md`
  - Added a `Spec Format` section with concrete authoring guidance and examples to keep user-facing schema instructions aligned with the updated template.

## Verification

- Ran `openspec schema validate minimalist` and confirmed: `Schema 'minimalist' is valid`.
