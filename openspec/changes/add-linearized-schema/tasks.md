## 1. Fork Baseline Schema

- [ ] 1.1 Run `openspec schema fork spec-driven linearized` to create `openspec/schemas/linearized/` from the built-in `spec-driven` schema.
- [ ] 1.2 Inspect the forked `schema.yaml` and templates to confirm proposal, specs, design, tasks, and apply tracking match the baseline `spec-driven` workflow.
- [ ] 1.3 Rename schema metadata to `linearized` and keep the schema package self-contained under `openspec/schemas/linearized/`.
- [ ] 1.4 Commit the baseline fork and metadata rename.

## 2. Add Linear Setup And Proposal Flow

- [ ] 2.1 Update the proposal artifact instructions to load `openspec/linear.yaml` when present and run first-time Linear setup when missing.
- [ ] 2.2 Define the `openspec/linear.yaml` contract with Linear team, project, optional issue label filter, and archive document mapping fields.
- [ ] 2.3 Update the proposal template with frontmatter slots for `linear_story_id` and useful Linear display metadata.
- [ ] 2.4 Add proposal instructions for selecting a configured-project Backlog issue, transitioning it to Todo when possible, and recording `linear_story_id`.
- [ ] 2.5 Add graceful-degradation language so proposal creation continues locally when Linear MCP is unavailable after setup exists.
- [ ] 2.6 Commit the Linear setup and proposal-flow changes.

## 3. Add Apply And Task Guidance

- [ ] 3.1 Update `apply.instruction` to read `linear_story_id`, sync proposal content to the Linear story when possible, transition Todo to In Progress when possible, and continue through `tasks.md`.
- [ ] 3.2 Keep `apply.requires` and `apply.tracks: tasks.md` aligned with the forked `spec-driven` baseline.
- [ ] 3.3 Update task artifact instructions to require small dependency-ordered checkbox tasks and a final verification/archive-readiness group.
- [ ] 3.4 Update the tasks template so generated task lists include best-effort Linear story completion before archive.
- [ ] 3.5 Ensure Linear update failures are documented as non-blocking for apply and task completion.
- [ ] 3.6 Commit the apply and task-guidance changes.

## 4. Add Archive-Time Project Document Sync Guidance

- [ ] 4.1 Document that OpenSpec canonical specs under `openspec/specs/` remain the source of truth and Linear Project Documents are mirrors.
- [ ] 4.2 Add README and task guidance for running Project Document sync only after OpenSpec archive merges delta specs into canonical specs.
- [ ] 4.3 Define the document upsert sequence: use stored document ID or slug from `openspec/linear.yaml`, otherwise match by deterministic title, otherwise create a project-scoped document.
- [ ] 4.4 Persist newly discovered or created Linear document IDs back into `openspec/linear.yaml` when possible.
- [ ] 4.5 Keep generic non-document Linear project resources explicitly out of scope.
- [ ] 4.6 Commit the archive-time Project Document sync guidance.

## 5. Add Documentation And Catalog Entries

- [ ] 5.1 Create `openspec/schemas/linearized/README.md` with purpose, suitable and unsuitable use cases, install and activation guidance, workflow sequence, Linear setup, graceful degradation, and archive document sync behavior.
- [ ] 5.2 Update the repository root `README.md` to list `linearized` in the schema catalog and point to `openspec/schemas/linearized/README.md`.
- [ ] 5.3 Ensure README examples use `openspec/linear.yaml`, `schema: linearized`, and `openspec schema validate linearized` consistently.
- [ ] 5.4 Commit the documentation and catalog updates.

## 6. Verify Schema And Smoke Behavior

- [ ] 6.1 Run `openspec schema validate linearized` and fix any schema or template issues.
- [ ] 6.2 Smoke check `openspec new change <name> --schema linearized` creates the expected first artifact instructions.
- [ ] 6.3 Smoke check proposal, apply, and tasks instructions mention Linear setup, `linear_story_id`, best-effort Linear updates, and Linear-disabled fallback behavior.
- [ ] 6.4 Smoke check archive guidance mentions post-archive canonical spec mirroring to Linear Project Documents and does not imply generic resource sync.
- [ ] 6.5 Run `openspec validate add-linearized-schema --strict` after implementation changes.
- [ ] 6.6 Commit final verification fixes, if any.
