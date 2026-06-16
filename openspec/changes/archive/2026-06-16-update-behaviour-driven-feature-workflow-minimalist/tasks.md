## 1. Update schema guidance

- [x] 1.1 Update `openspec/schemas/behaviour-driven/schema.yaml` so the `tasks` artifact describes the feature-file-first workflow, the failing `acceptance-tests/` step-definition step, the application implementation step, and the existing-feature update rule.
- [x] 1.2 Update `openspec/schemas/behaviour-driven/README.md` to explain that downstream projects should create root-level `features/` files and keep acceptance tests in a root-level `acceptance-tests/` Node project.
- [x] 1.3 Update `openspec/schemas/behaviour-driven/templates/spec.md` so spec authors write markdown that can be converted into feature files for acceptance testing.
- [x] 1.4 Remove any remaining schema guidance that tells contributors not to create `.feature` files.

## 2. Rewrite the task template

- [x] 2.1 Rewrite `openspec/schemas/behaviour-driven/templates/tasks.md` so generated task lists always follow this order: derive the feature file, install `gherkin-lint`, run it until zero errors, add failing step definitions, implement the application, then make the Gherkin test pass.
- [x] 2.2 Add explicit instructions for modified capabilities so the task list identifies the existing feature file to update during feature extraction rather than later.
- [x] 2.3 Add git commit checkpoints after each logical step so feature extraction, failing acceptance tests, and application work are committed separately.

## 3. Verify

- [x] 3.1 Run `openspec validate update-behaviour-driven-feature-workflow-minimalist --type change --strict`.
- [x] 3.2 Confirm the generated task template says `gherkin-lint` runs from `acceptance-tests/` against the root-level feature file and must pass with zero errors before commit.
