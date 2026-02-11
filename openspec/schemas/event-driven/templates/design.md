## Context

Summarize architecture context from `event-storming.md`, `event-modeling.md`,
and approved stories in `specs/**/*.md`.

## Goals / Non-Goals

- Goals:
- Non-goals:

## Messaging and Platform Decisions

### Broker / Runtime
- Selected broker/runtime:
- Rationale:
- Alternatives considered:

### Subject/Topic Naming
- Naming convention:
- Versioning strategy:
- Ownership conventions:

### Payload and Schema Format
- Message encoding format:
- Schema format and evolution rules:
- Compatibility expectations:

### Delivery Semantics and Reliability
- At-most-once / at-least-once / exactly-once expectations:
- Retry and dead-letter strategy:
- Idempotency strategy:

## Security Decisions

- Authentication approach:
- Authorization model:
- Sensitive data handling:
- Transport security and secret management:

## Operations and Observability

- Monitoring and alerting:
- Trace/correlation strategy:
- Capacity/performance considerations:

## Risks / Trade-offs

- [Risk] <description>
  - Mitigation:

## Handoff to AsyncAPI

List concrete inputs required to author `asyncapi.yaml`:
- Channels/subjects
- Messages and schemas
- Bindings/protocol details
- Security schemes
