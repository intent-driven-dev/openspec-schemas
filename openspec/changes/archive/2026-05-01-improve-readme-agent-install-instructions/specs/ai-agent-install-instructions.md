## ADDED User Stories

### User Story: Humans get clear schema install guidance from the root README
As a human user, I want the root `README.md` to show the basic install flow first, so that I can copy a schema into my OpenSpec setup without reading agent-specific instructions first.

#### Acceptance Criteria
- **Given** I open the root `README.md`
- **When** I look for installation guidance
- **Then** I first find a general `Install a Schema` section near the top of the document.

- **Given** I open the `Install a Schema` section
- **When** I look for the first actionable instruction
- **Then** it provides a copy-paste prompt block telling a coding agent to read the raw root `README.md` URL and install schema `<schema-name>`.

- **Given** I open the `Install a Schema` section
- **When** I look for a concrete example
- **Then** it includes a second prompt block using `event-driven` as the exact schema name.

- **Given** I want to install a schema manually instead of delegating to an agent
- **When** I follow the root README install section
- **Then** it tells me to clone this repository locally or otherwise download it locally, copy a schema folder into either `openspec/schemas/<schema-name>/` or `$HOME/.openspec/schemas/<schema-name>/`, then activate it in `openspec/config.yaml` and validate it with `openspec schema validate`.

### User Story: AI agents get deterministic schema install instructions from the root README
As an AI coding agent, I want a dedicated install section in the root `README.md`, so that I can install a schema into a project without inferring repository structure or missing nested files.

#### Acceptance Criteria
- **Given** I open the root `README.md`
- **When** I look for installation guidance intended for automated agents
- **Then** I find an `AI Agent Install Instructions` section after the general install section.

- **Given** I am about to install a schema from this repository
- **When** I follow the AI-agent instructions
- **Then** the README first tells me to run `openspec --version` and verify that OpenSpec is installed and the CLI version is at least `1.0.0` before cloning or copying any schema files.

- **Given** OpenSpec is not installed, the installed version is lower than `1.0.0`, or `openspec/config.yaml` is not present in the target project
- **When** an agent prepares to install a schema
- **Then** the README instructs the agent to stop, ask the user to run `openspec --version`, install or upgrade OpenSpec as needed, complete `openspec init` first, and exit with a message that schema installation can only happen after `openspec init` has been run.

- **Given** I need a copy-paste installation path
- **When** I follow the AI-agent instructions
- **Then** the README provides one exact command sequence that clones the repository locally and copies an entire schema directory recursively, including `schema.yaml`, `README.md`, and nested files under `templates/`.

- **Given** I need to activate the installed schema
- **When** I read the AI-agent instructions
- **Then** the README shows one exact `openspec/config.yaml` activation step and one exact validation step using `openspec schema validate`.

### User Story: README uses event-driven as an example, not as the only supported schema
As a maintainer, I want the AI-agent installation guidance to use `event-driven` as a concrete example without making the repository seem specific to that schema, so that the README stays generally correct for a multi-schema package.

#### Acceptance Criteria
- **Given** the README includes AI-agent installation guidance
- **When** it demonstrates a schema install flow
- **Then** it uses `event-driven` as an explicit example install target while still describing schemas in general terms elsewhere in the README.

- **Given** the README shows a concrete install flow
- **When** it introduces the `event-driven` example
- **Then** it includes the prerequisite check `openspec --version` before the example clone-and-copy command so the agent can verify `openspec >= 1.0.0` and the prerequisite applies generally rather than only to one schema.

- **Given** the AI-agent section introduces the install workflow
- **When** an agent reads that section top-to-bottom
- **Then** the first operational step in that section is the OpenSpec presence/version guardrail and early-exit behavior, before any schema fetch or copy command is shown.

- **Given** an agent reads the example activation step
- **When** it sees `schema: event-driven`
- **Then** the surrounding documentation makes clear that this value is the example for the demonstrated install flow rather than a repo-wide default.

- **Given** an agent wants to confirm installation succeeded
- **When** it follows the README example
- **Then** it is instructed to run `openspec schema validate` and compare the result against expected validation output for the example schema.

## MODIFIED User Stories

### User Story: Root README installation guidance is explicit enough for agents to execute
As a contributor, I want the root `README.md` installation section to be explicit about the install, activation, and verification flow, so that humans and AI agents can complete schema setup without guessing intermediate steps.

#### Acceptance Criteria
- **Given** the root README already explains that schemas are copied into `openspec/schemas/<schema-name>/`
- **When** the installation guidance is updated
- **Then** it presents an `Install a Schema` section that starts with agent prompt blocks, then a self-install fallback for human readers, and a separate AI-agent-focused section that spells out the end-to-end guarded flow: run `openspec --version` to confirm OpenSpec is installed and at least `1.0.0`, stop and ask the user to run `openspec init` first when that prerequisite is not met or `openspec/config.yaml` is missing, then clone the repo locally, copy the schema directory, set `schema: event-driven` for the example, and validate with `openspec schema validate`.

- **Given** the previous README could force readers to inspect repository layout or fetch files individually
- **When** the revised README is published
- **Then** the general install section gives an exact clone-and-copy agent prompt first, followed by manual clone/download-and-copy instructions for human readers, and the AI-agent section removes remaining ambiguity by explicitly telling agents to copy the full schema directory recursively instead of discovering nested files themselves.

- **Given** the AI-agent section shows expected validation output
- **When** an agent compares its results
- **Then** the example output includes `Validation Results:` and `✓ event-driven` as the success signal for the documented example flow.

## REMOVED User Stories
