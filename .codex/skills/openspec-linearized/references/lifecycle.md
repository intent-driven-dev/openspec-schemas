# Linearized OpenSpec Lifecycle

This reference distills the `linearized` OpenSpec schema into skill behavior. Use it to coordinate proposal, apply, and archive lifecycle events while keeping Linear responsible for the business "what" and the repo responsible for the technical "how".

## Ownership Boundary

- Linear issue/card owns the business "what": business goal, business use cases, user/persona context, workflows, scope, acceptance criteria, and stakeholder-facing status. Keep the issue description synchronized from the business-facing content in `proposal.md`.
- Repo change artifacts own the technical "how": design decisions, architecture trade-offs, data models, migrations, implementation tasks, test plans, and code.
- `proposal.md` is a lightweight repo coordination artifact. It records Linear binding metadata, capability impact, and a concise repo-facing summary; use its business-facing sections to refresh the Linear issue description when those details change.
- `design.md` and `tasks.md` stay in the repo. Do not copy detailed technical design, architecture, task lists, or implementation notes into the Linear issue/card.
- Canonical specs live under `openspec/specs/`. After archive succeeds, mirror finalized canonical specs into Linear Project Documents so stakeholders can read them in Linear.
- Linear Project Documents are mirrors, not the canonical source. Replace them from repo canonical spec content at archive time.

## Config

Project-local Linear setup lives at `openspec/linear.yaml`.

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
  title_prefix: "OpenSpec:"
  documents:
    "<capability-name>":
      id: "<linear-document-id-or-slug>"
      url: "<linear-document-url>"
      title: "OpenSpec: <capability-name>"
```

If the file is missing during proposal work:

1. Verify Linear MCP connectivity when tools are available.
2. List only Linear setup data: teams with `list_teams`, projects with `list_projects`, and issue labels with `list_issue_labels`.
3. Ask one question at a time for the Linear team, then the Linear project, then the issue label filter.
4. Include an explicit "no label filter" option in the label question.
5. Never infer or auto-select team, project, or label from names, ordering, previous results, or seemingly obvious matches.
6. Write selected IDs and display names to `openspec/linear.yaml`.
7. Return to the configured Proposal Binding flow; list Linear issues only after `openspec/linear.yaml` exists and story selection is required.

If setup cannot verify Linear MCP, ask whether to continue locally without a story binding or pause until Linear is available. After setup exists, Linear failures are non-blocking.

## Project Config Policy

When a project will use archive-time Linear Project Document mirrors, ensure `openspec/config.yaml` contains equivalent archive policy guidance. If the project already uses `schema: linearized`, this policy may already be present. If the project uses another schema, keep that schema and add/update only the context block when the user agrees.

```yaml
context: |
  Linearized ownership and archive policy:
  - Linear issue/card is the source for business what: business goal, use cases, personas/workflows, scope, and acceptance criteria.
  - Repo artifacts are the source for technical how: design decisions, tasks, implementation details, migrations, tests, and code.
  - Keep proposal.md lightweight; sync its business-facing details into the Linear issue description when they change.
  - NON-NEGOTIABLE: OpenSpec canonical specs under `openspec/specs/` are the only source of truth.
  - Linear Project Documents are disposable mirrors only. Generic non-document Linear project resources are out of scope.
  - Run Linear Project Document sync only after OpenSpec archive succeeds and merges delta specs into canonical spec files.
  - Mirror documents use deterministic titles: `OpenSpec: <capability-name>`.
  - Available Linear tools create project-scoped documents, not folders. Use the `OpenSpec:` title namespace as the controlled replacement boundary.
  - Because these documents are mirrors, archive-time agents may replace the full document body with canonical OpenSpec spec content.
  - Do not transition the bound Linear story to Done before OpenSpec archive succeeds.
