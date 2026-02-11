## 1. Implement the Change

- [ ] 1.1 Create a new skill package under `.codex/skills/` for OpenSpec schema understanding and custom schema authoring guidance.
- [ ] 1.2 Add skill documentation that explains schema anatomy (artifacts, dependencies, rules, outputs) using `spec-driven` as a worked example.
- [ ] 1.3 Include actionable guidance for drafting new custom schemas in this repo, including artifact sequence design and dependency mapping.
- [ ] 1.4 Wire the skill into repository-level discovery so it is available alongside existing OpenSpec skills.
- [ ] 1.5 Review upstream schemas in `https://github.com/Fission-AI/OpenSpec/tree/main/schemas` and capture a high-level comparison of each schema's artifact flow, dependencies, and intended use case.
- [ ] 1.6 Convert the upstream schema review into reusable guidance inside the skill so future custom schema creation in this repo starts from proven patterns.
- [ ] 1.7 Perform a deep read of upstream `spec-driven` schema at `https://github.com/Fission-AI/OpenSpec/tree/main/schemas/spec-driven` as the primary standard for schema structure, artifact semantics, and workflow behavior.
- [ ] 1.8 Use `openspec/schemas/minimalist/README.md` only as a local example of how to package and position a custom schema in this repository, without treating it as the canonical behavior reference.

## 2. Verify and Wrap Up

- [ ] 2.1 Validate the skill content against `openspec/changes/create-openspec-schema-understanding-skill/specs/schema-guidance/spec.md` scenarios.
- [ ] 2.2 Run targeted checks for changed files and ensure instructions are clear, accurate, and repository-specific.
- [ ] 2.3 If any files under `openspec/schemas/` are changed, run `openspec schema review <schema-name>` for each affected schema before marking complete.
- [ ] 2.4 Prepare concise reviewer notes summarizing the added skill and how to use it.
