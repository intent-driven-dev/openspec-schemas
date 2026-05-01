## 1. Implement the Change

- [x] 1.1 Restructure the root `README.md` so a general `Install a Schema` section appears near the top before any agent-specific instructions.
- [x] 1.2 Start the top-level install section with a copy-paste agent prompt block that points to the raw root `README.md` URL and uses the parameterized schema name placeholder `<schema-name>`.
- [x] 1.3 Add a second prompt block that shows the exact `event-driven` example before any manual install guidance.
- [x] 1.4 Document the human self-install fallback in the top-level install section: clone this repository locally or otherwise download it locally, then copy a schema into either `openspec/schemas/<schema-name>/` or `$HOME/.openspec/schemas/<schema-name>/`, activate it in `openspec/config.yaml`, and validate with `openspec schema validate`.
- [x] 1.5 Keep a separate `AI Agent Install Instructions` section that makes the first agent step a prerequisite check with `openspec --version` to confirm OpenSpec is installed and at least `1.0.0`, before any schema fetch or copy step.
- [x] 1.6 Update the detailed AI-agent install flow to prefer local repository clone before recursively copying the target schema folder.
- [x] 1.7 Document the early-exit behavior: if `openspec --version` shows OpenSpec is missing, below `1.0.0`, or `openspec/config.yaml` is not present in the target project, the agent must ask the user to install or upgrade OpenSpec, run `openspec init`, and stop with a message that schema installation can only proceed after initialization.
- [x] 1.8 Keep one copy-paste install example that clones the repository locally and recursively copies the full `event-driven` schema directory, including `schema.yaml`, `README.md`, and nested `templates/` content, while keeping surrounding README text general to all schemas.
- [x] 1.9 Document the example activation step in `openspec/config.yaml` with `schema: event-driven` and label it as an example rather than a repository-wide default.
- [x] 1.10 Keep the validation step `openspec schema validate` plus expected success output showing `Validation Results:` and `✓ event-driven`.
- [x] 1.11 Update the main OpenSpec spec for custom schema packaging so the repo-level requirement matches the new install-section structure: clone locally first, self-install fallback second, dedicated AI-agent flow below.

## 2. Verify and Wrap Up

- [x] 2.1 Review the updated README to confirm the first actionable content in the top-level install section is the agent prompt block and that the self-install fallback remains clear for human readers.
- [x] 2.2 Confirm the AI-agent section is still easy to follow without inspecting repository layout or fetching files individually, and that it now prefers local clone before copy.
- [x] 2.3 Confirm the final wording makes `openspec --version` the first prerequisite check inside the AI-agent section and tells the agent to verify `openspec >= 1.0.0` rather than leaving the check implicit.
- [x] 2.4 Confirm the early-exit guidance explicitly tells the agent to stop and ask for `openspec init` first when the prerequisite is not met or `openspec/config.yaml` is missing.
- [x] 2.5 Confirm the final wording keeps `event-driven` as an example install flow and does not imply the repository is specific to the event-driven schema.
- [x] 2.6 Prepare concise reviewer notes summarizing the clone-first install section, the OpenSpec prerequisite and early-exit behavior, and the reason for keeping manual self-install guidance as a fallback.
