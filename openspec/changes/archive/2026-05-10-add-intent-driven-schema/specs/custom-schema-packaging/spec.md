## MODIFIED Requirements

### Requirement: Repository root SHALL provide catalog and install guidance for humans and agents
The repository root SHALL include a `README.md` that explains the purpose of this schema collection, starts the main install section with an agent-oriented prompt that points to the raw root `README.md`, gives a self-install fallback for human readers, includes a dedicated agent-oriented install flow that removes ambiguity about prerequisites and copying the full schema folder, and lists only currently packaged schemas with canonical spec coverage.

#### Scenario: Human discovers schema options from repo root
- **WHEN** a human user opens the repository root `README.md`
- **THEN** they can find a self-install fallback that explains how to get the repository locally, where schema folders are copied, how a schema is activated in `openspec/config.yaml`, and how to validate the install

#### Scenario: Agent discovers deterministic install flow from repo root
- **WHEN** a coding agent opens the repository root `README.md`
- **THEN** it can find a top-level raw-README prompt handoff plus a dedicated agent-oriented install section that starts with prerequisite checks, explains the early-exit behavior, and tells it to clone the repo locally before copying the full schema directory recursively

#### Scenario: Human discovers the intent-driven schema from the root catalog
- **WHEN** a human user opens the repository root `README.md`
- **THEN** they can find `intent-driven` in the schema catalog
- **AND** they can find a reference to `openspec/schemas/intent-driven/README.md`.

#### Scenario: Agent can install the intent-driven schema from catalog guidance
- **WHEN** a coding agent follows the repository install guidance for `intent-driven`
- **THEN** it can copy the full `openspec/schemas/intent-driven/` folder into a target project's `openspec/schemas/intent-driven/`
- **AND** activate it with `schema: intent-driven`.

## ADDED Requirements

## REMOVED Requirements
