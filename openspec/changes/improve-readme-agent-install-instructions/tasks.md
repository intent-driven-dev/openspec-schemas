## 1. Implement the Change

- [ ] 1.1 Update the root `README.md` near the top to add an `AI Agent Install Instructions` section for schema installation.
- [ ] 1.2 Make the first AI-agent instruction a prerequisite check that runs `openspec --version` to confirm OpenSpec is installed and at least `1.0.0`, before any schema fetch or copy step.
- [ ] 1.3 Document the early-exit behavior: if `openspec --version` shows OpenSpec is missing, below `1.0.0`, or `openspec/config.yaml` is not present, the agent must ask the user to install or upgrade OpenSpec, run `openspec init`, and stop with a message that schema installation can only proceed after initialization.
- [ ] 1.4 Add one copy-paste install example that recursively copies the full `event-driven` schema directory, including `schema.yaml`, `README.md`, and nested `templates/` content, while keeping surrounding README text general to all schemas.
- [ ] 1.5 Document the example activation step in `openspec/config.yaml` with `schema: event-driven` and label it as an example rather than a repository-wide default.
- [ ] 1.6 Add the validation step `openspec schema validate` plus expected success output showing `Validation Results:` and `✓ event-driven`.

## 2. Verify and Wrap Up

- [ ] 2.1 Review the updated README to confirm the AI-agent section is easy to follow without inspecting repository layout or fetching files individually.
- [ ] 2.2 Confirm the final wording makes `openspec --version` the first prerequisite check before installation and tells the agent to verify `openspec >= 1.0.0` rather than leaving the check implicit.
- [ ] 2.3 Confirm the early-exit guidance explicitly tells the agent to stop and ask for `openspec init` first when the prerequisite is not met or `openspec/config.yaml` is missing.
- [ ] 2.4 Confirm the final wording keeps `event-driven` as an example install flow and does not imply the repository is specific to the event-driven schema.
- [ ] 2.5 Prepare concise reviewer notes summarizing the new AI-agent install flow, the OpenSpec prerequisite and early-exit behavior, and the reason for keeping the guidance schema-generic outside the example.
