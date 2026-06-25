## 1. Create the standalone agent install guide

- [ ] 1.1 Create root `AGENT_INSTALL.md` containing the full install flow moved out of the README's "AI Agent Install Instructions" section.
- [ ] 1.2 Add a schema-selection step that enumerates all available schemas (by listing directories under `openspec/schemas/`), presents the list, and has the user pick exactly one schema to install and enable before any clone/copy/activation.
- [ ] 1.3 Handle the case where the user named a schema up front by confirming it matches one of the enumerated schemas before proceeding.
- [ ] 1.4 Keep the flow agent-agnostic and parameterize the schema name (no hard-coded `event-driven`-only steps beyond labelled examples).

## 2. Update the README

- [ ] 2.1 Simplify the "Install a Schema" trigger prompt to instruct the agent to read `AGENT_INSTALL.md` and follow the instructions, without inline steps or a required schema name.
- [ ] 2.2 Remove the embedded "AI Agent Install Instructions" section and replace it with a pointer to `AGENT_INSTALL.md`.
- [ ] 2.3 Ensure no install step remains duplicated between `README.md` and `AGENT_INSTALL.md`.

## 3. Verify and Wrap Up

- [ ] 3.1 Validate acceptance criteria from the delta specs (standalone guide exists, README points to it, enumerate-and-pick-exactly-one step present, trigger simplified).
- [ ] 3.2 Confirm all internal links and file references resolve.
- [ ] 3.3 Prepare concise reviewer notes. (No schema under `openspec/schemas/` changed, so `openspec schema review` is not required.)
