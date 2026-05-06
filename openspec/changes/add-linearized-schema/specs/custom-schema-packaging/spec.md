## ADDED Requirements

### Requirement: Repository root SHALL catalog the linearized schema
The repository root `README.md` SHALL list `linearized` as an available schema and point readers to its schema README.

#### Scenario: Human discovers the linearized schema from the root catalog
- **WHEN** a human user opens the repository root `README.md`
- **THEN** they can find `linearized` in the schema catalog
- **AND** they can find a reference to `openspec/schemas/linearized/README.md`.

#### Scenario: Agent can install the linearized schema from catalog guidance
- **WHEN** a coding agent follows the repository install guidance for `linearized`
- **THEN** it can copy the full `openspec/schemas/linearized/` folder into a target project's `openspec/schemas/linearized/`
- **AND** activate it with `schema: linearized`.
