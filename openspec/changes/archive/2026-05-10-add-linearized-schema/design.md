## Context

This repository packages reusable OpenSpec schemas as self-contained folders under `openspec/schemas/`. The `linearized` schema will add a project-local workflow for teams that manage delivery in Linear but want OpenSpec specs to remain the canonical source of truth.

The integration must live in schema instructions, templates, and documentation. It must not require OpenSpec CLI changes, schema parser changes, or workflow resolver changes. Linear behavior is therefore best-effort agent behavior: use Linear MCP tools when available, continue locally when they are not.

We verified the relevant Linear MCP behavior against the `Intent-Driven Dev` project:

- `get_project` with resources can list project resources.
- Project-scoped documents appear as resources.
- `save_document` can update an existing project document resource.
- `save_document` can create a new project-scoped document resource.
- Generic non-document project resource create/update operations are not exposed by the available tools.

## Goals / Non-Goals

**Goals:**

- Package `linearized` as a copyable schema folder with `schema.yaml`, templates, and README guidance.
- Guide agents from a Linear Backlog story into OpenSpec proposal, specs, design, tasks, apply, and archive.
- Persist project-local Linear setup in `openspec/linear.yaml` so later changes can run without repeated setup prompts.
- Store `linear_story_id` in proposal frontmatter so apply/tasks can update the correct Linear story.
- Keep OpenSpec canonical specs under `openspec/specs/` as the source of truth.
- Optionally mirror canonical specs into Linear Project Documents during archive when Linear MCP is available.
- Degrade silently after setup when Linear MCP is unavailable.

**Non-Goals:**

- Modify OpenSpec CLI behavior or add built-in Linear support.
- Treat Linear issues, projects, or documents as the source of truth for specs.
- Sync generic non-document Linear project resources.
- Implement a continuous bidirectional sync between OpenSpec and Linear.
- Reintroduce Epic-based synchronization.

## Decisions

### Decision: Fork `spec-driven` as the implementation baseline

Implementation will create `linearized` by running `openspec schema fork spec-driven linearized` and then editing the generated schema package.

Rationale: `linearized` keeps the standard proposal, specs, design, tasks, and apply shape. Forking `spec-driven` preserves the default OpenSpec artifact contracts, template structure, and apply tracking behavior while keeping the Linear-specific changes easy to review.

Alternatives considered:

- Author `schema.yaml` and templates from scratch: rejected because it increases drift from the built-in workflow that `linearized` intentionally extends.
- Fork a custom schema from this repository: rejected because `linearized` should be the Linear-enabled variant of the standard OpenSpec flow, not of a narrower workflow such as `minimalist` or `event-driven`.

### Decision: Keep Linear integration as schema-level agent instructions

The schema will describe Linear interactions in `schema.yaml`, artifact templates, and README docs. Agents execute those instructions using available MCP tools.

Rationale: this repository distributes schemas, not OpenSpec runtime extensions. Keeping the integration instruction-only preserves compatibility with standard OpenSpec installs and avoids changing the CLI.

Alternatives considered:

- Add Linear behavior to OpenSpec CLI: rejected because it is outside this repository's scope and would couple OpenSpec core to one tracker.
- Generate helper scripts: rejected for this change because MCP availability and tool names are environment-specific.

### Decision: Persist Linear setup in `openspec/linear.yaml`

First-time setup will run immediately when `openspec/linear.yaml` is missing, verify Linear MCP connectivity, ask for the Linear team and project, optionally ask for an issue label filter, and write `openspec/linear.yaml`. After setup is written, the next user-facing question should be which configured-project Backlog issue to pick.

The file should store stable identifiers and display names, for example:

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
      document_id: "<linear-document-id-or-slug>"
      title: "OpenSpec: <capability-name>"
```

Rationale: agents need deterministic context after the first setup, and document IDs created during archive sync need a project-local place to be remembered.

Alternatives considered:

- Store only names: rejected because names can change and are ambiguous.
- Store Linear state in proposal frontmatter only: rejected because team/project/document mapping is project configuration, not change-specific state.

### Decision: Use proposal frontmatter for change-specific Linear state

The proposal template will include frontmatter slots for `linear_story_id` and related display fields. Proposal creation selects a Linear Backlog issue for the configured project context, transitions it to Todo when possible, and records the selected story ID.

Rationale: apply and task completion need to target the same Linear story without searching again. Proposal frontmatter travels with the OpenSpec change and is the right place for change-specific metadata.

Alternatives considered:

- Search by title during apply: rejected because titles can drift and duplicate.
- Store selected story only in `openspec/linear.yaml`: rejected because multiple active changes may exist at once.

### Decision: Treat Linear issue updates as best-effort lifecycle mirrors

After setup exists, Linear updates should not block OpenSpec progress. The schema will use `apply.instruction` for apply-specific guidance: read `linear_story_id`, sync proposal content to the Linear story description when possible, transition Todo to In Progress when possible with a short comment, then work through tracked tasks.

The schema will still use the standard apply tracking contract:

```yaml
apply:
  requires:
    - tasks
  tracks: tasks.md
  instruction: |
    ...
