# Tasks Template Contract

Replace every `<...>` placeholder with change-specific detail before treating
the task list as ready. Keep gate order, checkbox format, and commit
checkpoints. Add one implementation task per affected subsystem.

## 1. Feature Extraction Gate

- [ ] 1.1 Identify the source OpenSpec spec files for `<change-name>` and list the affected capabilities: `<capability-list>`.
- [ ] 1.2 Map each capability to an existing root-level `features/*.feature` file or a new root-level `features/<feature-name>.feature` file.
- [ ] 1.3 Derive or update the root-level feature files from the spec markdown: `<feature-file-list>`.
- [ ] 1.4 Ensure the root-level `acceptance-tests/` Node project ignores `node_modules/` in git and can run `gherkin-lint`.
- [ ] 1.5 Add or update the `acceptance-tests` package script `<gherkin-lint-script>` for `<feature-file-list>`.
- [ ] 1.6 Run `<gherkin-lint-script>` from `acceptance-tests/` and fix feature syntax until it reports zero errors.
- [ ] 1.7 Commit the feature extraction work to git before starting failing acceptance-test setup. Pause here if a commit cannot be made.

## 2. Failing Acceptance-Test Gate

- [ ] 2.1 Add or update Cucumber.js configuration at `<cucumber-config-path>`.
- [ ] 2.2 Add JavaScript lint tooling or scripts for `<step-definition-file-list>` and `<acceptance-helper-file-list>`, then run them.
- [ ] 2.3 Configure Cucumber.js to generate an HTML report at `<acceptance-html-report-path>`.
- [ ] 2.4 Add step definitions in `<step-definition-file-list>` for `<feature-file-list>`.
- [ ] 2.5 Add fixtures, helpers, or environment setup in `<acceptance-helper-file-list>` for `<capability-list>`.
- [ ] 2.6 Run the Gherkin acceptance test suite with HTML report output and confirm it fails for the expected unimplemented behaviour, not because of feature syntax, runner configuration, or missing test plumbing.
- [ ] 2.7 Commit the failing acceptance-test setup to git before implementing the application. Pause here if a commit cannot be made.

## 3. Granular Implementation Gate

- [ ] 3.1 Implement `<app-subsystem-1>` for `<capability-or-scenario>`.
- [ ] 3.2 Implement `<app-subsystem-2>` for `<capability-or-scenario>`.
- [ ] 3.3 Update `<persistence-config-adapter-ui-cli-or-docs-surface>` so observable behaviour matches the committed feature scenarios.
- [ ] 3.4 Add or update lower-level tests for `<subsystem-or-module-list>` where useful.
- [ ] 3.5 Ask how many acceptance-fix attempts to allow; if no limit is chosen, record `<acceptance-fix-attempt-limit>` as `3`.
- [ ] 3.6 Replace this placeholder with one checkbox per allowed `Acceptance attempt X/<acceptance-fix-attempt-limit>` using Cucumber.js and `<acceptance-html-report-path>`.
- [ ] 3.7 After failed attempts, fix implementation code without weakening committed feature files or acceptance tests.
- [ ] 3.8 If an early attempt passes, replace remaining unrun attempts with a completed "not needed" checkpoint naming the passing attempt.
- [ ] 3.9 If acceptance still fails after `<acceptance-fix-attempt-limit>` attempts, stop with an error saying there are still errors and include `<acceptance-html-report-path>`.
- [ ] 3.10 Commit the passing implementation to git before verification. Pause here if a commit cannot be made.

## 4. Verification Gate

- [ ] 4.1 Review changes since the failing acceptance-test checkpoint and confirm committed feature files and acceptance tests were not weakened to make implementation pass.
- [ ] 4.2 Review the final HTML acceptance report at `<acceptance-html-report-path>` and confirm it reflects the passing run.
- [ ] 4.3 Run `openspec validate <change-name> --type change --strict`.
- [ ] 4.4 Run the project test, lint, or build commands relevant to `<affected-subsystem-list>`.
- [ ] 4.5 If this change modifies files under `openspec/schemas/behaviour-driven/`, run `openspec schema validate behaviour-driven`.
