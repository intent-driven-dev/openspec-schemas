## ADDED Requirements

### Requirement: <!-- feature or business rule name -->
<!-- Optional Gherkin-style context, for example:
Feature: <capability>
Rule: <business rule>

Keep this markdown tight enough that downstream task generation can derive a
root-level `features/*.feature` file from it.
-->

#### Scenario: <!-- scenario name -->
- **GIVEN** <!-- starting context -->
- **WHEN** <!-- action or event -->
- **THEN** <!-- observable outcome -->

## MODIFIED Requirements

<!-- Copy the full existing requirement block from openspec/specs/<capability>/spec.md, then edit it so it represents the full desired behaviour after the change. The resulting markdown should remain suitable for translating into a root-level `features/*.feature` file. If a corresponding feature file already exists, update that file in place when the feature is extracted. -->

## REMOVED Requirements

### Requirement: <!-- removed feature or business rule name -->
**Reason**: <!-- why this behaviour is removed -->

**Migration**: <!-- how users or systems should adapt -->
