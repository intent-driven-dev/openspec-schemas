## 1. Implement the Change

- [ ] 1.1 Update Mermaid diagrams in `openspec/schemas/event-driven/templates/event-storming.md` and `openspec/schemas/event-driven/templates/event-modeling.md` to use explicit style directives (`classDef`/class assignments) instead of renderer-default colors.
- [ ] 1.2 Implement event-storming-standard color semantics in those diagrams: Domain Event (orange), Command (blue), Actor/User (yellow), Policy/Automation (pink or violet family), Read Model/Projection (green).
- [ ] 1.3 Add or update template guidance in `openspec/schemas/event-driven/README.md` (or the relevant template files) with a clear legend documenting the standard baseline and any intentional schema-specific deviations.

## 2. Verify and Wrap Up

- [ ] 2.1 Validate that generated Mermaid snippets in event-storming and event-modeling artifacts include explicit class/style definitions and apply the expected concept-to-color mapping.
- [ ] 2.2 Run targeted checks for changed files and confirm formatting/content consistency.
- [ ] 2.3 Run `openspec schema review event-driven` and treat a successful result as required for completion.
- [ ] 2.4 Prepare concise reviewer notes summarizing affected schema (`event-driven`), files changed, and verification outcomes.
