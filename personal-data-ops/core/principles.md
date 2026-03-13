---
title: Architectural Principles for Personal Data Operations
status: draft
created: 2025-02-05T00:00:00.000Z
methodology: W3C working group approach
derived_from:
  - "[[requirements]]"
related:
  - "[[An Ontology of Memex]]"
tags:
  - ai-slop
author:
  - Sonnet 4.5
uuid: 9b515e15-5e7a-4731-b4b0-1e305e176b92
share: false
---
# Architectural Principles for Personal Data Operations

This document articulates the fundamental architectural principles that emerge from the requirements analysis. These principles guide technical decisions and serve as evaluation criteria for implementations.

**Methodology:** Principles derived from 90 requirements across 19 use cases, grounded in the memex ontology.

---

## P1: Agent Sovereignty

**Principle:** The agent must retain ultimate control over their mnemegrams, including access, modification, and deletion.

**Derived From:**

- R24 (Irrevocable deletion)
- R52 (Fine-grained AI access)
- R54 (Revoke AI access)
- R79 (Local privacy for usage data)
- R90 (Privacy for mental health data)

**Rationale:** Personal data operations infrastructure serves the agent. Control cannot be delegated to platforms, vendors, or intermediaries without agent consent. This includes the "right to forget" as well as the right to persist.

**Implications:**

