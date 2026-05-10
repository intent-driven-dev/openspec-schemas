## Why

Teams using OpenSpec alongside Linear need a project-local workflow schema that can start from a Linear story, carry that story through proposal/spec/task/apply/archive phases, and update Linear best-effort without requiring changes to OpenSpec itself.

The schema should be packaged as `linearized` so consumer projects can copy one folder into `openspec/schemas/linearized/`, opt changes into the workflow, and keep Linear integration as agent instructions rather than OpenSpec CLI behavior.

## What Changes

- Add a self-contained `linearized` schema under `openspec/schemas/linearized/` by forking `spec-driven` and then updating schema YAML, templates, and README documentation where the Linearized workflow differs.
- Define a Linear-guided proposal flow:
  - first-time setup happens immediately when `openspec/linear.yaml` is missing, verifies Linear MCP connectivity, prompts for team and project, and writes `openspec/linear.yaml`;
  - setup may optionally persist a Linear issue label filter so backlog selection only includes issues for the configured project context;
  - subsequent changes load `openspec/linear.yaml` silently;
  - after first-time setup, the next user-facing question is which configured-project Backlog issue to pick;
  - proposal creation selects a Backlog story, transitions it to Todo, and records `linear_story_id` in proposal frontmatter.
- Define best-effort Linear behavior after first-time setup:
  - if Linear MCP is unavailable after `openspec/linear.yaml` exists, Linear updates are skipped silently and OpenSpec continues;
  - apply reads `linear_story_id`, syncs proposal content to the Linear story when possible, transitions Todo to In Progress when possible, then works tasks;
  - lifecycle transitions add short Linear comments when possible;
  - the Linear story moves to Done only after successful OpenSpec archive.
- Remove the earlier Epic-based synchronization idea from scope. Linear issues track work; OpenSpec archive remains responsible for merging specs into canonical project specs.
- Define Linear Project Document sync as an optional archive-time behavior:
  - OpenSpec's canonical project specs remain the source of truth;
  - installation guidance adds non-negotiable archive sync policy to `openspec/config.yaml`;
  - when Linear MCP is available, archive may create or update project-scoped Linear documents under project resources from those canonical specs;
  - document mirrors use deterministic `OpenSpec: <capability-name>` titles because available Linear tools do not create project document folders;
  - when Linear MCP is unavailable, archive remains local OpenSpec-only and skips document sync silently.
- Add templates for `proposal.md`, `spec.md`, `design.md`, and `tasks.md`, including frontmatter slots needed by the workflow.
- Document installation, opt-in, `openspec/linear.yaml`, frontmatter contracts, optional label filtering, graceful degradation, and optional Project Document sync.

## Capabilities

### New Capabilities

- `linearized-schema-workflow`: Defines the `linearized` OpenSpec schema package, artifact order, Linear setup/story/apply/archive instructions, optional label filtering, templates, README guidance, and validation expectations.

### Modified Capabilities

- `custom-schema-packaging`: Add `linearized` to the packaged schema catalog and ensure the schema follows this repository's self-contained custom schema conventions.

## Impact

- Adds files under `openspec/schemas/linearized/`.
- Updates repository catalog/install documentation only as needed to expose the new schema.
- Does not modify OpenSpec CLI, schema parser, workflow resolver, or files outside the schema package except repository documentation required to list the schema.
- Verification should include `openspec schema validate linearized` and smoke checks for `openspec new change <name> --schema linearized`, proposal/apply/tasks instructions, template loading, path portability, setup-language uniqueness, and Linear-disabled fallback language.

## Resolved Questions

- Can Linear MCP create or update Linear Project Documents / Resources?
  - Verified: Linear MCP can create and update project-scoped documents that appear under project resources.
  - Verified operations: `save_document` can update an existing project document resource and create a new document under a project.
  - Scope decision: OpenSpec canonical project specs remain the source of truth. Archive-time sync may mirror those specs into Linear Project Documents when Linear MCP is available.
  - Generic non-document project resource create/update operations are not exposed by the available Linear MCP tools, so this schema only targets Linear Project Documents.
