## ADDED User Stories

### User Story: AI agents get deterministic schema install instructions from the root README
As an AI coding agent, I want a dedicated install section in the root `README.md`, so that I can install a schema into a project without inferring repository structure or missing nested files.

#### Acceptance Criteria
- **Given** I open the root `README.md`
- **When** I look for installation guidance intended for automated agents
- **Then** I find an `AI Agent Install Instructions` section near the top of the document.

- **Given** I am about to install a schema from this repository
- **When** I follow the AI-agent instructions
- **Then** the README first tells me to run `openspec --version` and verify that OpenSpec is installed and the CLI version is at least `1.0.0` before copying any schema files.

- **Given** OpenSpec is not installed, the installed version is lower than `1.0.0`, or `openspec/config.yaml` is not present in the target project
- **When** an agent prepares to install a schema
- **Then** the README instructs the agent to stop, ask the user to run `openspec --version`, install or upgrade OpenSpec as needed, complete `openspec init` first, and exit with a message that schema installation can only happen after `openspec init` has been run.

- **Given** I need a copy-paste installation path
- **When** I follow the AI-agent instructions
- **Then** the README provides one exact command sequence that copies an entire schema directory recursively, including `schema.yaml`, `README.md`, and nested files under `templates/`.

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
- **Then** it includes the prerequisite check `openspec --version` before the example install command so the agent can verify `openspec >= 1.0.0` and the prerequisite applies generally rather than only to one schema.

- **Given** the AI-agent section introduces the install workflow
- **When** an agent reads the instructions top-to-bottom
- **Then** the first operational step is the OpenSpec presence/version guardrail and early-exit behavior, before any schema fetch or copy command is shown.

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
- **Then** it adds an AI-agent-focused section that spells out the end-to-end flow: run `openspec --version` to confirm OpenSpec is installed and at least `1.0.0`, stop and ask the user to run `openspec init` first when that prerequisite is not met or `openspec/config.yaml` is missing, then copy the schema directory, set `schema: event-driven` for the example, and validate with `openspec schema validate`.

- **Given** the previous README could force readers to inspect repository layout or fetch files individually
- **When** the revised README is published
- **Then** the AI-agent section removes that ambiguity by explicitly telling readers to copy the full schema directory recursively instead of discovering nested files themselves.

- **Given** the AI-agent section shows expected validation output
- **When** an agent compares its results
- **Then** the example output includes `Validation Results:` and `✓ event-driven` as the success signal for the documented example flow.

## REMOVED User Stories