```

## Proposal Binding

Proposal frontmatter should include these fields:

```yaml
---
linear_story_id:
linear_story_identifier:
linear_story_title:
linear_story_url:
linear_story_state:
linear_team:
linear_project:
---
```

Selection flow:

1. Load `openspec/linear.yaml`.
2. Query Linear Backlog issues for the configured team and project. Apply `issue_label_filter.name` only to candidate selection.
3. If the user gave a specific Linear identifier, retrieve/use that story when it matches the configured context.
4. Otherwise, present the candidate list and let the contributor choose.
5. Read available title, description, labels, comments, links, and related context.
6. Treat the story as the business brief. It may still be incomplete, but new or corrected business facts should be written back to the Linear issue/card when possible.
7. Ask clarifying questions covering:
   - business goal and business cases
   - target users, personas, and workflows
   - in-scope and out-of-scope behavior
   - acceptance criteria and affected OpenSpec capabilities
   - architecture constraints and preferred approach, for repo design only
   - tech stack constraints and integration points, for repo design only
   - risks, migrations, rollout constraints, and non-goals
8. Before finishing proposal setup, update the Linear issue description with confirmed business details from `proposal.md` when possible. Keep technical decisions in repo artifacts.
9. Transition the selected issue to Todo when possible.
10. Add a Linear comment of at most two sentences saying OpenSpec proposal discovery started and the story was linked.

Do not infer architecture, tech stack, acceptance criteria, or affected capabilities solely from the Linear story unless the story explicitly states them and the contributor confirms they are current.

## OpenSpec Artifacts

Artifact order remains:

```text
proposal -> specs -> design -> tasks
```

Proposal:
- Keep it lightweight and repo-facing. Record Linear binding metadata, affected capabilities, and a concise summary needed to coordinate OpenSpec artifacts.
- Use the business-facing sections in `proposal.md` to refresh the bound Linear issue description when possible.
- If proposal discovery creates or changes business details, update Linear when possible instead of expanding `proposal.md` into a long-form business brief.
- Description sync must exclude frontmatter, Linear metadata, detailed technical design, task lists, and implementation notes.
- Include New Capabilities and Modified Capabilities so specs can be generated correctly.
- Research `openspec/specs/` before listing modified capabilities.

Specs:
- Create one delta spec per capability listed in the proposal.
- Use `## ADDED Requirements`, `## MODIFIED Requirements`, `## REMOVED Requirements`, or `## RENAMED Requirements`.
- Each requirement uses `### Requirement: <name>`.
- Each scenario must use exactly `#### Scenario: <name>`.
- Every requirement must include at least one scenario.
- For modified requirements, copy the entire existing requirement block before editing it.

Design:
- Create only when the change is cross-cutting, introduces a meaningful architecture or data model decision, adds an external dependency, has security/performance/migration complexity, or contains ambiguity that benefits from decisions before coding.
- Include context, goals/non-goals, decisions with alternatives, risks/trade-offs, migration plan when applicable, and open questions.
- Keep design content in the repo. Linear comments may mention that design exists or was updated, but should not duplicate the detailed design.

Tasks:
- Use checkboxes exactly: `- [ ] X.Y Task description`.
- Keep tasks small, dependency ordered, and directly verifiable.
- Include relevant tests and `openspec validate <change> --strict`.
- If the change modifies `openspec/schemas/linearized/`, include `openspec schema validate linearized`.
- Do not add post-archive Linear Project Document sync checkboxes.

## Apply Hook

Before implementation:

1. Read `openspec/changes/<change>/proposal.md` frontmatter.
2. If `linear_story_id` is present and Linear MCP is available, sync confirmed business/context changes from `proposal.md` to the issue description when possible.
3. If the issue is in Todo, transition it to In Progress when possible.
4. Add a Linear comment of at most two sentences saying implementation began from the OpenSpec change and tracked tasks are being applied.

Then follow the normal OpenSpec apply workflow:

- Read context files from `openspec instructions apply --change "<change>" --json`.
- Work through pending tasks in `tasks.md`.
- Mark each checkbox complete immediately after the task is done.
- Pause for blockers, unclear requirements, or design issues.

Never transition the story to Done during apply.
Do not copy `design.md` or `tasks.md` into Linear during apply; Linear should show status and business context, while repo artifacts carry implementation detail.

## Archive Hook

Archive order is strict:

1. Complete normal OpenSpec archive readiness checks.
2. Sync delta specs into canonical specs when the user chooses to sync.
3. Archive the change.
4. Only after archive succeeds, mirror canonical specs to Linear Project Documents.
5. Transition the Linear story to Done when possible.

Recommended document upsert:

1. For each affected capability, read canonical `openspec/specs/<capability>/spec.md`.
2. Use stored document ID or slug from `openspec/linear.yaml` if available.
3. Otherwise list/search project documents for title `OpenSpec: <capability-name>`.
4. If found, update that document.
5. If not found, create a project-scoped document with that deterministic title.
6. Persist document ID, URL, and title back to `openspec/linear.yaml` when possible.

Only Linear Project Documents are in scope. The documents are disposable mirrors, so replacing the full body with canonical spec content is acceptable.

## Linear Tool Mapping

Use the available Linear MCP tools by capability:

- Setup: `list_teams`, `list_projects`, `list_issue_labels`
- Story selection: `list_issues`
- Story context: `list_comments`; use issue fields returned by `list_issues`
- State updates: `save_issue` with `id` and `state`
- Proposal/apply/archive comments: `save_comment` with `issueId`
- Document lookup: `list_documents`
- Document create/update: `save_document`

Use names or IDs accepted by the tool. Prefer IDs when already stored in `openspec/linear.yaml`.
