## ADDED User Stories

### User Story: Standalone agent install guide
As a maintainer of this repository, I want the AI agent install instructions to live in a single standalone file shared by all agents, so that the README stays focused and the install flow has one authoritative source.

#### Acceptance Criteria
- **Given** the repository root
- **When** I look for agent install instructions
- **Then** an `AGENT_INSTALL.md` file at the repository root contains the full step-by-step install flow for any schema in this repository
- **And** the file is agent-agnostic (no instruction is tied to a specific coding agent)
- **And** the file name does not collide with the `AGENTS.md` convention used for general agent/project instructions

### User Story: Enumerate schemas and pick exactly one
As a user installing a schema via my coding agent, I want the agent to list every available schema and have me choose exactly one to install and enable, so that the correct single schema is installed even when I did not name one.

#### Acceptance Criteria
- **Given** an agent is following `AGENT_INSTALL.md`
- **When** the agent reaches the schema-selection step
- **Then** the flow instructs the agent to enumerate all available schemas by listing the directories under `openspec/schemas/` in this repository
- **And** the agent presents that list and asks the user to pick exactly one schema to install and enable
- **And** the agent proceeds with the clone/copy and activation steps only after the user has chosen exactly one schema
- **And** if the user named a schema up front, the agent confirms it matches one of the enumerated schemas before proceeding

## MODIFIED User Stories

### User Story: Trigger schema install from README
As a user, I want a short README instruction that simply points my agent at the install guide and tells it to follow the instructions, so that I do not have to paste detailed steps.

#### Acceptance Criteria
- **Given** the README "Install a Schema" section
- **When** I read the agent trigger prompt
- **Then** it instructs the agent to read `AGENT_INSTALL.md` and follow the instructions, without embedding the detailed install steps inline
- **And** the trigger does not require the user to name a schema in the prompt (the guide enumerates schemas and asks)

### User Story: README references the install guide
As a reader of the README, I want the previous "AI Agent Install Instructions" section replaced by a reference to `AGENT_INSTALL.md`, so that there is no duplicated or drifting copy of the flow.

#### Acceptance Criteria
- **Given** the README
- **When** I reach the agent install content
- **Then** the embedded step-by-step flow is removed and replaced by a pointer to `AGENT_INSTALL.md`
- **And** no install step is documented in two places

## Notes

This change touches only `README.md` and the new root `AGENT_INSTALL.md`; it does not modify any schema under `openspec/schemas/`, so no schema is affected and `openspec schema review` is not required for this change.
