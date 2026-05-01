## ADDED User Stories

### User Story: ADR artifact uses plain path instruction
As a schema maintainer, I want the `spec-driven-with-adr` schema to instruct ADR placement in plain text instead of using the artifact `folder` parameter, so that the schema keeps ADR persistence behavior explicit without relying on special folder routing metadata.

#### Acceptance Criteria
- **Given** the affected schema is `spec-driven-with-adr`
- **When** `openspec/schemas/spec-driven-with-adr/schema.yaml` defines the `adr` artifact
- **Then** the artifact definition MUST NOT include the `folder` parameter
- **And** the artifact instruction MUST strongly direct agents to create ADR files under the target repository's top-level `adr/` folder outside `openspec/`
- **And** the artifact instruction MUST state that ADR files are not written under `openspec/changes/<change>/`

#### Acceptance Criteria
- **Given** the affected schema is `spec-driven-with-adr`
- **When** implementation changes `openspec/schemas/spec-driven-with-adr/schema.yaml`
- **Then** `openspec schema validate spec-driven-with-adr` MUST pass before the change is considered complete

## MODIFIED User Stories

### User Story: ADR-enabled workflow records persistent decisions
As a contributor, I want the ADR step to preserve durable architectural decisions outside the OpenSpec change workspace, so that future changes can read current decisions from a stable repository-level ADR folder.

#### Acceptance Criteria
- **Given** a project activates `schema: spec-driven-with-adr`
- **When** the `adr` artifact is created
- **Then** the schema instructions MUST direct ADR files to `<repo>/adr/NNNN-kebab-title.md`
- **And** `<repo>/adr/` MUST mean a top-level folder beside `openspec/`, not a folder inside `openspec/`
- **And** accepted ADR immutability and supersession rules MUST remain intact

## REMOVED User Stories
