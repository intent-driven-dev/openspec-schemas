## ADDED User Stories

### User Story: New schema-authoring skill uses schema init/fork
As a maintainer, I want a repository skill that guides contributors through creating new OpenSpec schemas using `openspec schema init` and `openspec schema fork`, so that schema proposals follow a consistent, low-friction workflow.

#### Acceptance Criteria
- **Given** I want to create a brand-new workflow schema
- **When** I follow the skill
- **Then** it instructs me to run `openspec schema init <schema-name>` (and documents the key flags like `--description`, `--artifacts`, and `--default/--no-default`).

- **Given** I want to customize an existing workflow
- **When** I follow the skill
- **Then** it instructs me to run `openspec schema fork <source> [name]` and explains what the copied schema folder contains (e.g., `schema.yaml` + `templates/`).

- **Given** I am authoring a schema in this repository
- **When** I follow the skill
- **Then** it sets the expectation that the schema lives under `openspec/schemas/<schema-name>/` and is packaged as a copyable folder.

### User Story: New schema-authoring skill covers validation and quality gates
As a contributor, I want the skill to tell me how to validate my schema locally, so that I can catch structural/template errors before opening a PR.

#### Acceptance Criteria
- **Given** I have created or modified `openspec/schemas/<schema-name>/schema.yaml` and/or templates
- **When** I finish my edits
- **Then** the skill includes a post-change verification step that runs schema validation for each affected schema name (e.g., `openspec schema validate <schema-name>`; if guidance references `openspec schema review`, it calls out that some CLI versions only provide `openspec schema validate`).

### User Story: CONTRIBUTING.md teaches schema creation and PR workflow
As an external contributor, I want a single CONTRIBUTING guide for creating and contributing new schemas, so that I can submit a high-quality PR without prior repo context.

#### Acceptance Criteria
- **Given** I am new to this repo
- **When** I read `CONTRIBUTING.md`
- **Then** it explains prerequisites (OpenSpec CLI installed), where schemas live (`openspec/schemas/<schema-name>/`), and how schemas are activated in a project (`openspec/config.yaml`).

- **Given** I want to start from scratch
- **When** I follow `CONTRIBUTING.md`
- **Then** it shows `openspec schema init <schema-name>` and the expected file layout (`schema.yaml` and `templates/`).

- **Given** I want to base my schema on an existing workflow
- **When** I follow `CONTRIBUTING.md`
- **Then** it shows `openspec schema fork <source> [name]` and how to pick a source (e.g., `spec-driven`, `tdd`, or a schema already in this repo).

- **Given** I am using OpenCode (and its skill system)
- **When** I follow `CONTRIBUTING.md`
- **Then** it points me at the repo's schema-authoring skill as the preferred guided workflow.

- **Given** I am using a different tool (no OpenCode skill integration)
- **When** I follow `CONTRIBUTING.md`
- **Then** it includes the raw, copy-pastable commands for `openspec schema init <schema-name>` and `openspec schema fork <source> [name]` without requiring any tool-specific skill.

- **Given** I am ready to validate my contribution
- **When** I follow `CONTRIBUTING.md`
- **Then** it includes a verification section that runs `openspec schema validate <schema-name>` for each schema changed under `openspec/schemas/`.

- **Given** I want to submit my work
- **When** I follow `CONTRIBUTING.md`
- **Then** it gives a short PR checklist (schema validates, templates exist for each artifact, README added/updated for the schema, and verification commands included).

## MODIFIED User Stories

### User Story: Update existing schema authoring guidance to prefer init/fork
As a maintainer, I want the existing schema authoring guide skill to prefer `openspec schema init`/`fork` over manual copying, so that the guidance matches the current experimental CLI workflow.

#### Acceptance Criteria
- **Given** the repository already contains schema authoring guidance in a skill
- **When** the guidance is updated
- **Then** it documents `openspec schema init` and `openspec schema fork` as first-class entry points for schema creation/customization.

## REMOVED User Stories
