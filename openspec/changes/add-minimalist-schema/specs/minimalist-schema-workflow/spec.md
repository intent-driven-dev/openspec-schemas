## ADDED Requirements

### Requirement: Minimalist schema SHALL define a specs-to-tasks workflow
The `minimalist` schema SHALL require `specs` and `tasks` artifacts for apply readiness and SHALL NOT require `proposal` or `design` artifacts.

#### Scenario: Apply readiness requires only tasks built from specs
- **WHEN** a change is created under the `minimalist` schema
- **THEN** artifact creation can proceed directly from `specs` to `tasks` without proposal and design stages

### Requirement: Minimalist schema SHALL communicate fit boundaries
The `minimalist` schema documentation SHALL define that it is intended for already well-scoped, INVEST-friendly, low-risk changes and SHALL include examples of good fit and non-fit.

#### Scenario: User evaluates whether to use minimalist
- **WHEN** a user reviews `minimalist` schema documentation before starting a change
- **THEN** they can identify from examples whether their change should use `minimalist` or a fuller schema

### Requirement: Minimalist workflow SHALL preserve delta-spec traceability
Changes created with `minimalist` SHALL capture requirement-level changes through delta `spec.md` files before task planning, so source-of-truth spec updates remain auditable.

#### Scenario: Requirement changes are captured before execution planning
- **WHEN** a team starts a `minimalist` change
- **THEN** they define delta requirements in specs before writing tasks for implementation
