## 1. Fork Baseline Schema

- [x] 1.1 Run `openspec schema fork spec-driven linearized` to create `openspec/schemas/linearized/` from the built-in `spec-driven` schema.
- [x] 1.2 Inspect the forked `schema.yaml` and templates to confirm proposal, specs, design, tasks, and apply tracking match the baseline `spec-driven` workflow.
- [x] 1.3 Rename schema metadata to `linearized` and keep the schema package self-contained under `openspec/schemas/linearized/`.
- [x] 1.4 Commit the baseline fork and metadata rename.

## 2. Add Linear Setup And Proposal Flow

- [x] 2.1 Update the proposal artifact instructions to load `openspec/linear.yaml` when present and run first-time Linear setup when missing.
- [x] 2.2 Define the `openspec/linear.yaml` contract with Linear team, project, optional issue label filter, and archive document mapping fields.
- [x] 2.3 Update the proposal template with frontmatter slots for `linear_story_id` and useful Linear display metadata.
- [x] 2.4 Add proposal instructions for selecting a configured-project Backlog issue, transitioning it to Todo when possible, and recording `linear_story_id`.
- [x] 2.5 Add graceful-degradation language so proposal creation continues locally when Linear MCP is unavailable after setup exists.
- [x] 2.6 Commit the Linear setup and proposal-flow changes.

## 3. Add Apply And Task Guidance

- [x] 3.1 Update `apply.instruction` to read `linear_story_id`, sync proposal content to the Linear story when possible, transition Todo to In Progress when possible, and continue through `tasks.md`.
- [x] 3.2 Keep `apply.requires` and `apply.tracks: tasks.md` aligned with the forked `spec-driven` baseline.
- [x] 3.3 Update task artifact instructions to require small dependency-ordered checkbox tasks and a final verification/archive-readiness group.
- [x] 3.4 Update the tasks template so generated task lists include best-effort Linear story completion before archive.
- [x] 3.5 Ensure Linear update failures are documented as non-blocking for apply and task completion.
- [x] 3.6 Commit the apply and task-guidance changes.

## 4. Add Archive-Time Project Document Sync Guidance

- [x] 4.1 Document that OpenSpec canonical specs under `openspec/specs/` remain the source of truth and Linear Project Documents are mirrors.
- [x] 4.2 Add README and task guidance for running Project Document sync only after OpenSpec archive merges delta specs into canonical specs.
- [x] 4.3 Define the document upsert sequence: use stored document ID or slug from `openspec/linear.yaml`, otherwise match by deterministic title, otherwise create a project-scoped document.
- [x] 4.4 Persist newly discovered or created Linear document IDs back into `openspec/linear.yaml` when possible.
- [x] 4.5 Keep generic non-document Linear project resources explicitly out of scope.
- [x] 4.6 Commit the archive-time Project Document sync guidance.

## 5. Add Documentation And Catalog Entries

- [x] 5.1 Create `openspec/schemas/linearized/README.md` with purpose, suitable and unsuitable use cases, install and activation guidance, workflow sequence, Linear setup, graceful degradation, and archive document sync behavior.
- [x] 5.2 Update the repository root `README.md` to list `linearized` in the schema catalog and point to `openspec/schemas/linearized/README.md`.
- [x] 5.3 Ensure README examples use `openspec/linear.yaml`, `schema: linearized`, and `openspec schema validate linearized` consistently.
- [x] 5.4 Commit the documentation and catalog updates.

## 6. Verify Schema And Smoke Behavior

- [x] 6.1 Run `openspec schema validate linearized` and fix any schema or template issues.
- [x] 6.2 Smoke check `openspec new change <name> --schema linearized` creates the expected first artifact instructions.
- [x] 6.3 Smoke check proposal, apply, and tasks instructions mention Linear setup, `linear_story_id`, best-effort Linear updates, and Linear-disabled fallback behavior.
- [x] 6.4 Smoke check archive guidance mentions post-archive canonical spec mirroring to Linear Project Documents and does not imply generic resource sync.
- [x] 6.5 Run `openspec validate add-linearized-schema --strict` after implementation changes.
- [x] 6.6 Commit final verification fixes, if any.

## 7. Treat Linear Story As Proposal Input

- [x] 7.1 Add requirement coverage that selected Linear story contents seed proposal discovery and require user clarification.
- [x] 7.2 Update proposal instructions to read story content and ask about business cases, scope, architecture, tech stack, constraints, integrations, risks, acceptance criteria, and affected capabilities.
- [x] 7.3 Document in the schema README that Linear stories are discovery input, not complete OpenSpec proposals.
- [x] 7.4 Re-run schema validation, instruction smoke checks, and strict change validation.

## 8. Move Archive Sync Out Of Tasks And Tighten Linear Lifecycle

- [x] 8.1 Remove post-archive Linear Project Document sync checkboxes from generated task instructions and template.
- [x] 8.2 Add preserved Linear archive guidance to the proposal template.
- [x] 8.3 Update proposal, apply, and archive guidance so Linear comments are at most two sentences at each transition.
- [x] 8.4 Ensure Linear stories move to Done only after successful OpenSpec archive.
- [x] 8.5 Update schema README and delta specs for proposal-carried archive guidance and task verification compatibility.
- [x] 8.6 Update proposal and design artifacts to remove stale task-based archive sync guidance.

## 9. Immediate Linear Setup And Stronger Spec Mirror Guidance

- [x] 9.1 Require immediate Linear setup when `openspec/linear.yaml` is missing before story selection or proposal discovery.
- [x] 9.2 Make the next user-facing question after setup be which configured-project Backlog issue to pick.
- [x] 9.3 Strengthen proposal archive guidance as non-negotiable schema-provided content.
- [x] 9.4 Document that available Linear tools create project-scoped documents but do not expose project document folders.
- [x] 9.5 Use deterministic `OpenSpec: <capability-name>` document titles as the controlled replacement boundary.

## 10. Move Archive Policy To Config

- [x] 10.1 Remove archive mirror policy from the proposal template.
- [x] 10.2 Add non-negotiable Linear archive policy to schema install `config.yaml` guidance.
- [x] 10.3 Change mirror document title convention to `OpenSpec: <capability-name>`.
- [x] 10.4 Update change artifacts to describe config-carried archive policy instead of proposal-carried archive policy.
