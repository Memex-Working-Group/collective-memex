---
date: 2026-01-25
author:
  - Opus 4.5
---

# Memex Ontology: Relations Supplement

## Primitive Element Relations

How the primitive elements relate to each other:

```mermaid
graph TD
    Agent[Agent] -->|creates| Mnemegram[Mnemegram]
    Agent -->|makes| Assertion[Assertion]
    Agent -->|applies| Schema[Schema]

    Mnemegram -->|references| Referent[Referent]
    Mnemegram -->|has| Context[Context]
    Mnemegram -->|connected by| Relation[Relation]
    Mnemegram -->|organized in| Collection[Collection]
    Mnemegram -->|tracked via| Provenance[Provenance]
    Mnemegram -->|found via| Index[Index]

    Assertion -->|about| Mnemegram
    Assertion -->|about| Referent
    Assertion -->|about| Relation

    Schema -->|interprets| Mnemegram
    Schema -->|interprets| Assertion

    Context -->|composed of| Assertion

    Relation -->|between| Mnemegram
    Relation -->|between| Referent

    Referent -->|emerges from| Mnemegram
```

---

## Information Flow

How information moves through the memex:

```mermaid
flowchart LR
    subgraph External
        Experience[Lived Experience]
        OtherAgent[Other Agents]
    end

    subgraph Memex
        direction TB
        Inscription[F1: Inscription]
        Mnemegram[(Mnemegram)]
        Assertion[F2: Assertion]
        Index[F3: Indexing]
        Retrieval[F4: Retrieval]
        Surfacing[F4.1: Surfacing]
        Relating[F5: Relating]
        Versioning[F6: Versioning]
        Generation[F7: Generation]
        Transmission[F8: Transmission]
        Protection[F9: Protection]
    end

    Experience -->|shadow cast| Inscription
    Inscription --> Mnemegram
    Mnemegram --> Assertion
    Mnemegram --> Index
    Index --> Retrieval
    Index --> Surfacing
    Mnemegram --> Relating
    Mnemegram --> Versioning
    Mnemegram --> Generation
    Generation -->|new| Mnemegram
    Mnemegram --> Transmission
    Transmission --> OtherAgent
    Protection -.->|guards| Mnemegram

    Retrieval -->|returns to| Agent[Agent]
    Surfacing -->|offers to| Agent
```

---

_Relations supplement to "[[An Ontology of Memex]]"_