- Local-first architectures are preferred over cloud-dependent systems
- Encryption keys must be agent-controlled
- Export must always be possible without platform permission
- Deletion must be meaningful, not performative (tombstones aren't enough)

**Tensions:**

- P1 vs P7 (Collective memory requires some persistence beyond individual control)
- P1 vs P10 (Sharing requires some access delegation)

**Related Essential Properties:** E6 (Agency)
**Related Telos:** T1 (To Persist), T11 (To Forget)

---

## P2: Temporal Integrity

**Principle:** Time is a first-class dimension of knowledge. Systems must preserve temporal ordering, support time-travel queries, and maintain provenance chains.

**Derived From:**

- R1 (Temporal ordering preservation)
- R2 (Provenance chain maintenance)
- R4 (Time-travel views)
- R66 (Graph queries for provenance)
- R68 (Temporal ordering of claim appearance)
- R72 (Temporal indexing)

**Rationale:** Understanding evolves over time. Knowing "what I thought when" and "what led to this thought" is essential for reflection, learning, and accountability. Time cannot be collapsed or lost.

**Implications:**

- Append-only or versioned storage models are favored
- Timestamps must be precise and trusted
- "Current state" views are derived from temporal history, not primary storage
- Edit history must be preserved

**Tensions:**

- P2 vs P1 (Time-travel conflicts with right to forget)
- P2 vs P9 (Storage costs of full history)

**Related Functions:** F6 (Versioning)
**Related Telos:** T7 (To Reflect), T5 (To Hold Accountable)

---

## P3: Semantic Richness

**Principle:** Meaning must be explicit and queryable, not implicit or locked in application logic. Relationships, context, and assertions are first-class data.

**Derived From:**

- R3 (Semantic query support)
- R14 (Graph traversal)
- R33 (Context assertions)
- R39 (Cross-type relatability)
- R41 (Entity and relationship modeling)
- R56 (Tasks as first-class entities)

**Rationale:** The value of personal knowledge lies in connections, not just content. "This relates to that because X" is knowledge. Systems that reduce everything to text search miss the graph structure.

**Implications:**

- Graph databases or RDF-like models preferred over document stores
- Relations must be typed and directional
- Context is metadata, not just tagging
- Queries must traverse relationships, not just match keywords

**Tensions:**

- P3 vs P9 (Semantic richness costs performance)
- P3 vs P4 (Too much structure reduces flexibility)

**Related Essential Properties:** E2 (Assertive Capacity), E3 (Referent Capacity)
**Related Functions:** F5 (Relating)
**Related Telos:** T3 (To Connect)

---

## P4: Schema Pluralism

**Principle:** No single schema can capture all knowledge. Systems must support schema evolution, multiple concurrent schemas, and schema-less capture when needed.

**Derived From:**

- R10 (Tool-independent representation)
- R11 (Relation preservation across schema transformations)
- R12 (Schema evolution without data loss)
- R28 (Maturity/status annotations)
- R37 (Low-friction integration)

**Rationale:** Understanding changes. Tools change. What you need to capture in the moment may not fit your current schema. Forcing premature formalization kills capture. But formalization enables query. Systems must support both.

**Implications:**

- "Schema-on-read" preferred over "schema-on-write"
- Multiple schema versions must coexist
- Core primitives (mnemegram, assertion, relation) must be schema-agnostic
- Tooling should suggest schemas, not enforce them

**Tensions:**

- P4 vs P3 (Flexibility vs queryability)
- P4 vs P6 (Interoperability requires some shared schema)

**Related Essential Properties:** E5 (Interpretability)
**Related Functions:** F1 (Inscription)

---

## P5: Friction Minimization

**Principle:** Capture friction determines what gets captured. Automation, integration, and low-effort inscription are critical for comprehensive memex.

**Derived From:**

- R36 (Automated multi-source capture)
- R37 (Low-friction integration)
- R45 (Communication platform integration)
- R46 (Platform API ingestion)
- R75 (Automated capture with manual annotation)
- R76 (Behavioral data capture)

**Rationale:** Manual logging doesn't scale. Data exhaust is knowledge. The memex must meet agents where they are, not require them to come to the memex. Automation enables comprehensiveness.

**Implications:**

- APIs and integrations are infrastructure, not nice-to-have
- Passive collection (with consent) is valid strategy
- Manual annotation should enhance, not enable, capture
- Mobile/wearable/ambient capture is legitimate

**Tensions:**

- P5 vs P1 (Automation risks losing agent control)
- P5 vs P8 (Comprehensive capture increases privacy risk)

**Related Functions:** F1 (Inscription)

---

## P6: Interoperability by Design

**Principle:** Personal knowledge must outlive any single tool. Systems must support export, import, and transformation without lock-in.

**Derived From:**

- R10 (Tool-independent representation)
- R11 (Relation preservation)
- R13 (Human-readable export)
- R29 (Presentation-ready export)
- R47 (Local content preservation)
- R49 (Handle platform shutdown)

**Rationale:** Tools die. Companies fail. Formats change. Personal knowledge spans decades. Lock-in is existential risk. Portability is not optional.

**Implications:**

- Open formats preferred over proprietary
- Full export must include structure, not just content
- Human-readable beats binary for longevity
- Import/export is core feature, not afterthought

**Tensions:**

- P6 vs P9 (Portable formats may be slower)
- P6 vs P3 (Generic formats may lose semantic richness)

**Related Telos:** T1 (To Persist), T6 (To Transmit)

---

## P7: Collective Possibility

**Principle:** While fundamentally personal, memex must support selective sharing, collaboration, and multi-generational transmission without sacrificing individual control.

**Derived From:**

- R8 (No duplication for sharing)
- R18 (Multi-agent support)
- R19 (Persistence beyond agent lifetime)
- R20 (Assertions by non-creator)
- R61 (Multi-agent authorship)
- R63 (Consensus mechanisms)

**Rationale:** Knowledge is social. Families remember together. Teams build shared understanding. Generations transmit to descendants. Personal memex must accommodate "we" alongside "I."

**Implications:**

- Multi-agent access models are required
- Attribution must be clear (who said what)
- Private and shared mnemegrams coexist in same space
- Generational handoff is design consideration

**Tensions:**

- P7 vs P1 (Collective memory may outlive individual control)
- P7 vs P8 (Sharing increases privacy complexity)

**Related Functions:** F8 (Transmission)
**Related Telos:** T9 (To Commune), T6 (To Transmit)

---

## P8: Protection by Default

**Principle:** Security and privacy must be foundational, not bolted on. Encryption, access control, and audit trails are core infrastructure.

**Derived From:**

- R5 (Fine-grained access control)
- R6 (Mnemegram-level access control)
- R9 (Auditable access grants)
- R23 (Cryptographic verification)
- R27 (Offline and under-duress protection)
- R44 (Privacy for relationship data)
- R74 (Privacy-preserving location storage)

**Rationale:** Personal knowledge is deeply intimate. Relationship graphs, location history, mental states, decisions - all highly sensitive. Breaches are catastrophic. Protection cannot be optional feature.

**Implications:**

- Encryption at rest and in transit
- Zero-knowledge architectures where possible
- Access control is granular (mnemegram-level, not just collection-level)
- Audit logs for all access
- Local processing for sensitive computation

**Tensions:**

- P8 vs P3 (Encryption limits queryability)
- P8 vs P5 (Security adds friction)
- P8 vs P10 (Fine-grained permissions are complex)

**Related Functions:** F9 (Protection)

---

## P9: Performance Pragmatism

**Principle:** Systems must perform at scale - decades of daily capture, millions of mnemegrams, complex graph queries - without requiring supercomputers.

**Derived From:**

- R3 (Semantic query support)
- R14 (Graph traversal)
- R38 (Temporal correlation analysis)
- R50 (Full-text search across heterogeneous content)
- R71 (Geospatial indexing)

**Rationale:** A memex that's too slow to query won't be used. Real-time retrieval is required for integration into daily work. Comprehensive knowledge is worthless if inaccessible.

**Implications:**

- Indexing strategies are critical
- Caching and materialized views may be necessary
- Some queries may require pre-computation
- Local-first helps (no network latency)
- Storage is cheaper than compute - denormalization acceptable

**Tensions:**

- P9 vs P2 (Full history is storage-intensive)
- P9 vs P3 (Graph queries can be expensive)
- P9 vs P6 (Optimized formats may be less portable)

**Related Functions:** F3 (Indexing), F4 (Retrieval)
**Related Essential Properties:** E4 (Retrievability)

---

## P10: Contextual Access

**Principle:** Access to knowledge must adapt to context - who's asking, why, when, and under what conditions. Static permissions are insufficient.

**Derived From:**

- R7 (Multi-context mnemegrams)
- R21 (Family as access unit)
- R25 (Capability-based delegation)
- R32 (Context-based partitioning)
- R52 (Fine-grained AI access)
- R87 (Context-aware surfacing)

**Rationale:** Knowledge exists in multiple contexts simultaneously. Work/personal boundaries are fluid. Sharing needs are situational. Access control must be expressive enough to handle complexity.

**Implications:**

- Attribute-based or capability-based access control
- Context as first-class metadata
- Temporal access grants (expire after time/condition)
- Delegatable, revocable permissions

**Tensions:**

- P10 vs P8 (Complexity increases attack surface)
- P10 vs P9 (Context evaluation adds overhead)

**Related Functions:** F9 (Protection)

---

## P11: Proactive Surfacing

**Principle:** The system should surface relevant knowledge without explicit queries. Retrieval is necessary but insufficient; surfacing is critical for serendipity and awareness.

**Derived From:**

- R17 (Non-obvious connection discovery)
- R30 (Surface knowledge gaps)
- R42 (Temporal decay functions)
- R77 (Pattern detection and anomaly alerts)
- R87 (Context-aware surfacing rules)
- R89 (Time-based triggers)

**Rationale:** You don't know what you need until you need it. Serendipitous discovery is how insight happens. Agents benefit from system that "reminds" them of relevant knowledge without request.

**Implications:**

- Recommendation algorithms based on context, time, patterns
- Anomaly detection (something unusual is happening)
- Relationship maintenance reminders
- Pattern surfacing (you always feel better after X)

**Tensions:**

- P11 vs P1 (Proactive surfacing risks being intrusive)
- P11 vs P9 (Recommendation computation is expensive)

**Related Functions:** F4.1 (Surfacing)
**Related Telos:** T4 (To Orient), T7 (To Reflect)

---

## P12: Provenance Traceability

**Principle:** Every mnemegram's lineage must be traceable - what it derives from, who created it, what influenced it, what it influenced.

**Derived From:**

- R2 (Provenance chain maintenance)
- R15 (Maintain provenance to source mnemegrams)
- R16 (Distinguish captured vs generative information)
- R55 (Boundary between AI-generated and human content)
- R66 (Graph queries for provenance chains)
- R82 (Link decisions to outcomes)

**Rationale:** Without provenance, knowledge becomes unmoored. "Where did I learn this?" "What led me to this conclusion?" "Did I write this or did AI?" Provenance enables accountability, reflection, and trust.

**Implications:**

- Provenance metadata on all mnemegrams
- Graph structure tracks influence/derivation
- AI-generated content is clearly marked
- Decision-outcome linkage preserved

**Tensions:**

- P12 vs P1 (Full provenance limits forgetting)
- P12 vs P9 (Provenance storage and query costs)

**Related Functions:** F6 (Versioning), F7 (Generation)
**Related Telos:** T5 (To Hold Accountable)

---

## P13: Heterogeneous Integration

**Principle:** Personal knowledge spans text, images, locations, biometrics, communications, decisions - all must be relatable within unified system.

**Derived From:**

- R39 (Cross-type relatability)
- R48 (Preserve context structure)
- R50 (Full-text search across heterogeneous content)
- R60 (Temporal data integration)
- R73 (Entity tracking - people, places)
- R86 (Emotional/mental state as first-class data)

**Rationale:** Life isn't siloed by data type. Understanding emerges from connections across modalities. "I slept poorly when I was in this location" requires relating sleep data, location data, and temporal data.

**Implications:**

- Unified graph model across data types
- Entity resolution (same person across systems)
- Flexible schema accommodates new data types
- Query language spans modalities

**Tensions:**

- P13 vs P3 (Heterogeneity complicates semantic modeling)
- P13 vs P9 (Cross-type queries are complex)

**Related Functions:** F5 (Relating)

---

## P14: Longevity Over Features

**Principle:** Long-term viability matters more than cutting-edge features. Systems must be maintainable across decades, independent of vendor survival.

**Derived From:**

- R13 (Human-readable export)
- R22 (Decadal maintainability)
- R47 (Local content preservation)
- R49 (Handle platform shutdown)

**Rationale:** Personal knowledge spans lifetimes. Systems that depend on startups, proprietary formats, or active maintenance will fail. Simplicity, openness, and self-hosting enable longevity.

**Implications:**

- Open source preferred over proprietary
- Self-hostable, not cloud-dependent
- Simple formats outlive complex ones
- Minimize external dependencies
- Documentation for future maintainers

**Tensions:**

- P14 vs P5 (Simple systems may have more friction)
- P14 vs P9 (Optimization may require complexity)

**Related Telos:** T1 (To Persist), T6 (To Transmit)

---

## P15: Graceful Degradation

**Principle:** Partial functionality is better than total failure. Systems should work offline, with limited data, or without AI enhancement.

**Derived From:**

- R27 (Offline and under-duress protection)
- R40 (Privacy-preserving local processing)
- R49 (Handle platform shutdown gracefully)

**Rationale:** Network fails. Servers go down. APIs get deprecated. AI models become unavailable. Core memex functions (capture, retrieve, relate) must work regardless.

**Implications:**

- Offline-first architecture
- Local processing where possible
- Core features don't depend on external services
- AI is enhancement, not requirement

**Tensions:**

- P15 vs P5 (Some automation requires external services)
- P15 vs P11 (Advanced surfacing may need cloud compute)

---

## Principle Interdependencies

### Reinforcing Principles (strengthen each other)

- **P1 (Agent Sovereignty) ↔ P6 (Interoperability)**: Control requires portability
- **P2 (Temporal Integrity) ↔ P12 (Provenance)**: Time enables provenance tracking
- **P3 (Semantic Richness) ↔ P13 (Heterogeneous Integration)**: Both require graph thinking
- **P5 (Friction Minimization) ↔ P11 (Proactive Surfacing)**: Both reduce agent effort
- **P8 (Protection) ↔ P10 (Contextual Access)**: Fine-grained control enables safe sharing
- **P14 (Longevity) ↔ P15 (Graceful Degradation)**: Both prioritize resilience

### Conflicting Principles (require tradeoffs)

- **P1 (Agent Sovereignty) ⚡ P7 (Collective Possibility)**: Individual vs collective control
- **P2 (Temporal Integrity) ⚡ P1 (Agent Sovereignty)**: Full history vs right to forget
- **P3 (Semantic Richness) ⚡ P4 (Schema Pluralism)**: Structure vs flexibility
- **P5 (Friction Minimization) ⚡ P8 (Protection)**: Ease of use vs security
- **P8 (Protection) ⚡ P9 (Performance)**: Encryption costs performance
- **P9 (Performance) ⚡ P2 (Temporal Integrity)**: Speed vs full history
- **P11 (Proactive Surfacing) ⚡ P1 (Agent Sovereignty)**: Helpfulness vs intrusion
- **P14 (Longevity) ⚡ P9 (Performance)**: Simple/portable vs optimized

---

## Essential vs Aspirational Principles

### Essential (Non-Negotiable)

These must be satisfied for system to qualify as personal data operations infrastructure:

1. **P1 - Agent Sovereignty**: Without this, it's not "personal"
2. **P6 - Interoperability**: Without this, it's not sustainable
3. **P8 - Protection**: Without this, it's not safe
4. **E4 (from ontology) - Retrievability**: Without this, it's not functional

### Core (Highly Important)

These dramatically affect quality but system can function without perfect implementation:

5. **P2 - Temporal Integrity**: Makes reflection possible
6. **P3 - Semantic Richness**: Makes insight possible
7. **P4 - Schema Pluralism**: Makes growth possible
8. **P12 - Provenance Traceability**: Makes accountability possible

### Desirable (Quality of Life)

These improve experience but aren't definitional:

9. **P5 - Friction Minimization**: Affects adoption
10. **P9 - Performance Pragmatism**: Affects usability
11. **P11 - Proactive Surfacing**: Affects value
12. **P15 - Graceful Degradation**: Affects reliability

### Contextual (Depends on Use Case)

Some scenarios need these more than others:

13. **P7 - Collective Possibility**: Essential for families/teams, optional for pure individual use
14. **P10 - Contextual Access**: Essential for work/personal mix, simpler for purely personal
15. **P13 - Heterogeneous Integration**: Essential for quantified self, less so for text-only
16. **P14 - Longevity Over Features**: Essential for archival use, less so for active research

---

## Evaluation Framework

Use these principles to evaluate any personal data operations implementation:

**Score each principle: 0 (not addressed), 1 (partially), 2 (fully)**

Minimum viable system: P1, P6, P8, E4 must score 2
High-quality system: At least 12/15 principles score ≥1
Excellent system: At least 10/15 principles score 2

---

## Next Steps

1. **Map Existing Systems**: How do Obsidian, Roam, atproto, Solid score against these principles?
2. **Identify Gaps**: Which principles are universally underserved?
3. **Design Patterns**: What architectural patterns satisfy multiple principles?
4. **Prioritize Experiments**: Which principles should guide initial prototypes?

---

## Cross-References

- [[requirements]] - 90 requirements these principles derive from
- [[use-cases]] - 19 use cases that generated requirements
- [[An Ontology of Memex]] - Foundational ontology
- [[design-tradeoffs]] - Tensions document (from earlier landscape work)