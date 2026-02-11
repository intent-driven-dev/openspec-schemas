# Event Modeling

Convert event-storming outputs into explicit behavior flows.

Use this lane sequence for each scenario:
`Trigger -> Command -> Event -> Read Model`

## Scenario Overview
- Scenario:
- Business objective:
- Source references from `event-storming.md`:

## Swim Lanes

### Trigger
- Human/system trigger:
- Input signal:

### Command
- Command name:
- Target aggregate/context:
- Validation rules:

### Event
- Event name:
- Event payload summary:
- Ordering/idempotency notes:

### Read Model
- Projection or materialized view:
- Consumer(s):
- Query/use-case enabled:

## Mermaid Flow
```mermaid
flowchart LR
  T[Trigger] --> C[Command]
  C --> E[Event]
  E --> R[Read Model]

  classDef actor fill:#F7DC6F,stroke:#B7950B,color:#1C1C1C
  classDef command fill:#85C1E9,stroke:#2471A3,color:#1C1C1C
  classDef event fill:#F5B041,stroke:#AF601A,color:#1C1C1C
  classDef policy fill:#D7BDE2,stroke:#884EA0,color:#1C1C1C
  classDef readModel fill:#82E0AA,stroke:#1E8449,color:#1C1C1C

  class T actor
  class C command
  class E event
  class R readModel
```

## Timeline / Swimlane Diagram
```mermaid
flowchart LR
  subgraph TriggerLane[Trigger]
    T1[Trigger]
  end
  subgraph CommandLane[Command]
    C1[Command]
  end
  subgraph EventLane[Event]
    E1[Event]
  end
  subgraph ReadModelLane[Read Model]
    R1[Read Model]
  end

  T1 --> C1
  C1 --> E1
  E1 --> R1

  classDef actor fill:#F7DC6F,stroke:#B7950B,color:#1C1C1C
  classDef command fill:#85C1E9,stroke:#2471A3,color:#1C1C1C
  classDef event fill:#F5B041,stroke:#AF601A,color:#1C1C1C
  classDef policy fill:#D7BDE2,stroke:#884EA0,color:#1C1C1C
  classDef readModel fill:#82E0AA,stroke:#1E8449,color:#1C1C1C

  class T1 actor
  class C1 command
  class E1 event
  class R1 readModel
```

## Derivation Notes for Downstream Artifacts
- Specs inputs (user stories and acceptance criteria):
- Design inputs (broker, subject naming, payload format, security):
- AsyncAPI inputs (channels, messages, bindings, schemas):
