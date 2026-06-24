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

The current `behaviour-driven` workflow is too coarse after the failing acceptance gate: it tells contributors to implement until acceptance passes, but does not make scenario coverage, acceptance artifact stability, or slice-by-slice progress explicit.

## What Changes

- Refine feature extraction so existing `features/*.feature` files are patched semantically instead of overwritten or duplicated.
- Require committed failing acceptance coverage for all in-scope business scenarios before implementation begins.
- Freeze `features/` and `acceptance-tests/` during implementation unless OpenSpec artifacts are deliberately updated first.
- Drive implementation in scenario slices, measuring progress by business scenarios passing rather than by filled-in step definitions.
- Require every scenario slice to run the full acceptance suite, allowing only recorded not-yet-implemented scenarios to remain red.

## Capabilities

### New Capabilities

- None.

### Modified Capabilities

- `behaviour-driven-schema-workflow`: Refines the packaged behaviour-driven workflow around semantic feature-file merging, frozen acceptance coverage, scenario slices, and full-suite acceptance gates.

## Impact

- Updates behaviour expectations for `openspec/schemas/behaviour-driven/schema.yaml`.
- Updates packaged behaviour-driven documentation in `openspec/schemas/behaviour-driven/README.md`.
- Updates the behaviour-driven task template in `openspec/schemas/behaviour-driven/templates/tasks.md`.
- Updates canonical OpenSpec coverage in `openspec/specs/behaviour-driven-schema-workflow/spec.md` when archived.
