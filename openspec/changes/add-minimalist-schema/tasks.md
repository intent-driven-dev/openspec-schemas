## 1. Define Schema Packaging Structure

- [x] 1.1 Create repository folder conventions for one-schema-per-folder packaging.
- [x] 1.2 Add the `minimalist` schema folder with required core files (`schema.yaml`, templates, README).
- [x] 1.3 Ensure schema folder layout is copy-installable into `openspec/schemas/<name>/` in any target project.

## 2. Implement Minimalist Workflow Schema

- [x] 2.1 Define `minimalist` schema artifact flow so apply readiness depends on `tasks` built from `specs`.
- [x] 2.2 Configure schema templates for delta specs and executable task lists aligned with lightweight changes.
- [x] 2.3 Validate schema structure and template resolution with OpenSpec CLI schema validation commands.

## 3. Document Usage, Fit, and Agent Installation

- [x] 3.1 Write schema README sections: purpose and concise good-fit/non-fit guidance.
- [x] 3.2 Add a single-line coding-agent install command in root README with schema name as an argument.
- [x] 3.3 Document activation step to set `schema: minimalist` in `openspec/config.yaml`.
- [x] 3.4 Create repository-root `README.md` describing this schema collection and an agent quick start that points to each schema README.

## 4. Validate Schema Artifacts and Packaging

- [x] 4.1 Run `openspec schema validate minimalist` and resolve all reported template/schema issues before marking the change complete.
- [x] 4.2 Confirm template resolution paths for all `minimalist` artifacts with OpenSpec CLI.
- [x] 4.3 Verify README install instructions match the final folder structure and activation flow.
