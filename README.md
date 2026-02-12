# OpenSpec Schemas

Custom [OpenSpec](https://github.com/Fission-AI/OpenSpec) schemas packaged as copyable folders under `openspec/schemas/`.

Default OpenSpec includes the `spec-driven` schema, which is a strong general-purpose workflow. This repo adds more focused workflows for specific delivery contexts, and also demonstrates how to customise OpenSpec for different styles of work.

## Install a Schema

Copy the schema folder you want from `https://github.com/intent-driven-dev/openspec-schemas/openspec/schemas` into one of these locations:

1. Project Local:
Create `openspec/schemas/` in your project (if it does not exist), then copy your schema to `openspec/schemas/<schema-name>/`.

2. User Level:
Copy your schema to `$HOME/.openspec/schemas/<schema-name>/`.

Once the schema exists in either location, update `openspec/config.yaml` to activate it.

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

## Minimalist

Fast path from spec to execution using user-story requirements and Gherkin acceptance-criteria style.

For more details, see `openspec/schemas/minimalist/README.md`.

## Event-Driven

Structured workflow for event-centric systems with [Event Storming](https://en.wikipedia.org/wiki/Event_storming) discovery followed by [AsyncAPI](https://www.asyncapi.com/) specification.

For more details, see `openspec/schemas/event-driven/README.md`.
