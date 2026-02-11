# OpenSpec Schemas

Custom [OpenSpec](https://github.com/Fission-AI/OpenSpec) schemas packaged as copyable folders under `openspec/schemas/`.

Default OpenSpec includes the `spec-driven` schema, which is a strong general-purpose workflow. This repo adds more focused workflows for specific delivery contexts, and also demonstrates how to customise OpenSpec for different styles of work.

## Install a Schema (Agent + Shell Agnostic)

Copy the schema folder you want from `https://github.com/intent-driven-dev/openspec-schemas` into your project at `openspec/schemas/<schema-name>`.

Example: copy `openspec/schemas/event-driven` from this repo into your project as `openspec/schemas/event-driven`.

## Minimalist

Fast path from spec to execution using user-story requirements and Gherkin acceptance-criteria style.

For more details, see `openspec/schemas/minimalist/README.md`.

## Event-Driven

Structured workflow for event-centric systems with [Event Storming](https://en.wikipedia.org/wiki/Event_storming) discovery followed by [AsyncAPI](https://www.asyncapi.com/) specification.

For more details, see `openspec/schemas/event-driven/README.md`.
