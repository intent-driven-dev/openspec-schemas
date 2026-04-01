---
name: openspec-bulk-apply-change
description: Use when multiple active OpenSpec changes should be applied concurrently in isolated worktrees with delegated verification and no merge.
---

# OpenSpec Bulk Apply

Apply multiple active OpenSpec changes by creating isolated worktrees, dispatching delegated apply flows in parallel subagents, running verification in each flow, and reporting back without merging.

## When to Use

- More than one active OpenSpec change exists
- `/opsx-apply` was invoked without an explicit change target
- The user wants multiple changes applied in parallel

Do not use this skill when the user explicitly targeted one change for `/opsx-apply`.

## Steps

1. **Get candidate changes**

   Run `openspec list --json` to get active changes.

   - If the command input included change names, limit analysis to those changes.
   - If fewer than 2 active candidate changes remain, do not use bulk mode. Fall back to normal single-change apply.

2. **Collect change context**

   For each candidate change:

   - Run `openspec status --change "<name>" --json`
   - Run `openspec instructions apply --change "<name>" --json`
   - Read listed `contextFiles`
   - Read the tasks artifact and summarize pending work
   - Note the implementation scope needed by the delegated apply flow

3. **Create isolated worktrees**

   For each candidate change:

   - Create a git worktree under `.worktrees/<change>`
   - Keep the parent agent out of direct implementation work in the main workspace

4. **Dispatch subagents in parallel**

   For each candidate change:

   - Dispatch one subagent in that change's worktree
   - Run all delegated apply flows in parallel
   - Do not apply any change directly in the parent agent

5. **Require apply then verify in each subagent**

   Instruct each subagent to:

   - run `/opsx-apply <change>`
   - run `/opsx-verify <change>` after apply work is complete
   - stop after verification
   - summarize implementation outcome, verification status, changed files, blockers, and unresolved warnings

6. **Collect and normalize reports**

   For each executed change, capture:

   - Worktree path
   - Apply status (`complete`, `paused`, `failed`)
   - Verify status (`ready`, `warnings`, `critical`, `failed`)
   - Files changed summary
   - Blockers or unresolved warnings

7. **Report back without merging**

   Present a final bulk-apply report:

   - Changes analyzed
   - Worktrees created
   - Apply result per change
   - `/opsx-verify` result per change
   - Which changes are ready for human review

   End with a clear statement that no merge was performed and that explicit user approval is required before any merge.

## Guardrails

- Do not auto-merge
- Do not auto-archive
- Do not bulk-apply when only one candidate change remains
- Do not perform apply work in the parent agent; use subagents only
- Do not run bulk apply in the main workspace; use isolated worktrees only
- Keep `.worktrees/` as the default worktree root unless the user specifies another location
- Require `/opsx-verify` in every delegated apply flow before reporting a change as review-ready
