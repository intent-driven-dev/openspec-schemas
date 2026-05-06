---
linear_story_id:
linear_story_identifier:
linear_story_title:
linear_story_url:
linear_story_state:
linear_team:
linear_project:
---

## Why

<!-- Explain the motivation for this change. What problem does this solve? Why now? -->

## What Changes

<!-- Describe what will change. Be specific about new capabilities, modifications, or removals. -->

## Capabilities

### New Capabilities
<!-- Capabilities being introduced. Replace <name> with kebab-case identifier (e.g., user-auth, data-export, api-rate-limiting). Each creates specs/<name>/spec.md -->
- `<name>`: <brief description of what this capability covers>

### Modified Capabilities
<!-- Existing capabilities whose REQUIREMENTS are changing (not just implementation).
     Only list here if spec-level behavior changes. Each needs a delta spec file.
     Use existing spec names from openspec/specs/. Leave empty if no requirement changes. -->
- `<existing-name>`: <what requirement is changing>

## Impact

<!-- Affected code, APIs, dependencies, systems -->

## Linear Archive Guidance

<!-- Schema-provided guidance. Preserve this section unless the linearized schema itself changes. -->

OpenSpec canonical specs under `openspec/specs/` are the source of truth. Linear Project Documents are mirrors only, and generic non-document Linear project resources are out of scope.

When this proposal is archived, run Linear Project Document sync only after OpenSpec archive succeeds and merges delta specs into canonical spec files. Use a stored document ID or slug from `openspec/linear.yaml` first; otherwise match an existing project document by deterministic title `OpenSpec: <capability-name>`; otherwise create a project-scoped document and persist its ID back to `openspec/linear.yaml` when possible.

After successful OpenSpec archive and best-effort document sync, transition the bound Linear story to Done when possible and add a Linear comment in at most two sentences summarizing that archive completed and canonical specs or mirrors were handled. Do not transition the story to Done before OpenSpec archive succeeds.
