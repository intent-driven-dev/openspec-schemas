# Event Storming

Capture collaborative discovery outcomes for the domain before formal specs.

## Scope and Goal
- Domain/problem area:
- Desired business outcome:
- In/out of scope:

## Actors
- Primary users:
- External systems:
- Automated agents:

## Domain Events (Past Tense)
- Event:
  - Trigger/why it happened:
  - Data emitted:
  - Business impact:

## Commands
- Command:
  - Issuer (actor/system):
  - Aggregate/context target:
  - Preconditions:
  - Expected event(s):

## Aggregates / Bounded Contexts
- Aggregate/context:
  - Responsibilities:
  - Invariants:
  - Owned data:

## Automations / Policies
- Automation/policy name:
  - Triggering event:
  - Command emitted:
  - Failure handling:

## Timeline Diagram (Mermaid)
```mermaid
flowchart LR
  A[Actor/User] --> B[Command]
  B --> C[Domain Event]
  C --> D[Policy/Automation]
  C --> E[Read Model/Projection]

  classDef actor fill:#F7DC6F,stroke:#B7950B,color:#1C1C1C
  classDef command fill:#85C1E9,stroke:#2471A3,color:#1C1C1C
  classDef event fill:#F5B041,stroke:#AF601A,color:#1C1C1C
  classDef policy fill:#D7BDE2,stroke:#884EA0,color:#1C1C1C
  classDef readModel fill:#82E0AA,stroke:#1E8449,color:#1C1C1C

  class A actor
  class B command
  class C event
  class D policy
  class E readModel
```

## Hotspots and Open Questions
- Ambiguity:
- Risk:
- Decision needed:

## Handoff to Next Artifacts
Summarize how these findings should inform:
- `event-modeling.md`
- `specs/**/*.md`
- `design.md`
- `asyncapi.yaml`
