## MODIFIED User Stories

### User Story: Spec-driven schema with ADR support persists durable decisions as top-level ADRs
As a schema user, I want the `spec-driven-with-adr` ADR artifact to report its generated files under the repository-level ADR folder, so that OpenSpec does not consider ADR creation complete based on unrelated change files such as `proposal.md`.

#### Acceptance Criteria
- **Given** the affected schema is `spec-driven-with-adr`
- **When** `openspec/schemas/spec-driven-with-adr/schema.yaml` defines the `adr` artifact
- **Then** the artifact `generates` value MUST resolve to `<repo>/adr/*.md` from the change directory
- **And** the value MUST match the known-good relative path pattern `../../../adr/*.md`

#### Acceptance Criteria
- **Given** a project uses the `spec-driven-with-adr` schema
- **When** a change contains `proposal.md` but no generated ADR file under the repository-level `adr/` folder
- **Then** the `adr` artifact MUST NOT be considered complete
- **And** downstream task readiness MUST remain blocked until the ADR artifact completion check observes the intended ADR output location

#### Acceptance Criteria
- **Given** implementation changes files under `openspec/schemas/spec-driven-with-adr/`
- **When** the implementation is complete
- **Then** `openspec schema review spec-driven-with-adr` MUST pass before the change is considered complete
