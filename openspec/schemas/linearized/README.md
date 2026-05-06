# Linearized OpenSpec Schema

`linearized` is the standard OpenSpec proposal-to-tasks workflow with
best-effort Linear story mirroring. It is for teams that plan delivery in Linear
but keep OpenSpec specs as the source of truth.

Use it when:
- Linear issues represent implementation stories.
- OpenSpec proposals, specs, designs, and tasks should remain local files.
- Linear should reflect progress when MCP tools are available.
- Canonical OpenSpec specs should be mirrored into Linear Project Documents
  after archive.

Do not use it when:
- Linear must be the source of truth for specifications.
- You need bidirectional or continuous Linear synchronization.
- You need to create or update generic non-document Linear project resources.
- A simple local-only `spec-driven` workflow is enough.

## Install

Copy the full schema folder into a project or user schema location:

```bash
cp -R openspec/schemas/linearized <target-project>/openspec/schemas/linearized
```

Then activate it in `openspec/config.yaml`:

```yaml
schema: linearized
```

Validate the installed schema:

```bash
openspec schema validate linearized
```

## Workflow

Artifact order:

```text
proposal -> specs -> design -> tasks
```

Apply still uses the standard tracking contract:

```yaml
apply:
  requires:
    - tasks
  tracks: tasks.md
```

The difference from `spec-driven` is the Linear guidance embedded in proposal,
apply, task, and archive-readiness instructions.

## Linear Setup

The schema uses project-local configuration at `openspec/linear.yaml`.

Example:

```yaml
team:
  id: "<linear-team-id>"
  key: "<team-key>"
  name: "<team-name>"
project:
  id: "<linear-project-id>"
  name: "<project-name>"
issue_label_filter:
  name: "<optional-label-name>"
archive_documents:
  enabled: true
  documents:
    "<capability-name>":
      document_id: "<linear-document-id-or-slug>"
      title: "OpenSpec: <capability-name>"
```

When this file exists, agents load it silently. When it is missing, agents
should verify Linear MCP connectivity when possible, ask for the Linear team and
project, optionally ask for one issue label filter, and write the selected
configuration to `openspec/linear.yaml`.

After `openspec/linear.yaml` exists, Linear availability is non-blocking. If
Linear MCP is unavailable or a Linear update fails, agents continue the local
OpenSpec workflow and skip Linear updates silently.

## Proposal Binding

The proposal template includes frontmatter for change-specific Linear metadata:

```yaml
linear_story_id:
linear_story_identifier:
linear_story_title:
linear_story_url:
linear_story_state:
linear_team:
linear_project:
```

When Linear MCP is available, proposal creation should select a Backlog issue
for the configured team and project, apply the optional issue label filter to
candidate selection, transition the issue to Todo when possible, and record
`linear_story_id`. The agent should add a Linear comment in at most two
sentences summarizing that OpenSpec proposal discovery started and the story was
linked.

The selected Linear story is discovery input, not an already-complete OpenSpec
proposal. Agents should read available story title, description, labels,
comments, links, and related context, then ask the contributor proposal-style
clarifying questions before writing `proposal.md`. The questions should cover
business cases, target users, scope, architecture, tech stack, constraints,
integrations, risks, acceptance criteria, and affected capabilities.

## Apply Behavior

During apply, agents read `linear_story_id` from `proposal.md`. When Linear MCP
is available, they should sync useful proposal content to the Linear story and
transition Todo to In Progress when possible. The transition should include a
Linear comment in at most two sentences summarizing that implementation began
from the OpenSpec change and tracked tasks are being applied. These updates are
best-effort: implementation continues through `tasks.md` even when Linear is
unavailable.

Generated task lists should include small dependency-ordered checkboxes and a
final verification/archive-readiness group. They should not include
post-archive Linear Project Document sync checkboxes; archive-time sync guidance
lives in `proposal.md`. For schema changes, include:

```bash
openspec schema validate linearized
```

## Archive Document Sync

OpenSpec canonical specs under `openspec/specs/` are the source of truth. Linear
Project Documents are mirrors.

The proposal template includes a preserved Linear Archive Guidance section.
Archive-time agents should use that section when a proposal is being archived.
Run document sync only after OpenSpec archive succeeds and merges delta specs
into canonical spec files. The recommended upsert sequence is:

1. Use a stored document ID or slug from `openspec/linear.yaml`.
2. Otherwise, look for an existing project document with deterministic title
   `OpenSpec: <capability-name>`.
3. If found, update that document and persist its ID to `openspec/linear.yaml`
   when possible.
4. If not found, create a project-scoped document and persist its ID when
   possible.

Only Linear Project Documents are in scope. Generic non-document Linear project
resources are explicitly out of scope.

Do not transition the bound Linear story to Done during apply or task
completion. After successful OpenSpec archive and best-effort document sync,
transition the story to Done when possible and add a Linear comment in at most
two sentences summarizing that archive completed and canonical specs or mirrors
were handled.
