## 1. Refine Schema Guidance

- [x] 1.1 Update `openspec/schemas/behaviour-driven/schema.yaml` so proposal/spec/task/apply guidance requires semantic feature-file merging, upfront failing coverage for all in-scope scenarios, frozen acceptance artifacts after the failing checkpoint, scenario-slice implementation, and full-suite acceptance runs.
- [x] 1.2 Update `openspec/schemas/behaviour-driven/templates/tasks.md` so generated task lists identify existing feature files, reject duplicate feature/scenario extraction, commit full failing acceptance coverage before implementation, implement by business scenario slice, and run the full suite for every slice.
- [x] 1.3 Update `openspec/schemas/behaviour-driven/README.md` so the packaged baseline documents `features/` as canonical executable behaviour documentation and `acceptance-tests/` as runtime/test glue.

## 2. Update Canonical Behaviour Specs

- [x] 2.1 Confirm the canonical spec still lists `behaviour-driven` as the affected schema for each modified requirement.
- [x] 2.2 Confirm the canonical spec includes post-apply verification expectations for `openspec schema validate behaviour-driven`, `openspec schema review behaviour-driven`, and strict change validation.

## 3. Verify

- [x] 3.1 Run `openspec validate refine-behaviour-driven-acceptance-workflow --type change --strict`.
- [x] 3.2 Run `openspec schema validate behaviour-driven`.
- [x] 3.3 Run `openspec schema review behaviour-driven`. Note: `openspec schema review` is not yet implemented in the CLI; skipped.
- [x] 3.4 Review generated guidance for placeholder leakage and confirm no `<...>` placeholders remain in the packaged task template after implementation.
- [x] 3.5 Run `git diff <failing-acceptance-checkpoint-sha> -- features/ acceptance-tests/` and confirm no unintended modifications to committed acceptance coverage.
