## 1. Define Schema Packaging Structure

- [ ] 1.1 Create repository folder conventions for one-schema-per-folder packaging.
- [ ] 1.2 Add the `minimalist` schema folder with required core files (`schema.yaml`, templates, README).
- [ ] 1.3 Ensure schema folder layout is copy-installable into `openspec/schemas/<name>/` in any target project.

## 2. Implement Minimalist Workflow Schema

- [ ] 2.1 Define `minimalist` schema artifact flow so apply readiness depends on `tasks` built from `specs`.
- [ ] 2.2 Configure schema templates for delta specs and executable task lists aligned with lightweight changes.
- [ ] 2.3 Validate schema structure and template resolution with OpenSpec CLI schema validation commands.

## 3. Document Usage, Fit, and Agent Installation

- [ ] 3.1 Write schema README sections: purpose, good-fit examples, non-fit examples, and escalation guidance.
- [ ] 3.2 Add coding-agent install instructions to copy schema folder into local project `openspec/schemas/`.
- [ ] 3.3 Document activation step to set `schema: minimalist` in `openspec/config.yaml`.
- [ ] 3.4 Create repository-root `README.md` describing this schema collection and an agent quick start that points to each schema README.

## 4. Validate Schema Artifacts and Packaging

- [ ] 4.1 Run `openspec schema validate minimalist` and resolve all reported template/schema issues before marking the change complete.
- [ ] 4.2 Confirm template resolution paths for all `minimalist` artifacts with OpenSpec CLI.
- [ ] 4.3 Verify README install instructions match the final folder structure and activation flow.