```

The Linear story must not move to Done during apply or task completion. It moves to Done only after OpenSpec archive succeeds for the associated change, with a short comment summarizing archive completion.

Rationale: Linear should reflect delivery progress, but the OpenSpec workflow must remain usable offline or in environments without Linear MCP.

Alternatives considered:

- Fail the workflow when Linear updates fail: rejected because it makes local OpenSpec work depend on an external service.
- Skip lifecycle transitions entirely: rejected because the schema's purpose is to keep Linear reasonably current.

### Decision: Mirror canonical specs to Linear Project Documents at archive time

OpenSpec specs under `openspec/specs/` remain canonical. After archive merges delta specs into canonical specs, an agent may mirror changed canonical spec files into Linear Project Documents when Linear MCP is available.

OpenSpec schemas do not currently provide a first-class `archive` instruction section equivalent to `apply.instruction`. The archive sync contract will therefore be documented as non-negotiable `openspec/config.yaml` context/rules in installation guidance, rather than emitted as implementation task checkboxes that would affect apply verification or repeated in every proposal.

- the target project's `openspec/config.yaml`, which carries the durable archive policy for agents;
- the schema README, which documents the required config snippet and archive sequence for agents.

The archive sequence should be:

1. Complete implementation tasks.
2. Complete implementation and verification tasks without moving the Linear story to Done.
3. Run OpenSpec archive so delta specs merge into canonical `openspec/specs/`.
4. After successful archive, mirror changed canonical specs into Linear Project Documents when possible.
5. Transition the Linear story to Done when possible and add a short comment summarizing the archive outcome.

Document sync should use this upsert order:

1. If `openspec/linear.yaml` has a stored document ID or slug for the capability, update that document with `save_document`.
2. Otherwise, list or inspect project resources and look for an existing project document with the expected title.
3. If found, update it and persist its ID in `openspec/linear.yaml`.
4. If not found, create a new project-scoped document with `save_document` and persist its ID in `openspec/linear.yaml`.

The default title should be deterministic, such as `OpenSpec: <capability-name>`, so repeated archive syncs can find the same document even before the ID is persisted. The available Linear tools support creating project-scoped documents but do not expose project document folder creation, so the title namespace is the controlled replacement boundary.

Rationale: verified Linear MCP tools support project document resources. Mirroring canonical specs gives Linear users readable project resources while preserving OpenSpec as source of truth.

Alternatives considered:

- Sync delta specs before archive: rejected because delta specs are not canonical and may not contain the final merged requirement set.
- Make Linear Project Documents canonical: rejected because OpenSpec archive is responsible for maintaining the authoritative project specs.
- Sync all project resources: rejected because only document resources have create/update tool support.

### Decision: Keep optional label filtering narrow

Setup may persist a single Linear issue label filter for backlog selection. The filter narrows candidate issues for the configured project/team context but does not become a requirement for every Linear operation.

Rationale: labels are useful for selecting the right backlog, but overloading labels as a hard workflow invariant would make setup brittle.

Alternatives considered:

- Require a label filter: rejected because some Linear projects organize work without labels.
- Support complex filter expressions: rejected because this is schema guidance, not a query language.

## Risks / Trade-offs

- Linear MCP unavailable after setup -> Continue OpenSpec locally and skip Linear updates silently, as documented.
- Linear document renamed or moved -> Prefer stored document ID/slug over title matching; title matching is only a fallback.
- Archive sync runs before canonical specs are merged -> Document that spec mirroring must happen after archive updates `openspec/specs/`.
- Document sync overwrites manual Linear edits -> Make OpenSpec canonical and document the overwrite behavior; Linear documents are mirrors, not editable sources.
- Multiple active changes touch the same capability -> Last archive sync wins in Linear, while OpenSpec archive remains the source of truth.
- `openspec/linear.yaml` contains environment-specific IDs -> Keep it project-local and document that teams may choose whether to commit it.

## Migration Plan

1. Add `openspec/schemas/linearized/` with schema definition, templates, and README.
2. Update repository catalog documentation so users and agents can discover and install `linearized`.
3. Validate the schema with `openspec schema validate linearized`.
4. Smoke test a new change using `--schema linearized`.
5. Smoke test graceful degradation language by checking instructions still allow local progress when Linear MCP is unavailable.
6. Smoke test optional Project Document sync instructions against the verified Linear MCP operations where practical.

Rollback is deleting `openspec/schemas/linearized/` and removing the catalog entry. The change does not alter OpenSpec runtime behavior or existing schemas.

## Open Questions

None. Linear Project Document creation and update were verified through the available Linear MCP tools, and generic non-document resource sync is explicitly out of scope.
