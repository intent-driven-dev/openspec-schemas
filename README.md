# OpenSpec Custom Schemas

Custom [OpenSpec](https://github.com/Fission-AI/OpenSpec) schemas packaged as copyable folders under `openspec/schemas/`.

Default OpenSpec includes the `spec-driven` schema, which is a strong general-purpose workflow. This repo adds more focused workflows for specific delivery contexts, and also demonstrates how to customise OpenSpec for different styles of work.

Detailed write-up: [https://intent-driven.dev/blog/2026/02/12/openspec-custom-schemas/](https://intent-driven.dev/blog/2026/02/12/openspec-custom-schemas/)

## Video

[![Watch on YouTube](https://img.youtube.com/vi/k01nbZfwB34/0.jpg)](https://www.youtube.com/watch?v=k01nbZfwB34)

## Install a Schema

Ask your coding agent to read the install guide and follow the instructions:

```text
Read this file: https://raw.githubusercontent.com/intent-driven-dev/openspec-schemas/refs/heads/main/AGENT_INSTALL.md and follow the instructions.
```

If you already know which schema you want, include the name and the guide will confirm it exists before proceeding:

```text
Read this file: https://raw.githubusercontent.com/intent-driven-dev/openspec-schemas/refs/heads/main/AGENT_INSTALL.md and install schema intent-driven.
```

Otherwise the guide will enumerate all available schemas and ask you to pick one.

### Example: intent-driven `config.yaml`

```yaml
schema: intent-driven

context: |
  Tech Stack:
    - Node.js, TypeScript
    - PostgreSQL

rules:
  proposal:
    - Maximum of 250 words
  tasks:
    - Break tasks to logical commits.
```

Artifact alignment source: `openspec/schemas/intent-driven/schema.yaml` (`proposal`, `specs`, `design`, `adr`, `tasks`).

For the full step-by-step install flow, see [`AGENT_INSTALL.md`](./AGENT_INSTALL.md).

## Custom Schemas

### Minimalist

Fast path from spec to execution using user-story requirements and Gherkin acceptance-criteria style.

For more details, see `openspec/schemas/minimalist/README.md`.

### Event-Driven

Structured workflow for event-centric systems with [Event Storming](https://en.wikipedia.org/wiki/Event_storming) discovery followed by [AsyncAPI](https://www.asyncapi.com/) specification.

For more details, see `openspec/schemas/event-driven/README.md`.

### Behaviour-Driven

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

### Intent-Driven

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

## Spec-Driven With ADR

Experimental proposal-to-tasks workflow for changes that also need durable
Architecture Decision Records persisted under the target repository's top-level
`adr/` folder.

For more details, see `openspec/schemas/spec-driven-with-adr/README.md`.

## Contributing

See `CONTRIBUTING.md` for how to create/customize schemas using `openspec schema init` / `openspec schema fork`, and how to validate before opening a PR.
