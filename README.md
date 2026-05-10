# OpenSpec Schemas

Custom [OpenSpec](https://github.com/Fission-AI/OpenSpec) schemas packaged as copyable folders under `openspec/schemas/`.

Default OpenSpec includes the `spec-driven` schema, which is a strong general-purpose workflow. This repo adds more focused workflows for specific delivery contexts, and also demonstrates how to customise OpenSpec for different styles of work.

## Install a Schema

Ask your coding agent to read this file and install the schema you want:

```text
Read this file: https://raw.githubusercontent.com/intent-driven-dev/openspec-schemas/refs/heads/main/README.md and install schema <schema-name>.
```

Example:

```text
Read this file: https://raw.githubusercontent.com/intent-driven-dev/openspec-schemas/refs/heads/main/README.md and install schema event-driven.
```

If you prefer to install the schema yourself, clone this repository locally or otherwise download it locally, then copy the relevant schema folder from `openspec/schemas/` into one of these locations:

1. Project Local:
Create `openspec/schemas/` in your project if it does not exist, then copy your schema to `openspec/schemas/<schema-name>/`.

2. User Level:
Copy your schema to `$HOME/.openspec/schemas/<schema-name>/`.

Once the schema exists in either location, update `openspec/config.yaml` to activate it and run `openspec schema validate`.

`config.yaml` guidance:
- Set `schema: <schema-name>`.
- Ensure `rules` keys correspond to artifact IDs in your schema's `schema.yaml` (`artifacts[].id`).
- For example, when using `minimalist`, artifacts are `specs` and `tasks`, so use `rules.specs` and `rules.tasks`.

### Example: minimalist

```yaml
schema: minimalist

context: |
 Tech Stack:
  - Pure HTML5, CSS3, vanilla JavaScript
  - No build tools, package managers

rules:
  specs:
    - Note accessibility requirements (WCAG 2.1 AA)
  tasks:
    - Include responsiveness checks.
```

Artifact alignment source: `openspec/schemas/minimalist/schema.yaml` (`specs`, `tasks`).

## AI Agent Install Instructions

Use this flow when installing any schema from this repository into an existing OpenSpec project.

1. Run `openspec --version` before cloning or copying any schema files. Confirm OpenSpec is installed and the CLI version is at least `1.0.0`.
2. If `openspec --version` fails, reports a version below `1.0.0`, or `openspec/config.yaml` is missing in the target project, stop and ask the user to install or upgrade OpenSpec and run `openspec init` first. Exit with a message that schema installation can only proceed after initialization.
3. Clone this repository locally, then copy the full schema directory recursively so you keep `schema.yaml`, the schema `README.md`, and all nested `templates/` files together.
4. Update `openspec/config.yaml` to activate the installed schema.
5. Run `openspec schema validate` to confirm the copied schema loads correctly.

Example install flow using `event-driven`:

```bash
openspec --version

# Stop here if OpenSpec is missing, below 1.0.0, or openspec/config.yaml does not exist yet.
git clone https://github.com/intent-driven-dev/openspec-schemas.git /tmp/openspec-schemas
cp -R /tmp/openspec-schemas/openspec/schemas/event-driven ./your-project/openspec/schemas/event-driven
```

Example activation in `openspec/config.yaml`:

```yaml
schema: event-driven
```

This activation snippet is only an example for the `event-driven` install flow. Replace the schema name when installing a different schema from this repository.

Validate the installed schema:

```bash
openspec schema validate
```

Expected success output for this example:

```text
Validation Results:
✓ event-driven
```

## Contributing

See `CONTRIBUTING.md` for how to create/customize schemas using `openspec schema init` / `openspec schema fork`, and how to validate before opening a PR.

## Video

[![Watch on YouTube](https://img.youtube.com/vi/k01nbZfwB34/0.jpg)](https://www.youtube.com/watch?v=k01nbZfwB34)

## Minimalist

Fast path from spec to execution using user-story requirements and Gherkin acceptance-criteria style.

For more details, see `openspec/schemas/minimalist/README.md`.

## Event-Driven

Structured workflow for event-centric systems with [Event Storming](https://en.wikipedia.org/wiki/Event_storming) discovery followed by [AsyncAPI](https://www.asyncapi.com/) specification.

For more details, see `openspec/schemas/event-driven/README.md`.

## Behaviour-Driven

Proposal-led workflow for changes where observable behaviour should drive design
and implementation. Specs stay mergeable by OpenSpec as `spec.md` files, while
the requirement and scenario content uses Gherkin-style `GIVEN` / `WHEN` /
`THEN` steps.

Activation:

```yaml
schema: behaviour-driven
```

Validate:

```bash
openspec schema validate behaviour-driven
```

For more details, see `openspec/schemas/behaviour-driven/README.md`.

## Intent-Driven

Proposal-led workflow for changes that need observable behaviour, technical
design, durable Architecture Decision Records, and implementation tasks. Specs
stay mergeable by OpenSpec as `spec.md` files, while the requirement and
scenario content uses Gherkin-style `GIVEN` / `WHEN` / `THEN` steps.

Artifact order:

```text
proposal -> specs -> design -> adr -> tasks
```

Activation:

```yaml
schema: intent-driven
```

Validate:

```bash
openspec schema validate intent-driven
```

For more details, see `openspec/schemas/intent-driven/README.md`.

## Linearized

Spec-driven workflow for teams that coordinate work in Linear while keeping
OpenSpec specs as the source of truth. It starts changes from Linear stories,
stores project setup in `openspec/linear.yaml`, records `linear_story_id` in
proposal frontmatter, and mirrors canonical specs to Linear Project Documents
after archive when Linear MCP is available.

Activation:

```yaml
schema: linearized

context: |
  Linearized archive policy:
  - NON-NEGOTIABLE: OpenSpec canonical specs under `openspec/specs/` are the only source of truth.
  - Linear Project Documents are disposable mirrors only. Generic non-document Linear project resources are out of scope.
  - Run Linear Project Document sync only after OpenSpec archive succeeds and merges delta specs into canonical spec files.
  - Mirror documents use deterministic titles: `OpenSpec: <capability-name>`.
  - Available Linear tools create project-scoped documents, not folders. Use the `OpenSpec:` title namespace as the controlled replacement boundary.
  - Because these documents are mirrors, archive-time agents may replace the full document body with canonical OpenSpec spec content.
  - Do not transition the bound Linear story to Done before OpenSpec archive succeeds.
```

Validate:

```bash
openspec schema validate linearized
```

For more details, see `openspec/schemas/linearized/README.md`.

## Spec-Driven With ADR

Experimental proposal-to-tasks workflow for changes that also need durable
Architecture Decision Records persisted under the target repository's top-level
`adr/` folder.

Based on OpenSpec PR: https://github.com/Fission-AI/OpenSpec/pull/1020

For more details, see `openspec/schemas/spec-driven-with-adr/README.md`.
