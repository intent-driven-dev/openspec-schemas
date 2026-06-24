## 1. Refine Schema Guidance

- [ ] 1.1 Update `openspec/schemas/behaviour-driven/schema.yaml` so proposal/spec/task/apply guidance requires semantic feature-file merging, upfront failing coverage for all in-scope scenarios, frozen acceptance artifacts after the failing checkpoint, scenario-slice implementation, and full-suite acceptance runs.
- [ ] 1.2 Update `openspec/schemas/behaviour-driven/templates/tasks.md` so generated task lists identify existing feature files, reject duplicate feature/scenario extraction, commit full failing acceptance coverage before implementation, implement by business scenario slice, and run the full suite for every slice.
- [ ] 1.3 Update `openspec/schemas/behaviour-driven/README.md` so the packaged baseline documents `features/` as canonical executable behaviour documentation and `acceptance-tests/` as runtime/test glue.

## 2. Update Canonical Behaviour Specs

- [ ] 2.1 Update `openspec/specs/behaviour-driven-schema-workflow/spec.md` with the archived version of this change's modified requirements.
- [ ] 2.2 Confirm the canonical spec still lists `behaviour-driven` as the affected schema for each modified requirement.
- [ ] 2.3 Confirm the canonical spec includes post-apply verification expectations for `openspec schema validate behaviour-driven`, `openspec schema review behaviour-driven`, and strict change validation.

## 3. Verify

- [ ] 3.1 Run `openspec validate refine-behaviour-driven-acceptance-workflow --type change --strict`.
- [ ] 3.2 Run `openspec schema validate behaviour-driven`.
- [ ] 3.3 Run `openspec schema review behaviour-driven`.
- [ ] 3.4 Review generated guidance for placeholder leakage and confirm no `<...>` placeholders remain in the packaged task template after implementation.
