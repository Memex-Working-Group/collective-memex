---
title: Requirements for Personal Data Operations
status: draft
created: 2025-02-05
methodology: W3C working group approach
source:
  - "[[use-cases]]"
related:
  - "[[An Ontology of Memex]]"
tags:
  - ai-slop
---

# Requirements for Personal Data Operations

This document consolidates requirements extracted from use cases. Requirements are organized by functional domain and mapped back to the memex ontology (Essential properties, Functions, and Teleological orientations).

**Methodology:** Requirements derived from 19 use cases following W3C working group approach.

---

## Temporal & Provenance Requirements

Requirements for tracking time, history, and lineage of knowledge.

### R1: Temporal Ordering Preservation

**Definition:** System must preserve temporal ordering of mnemegrams
**Rationale:** Understanding conceptual evolution requires knowing "when" - the sequence matters
**Related Functions:** F6 (Versioning)
**Source:** UC-1 (Researcher Traces Evolution)

### R2: Provenance Chain Maintenance

**Definition:** System must maintain provenance chains (what influenced what)
**Rationale:** Tracing how understanding developed requires tracking causal/influence relationships
**Related Functions:** F6 (Versioning), F5 (Relating)
**Related Telos:** T7 (To Reflect)
**Source:** UC-1, UC-15 (News Provenance)

### R4: Time-Travel Views

**Definition:** System must support "time-travel" views (what did I know when?)
**Rationale:** Reflecting on past understanding requires ability to see state at specific moments
**Related Functions:** F6 (Versioning), F4 (Retrieval)
**Source:** UC-1

### R66: Graph Queries for Provenance Chains

**Definition:** System must support graph queries for provenance chains
**Rationale:** Tracing information genealogy requires graph traversal capabilities
**Related Functions:** F5 (Relating)
**Source:** UC-15

### R67: Same Claim, Different Framings

**Definition:** System must support "same claim, different framings"
**Rationale:** Understanding information evolution requires comparing variations
**Source:** UC-15

### R68: Temporal Ordering of Claim Appearance

**Definition:** System must track temporal ordering of claim appearance
**Rationale:** Knowing "who said it first" matters for provenance
**Related Functions:** F6 (Versioning)
**Source:** UC-15

### R82: Link Decisions to Outcomes

**Definition:** System must link decisions to outcomes (retroactive evaluation)
**Rationale:** Learning from decisions requires connecting them to results
**Related Functions:** F5 (Relating), F6 (Versioning)
**Source:** UC-18

---

## Retrieval & Query Requirements

Requirements for finding, surfacing, and accessing mnemegrams.

### R3: Semantic Query Support

**Definition:** Retrieval must support semantic queries, not just keyword matching
**Rationale:** Personal knowledge often needs conceptual search, not exact text match
**Related Functions:** F4 (Retrieval)
**Related Telos:** T3 (To Connect)
**Source:** UC-1

### R14: Graph Traversal and Pattern Detection

**Definition:** System must support graph traversal and pattern detection
**Rationale:** Discovering connections requires exploring relationship networks
**Related Functions:** F5 (Relating), F4.1 (Surfacing)
**Source:** UC-4

### R17: Non-Obvious Connection Discovery

**Definition:** Surfacing should help discover non-obvious connections
**Rationale:** Value of memex includes serendipitous insight
**Related Functions:** F4.1 (Surfacing)
**Related Telos:** T3 (To Connect), T8 (To Generate)
**Source:** UC-4

### R30: Surface Knowledge Gaps

**Definition:** System should surface gaps (what's underexplored)
**Rationale:** Metacognition requires awareness of what's missing
**Related Functions:** F4.1 (Surfacing)
**Related Telos:** T7 (To Reflect)
**Source:** UC-7

### R31: Progression Queries

**Definition:** Retrieval should support "show my progression on X"
**Rationale:** Learning requires seeing development over time
**Related Functions:** F4 (Retrieval), F6 (Versioning)
**Source:** UC-7

### R43: Context Retrieval Based on Agent Queries

**Definition:** System must support context retrieval based on agent queries
**Rationale:** Pre-meeting briefings, task context depend on agent-initiated queries
**Related Functions:** F4 (Retrieval)
**Source:** UC-10

### R50: Full-Text Search Across Heterogeneous Content

**Definition:** System must support full-text search across heterogeneous content types
**Rationale:** Personal memex contains varied formats - all must be searchable
**Related Functions:** F4 (Retrieval)
**Source:** UC-11

### R58: Task Queries Surface Relevant Mnemegrams

**Definition:** Task queries should surface relevant mnemegrams
**Rationale:** Context-aware work requires linking tasks to knowledge
**Related Functions:** F4 (Retrieval), F5 (Relating)
**Source:** UC-13

### R71: Geospatial Indexing and Query Support

**Definition:** System must support geospatial indexing and query
**Rationale:** "Where was I when X happened?" is valid query pattern
**Related Functions:** F3 (Indexing), F4 (Retrieval)
**Source:** UC-16

### R72: Temporal Indexing

**Definition:** System must support temporal indexing (when)
**Rationale:** Time-based queries are fundamental to personal memory
**Related Functions:** F3 (Indexing)
**Source:** UC-16

### R84: Temporal Queries

**Definition:** System must support temporal queries ("what did we decide when?")
**Rationale:** Decision archaeology requires time-based search
**Related Functions:** F4 (Retrieval)
**Source:** UC-18

---

## Access Control & Protection Requirements

Requirements for security, privacy, and permission management.

### R5: Fine-Grained Access Control

**Definition:** System must support fine-grained access control (not just all-or-nothing)
**Rationale:** Sharing requires nuance - not everything should be visible to everyone
**Related Functions:** F9 (Protection)
**Related Telos:** T9 (To Commune), T5 (To Hold Accountable)
**Source:** UC-2

### R6: Mnemegram-Level Access Control

**Definition:** Access control must work at mnemegram level, not just collection level
**Rationale:** Individual items may have different sensitivity/context
**Related Functions:** F9 (Protection)
**Source:** UC-2

### R7: Multi-Context Mnemegrams

**Definition:** System must handle mnemegrams that belong to multiple contexts
**Rationale:** Work/personal boundaries are not always clean
**Related Functions:** F9 (Protection), F2 (Assertion)
**Source:** UC-2

### R9: Auditable Access Grants

**Definition:** Access grants must be auditable (who saw what, when)
**Rationale:** Accountability requires knowing who accessed what
**Related Functions:** F9 (Protection)
**Related Telos:** T5 (To Hold Accountable)
**Source:** UC-2

### R21: Family as Access Unit

**Definition:** Access control must support "family" as unit, not just individuals
**Rationale:** Some sharing contexts are collective, not individual
**Related Functions:** F9 (Protection)
**Source:** UC-5

### R23: Cryptographic Verification

**Definition:** System must support cryptographic verification of mnemegrams
**Rationale:** Proving authenticity under threat requires cryptography
**Related Functions:** F9 (Protection)
**Related Telos:** T5 (To Hold Accountable)
**Source:** UC-6

### R24: Irrevocable Deletion

**Definition:** Deletion must be irrevocable (not just tombstones)
**Rationale:** True forgetting requires actual removal, not just marking deleted
**Related Functions:** F9 (Protection)
**Related Telos:** T11 (To Forget)
**Source:** UC-6

### R25: Capability-Based Delegation

**Definition:** Access control must support capability-based delegation
**Rationale:** Flexible sharing requires delegatable access tokens
**Related Functions:** F9 (Protection), F8 (Transmission)
**Source:** UC-6

### R26: Dead Man's Switch Transmission

**Definition:** System must support "dead man's switch" transmission
**Rationale:** Some information should be shared upon creator's death/absence
**Related Functions:** F8 (Transmission), F9 (Protection)
**Related Telos:** T6 (To Transmit)
**Source:** UC-6

### R27: Offline and Under-Duress Protection

**Definition:** Protection must work offline and under duress
**Rationale:** Activist/threat scenarios require local-only security
**Related Functions:** F9 (Protection)
**Source:** UC-6

### R32: Context-Based Partitioning

**Definition:** System must support context-based partitioning
**Rationale:** Work/personal separation requires contextual boundaries
**Related Functions:** F9 (Protection)
**Source:** UC-8

### R35: Audit Trail of Preservation/Deletion

**Definition:** Audit trail must show what was preserved/deleted
**Rationale:** Transitions require knowing what happened to data
**Related Functions:** F9 (Protection)
**Source:** UC-8

### R44: Privacy for Relationship Data

**Definition:** Privacy: relationship data is especially sensitive
**Rationale:** Social graph information reveals personal connections
**Related Functions:** F9 (Protection)
**Source:** UC-10

### R52: Fine-Grained AI Access Permissions

**Definition:** System must have fine-grained permission model for AI access
**Rationale:** AI agents need controlled, specific access, not blanket permissions
**Related Functions:** F9 (Protection)
**Source:** UC-12

### R53: AI Query Audit Trail

**Definition:** System must maintain audit trail of AI queries and actions
**Rationale:** Knowing what AI accessed matters for control
**Related Functions:** F9 (Protection)
**Source:** UC-12

### R54: Revoke AI Access to Specific Mnemegrams

**Definition:** System must allow revoking AI access to specific mnemegrams
**Rationale:** Permissions should be changeable, not permanent
**Related Functions:** F9 (Protection)
**Source:** UC-12

### R74: Privacy-Preserving Location Storage

**Definition:** System must use privacy-preserving location storage
**Rationale:** Location history is highly sensitive
**Related Functions:** F9 (Protection)
**Source:** UC-16

### R79: Local Privacy for Usage Data

**Definition:** Privacy: usage data stays local
**Rationale:** Behavioral patterns are intimate, should not leak
**Related Functions:** F9 (Protection)
**Source:** UC-17

### R90: Privacy for Mental Health Data

**Definition:** Privacy: deeply personal mental health data
**Rationale:** Emotional states are extremely sensitive
**Related Functions:** F9 (Protection)
**Source:** UC-19

---

## Schema & Interoperability Requirements

Requirements for data representation, portability, and tool independence.

### R10: Tool-Independent Representation

**Definition:** Mnemegrams must have tool-independent representation
**Rationale:** Tool lock-in prevents long-term knowledge preservation
**Related Essential:** E5 (Interpretability)
**Related Telos:** T1 (To Persist)
**Source:** UC-3

### R11: Relation Preservation Across Schema Transformations

**Definition:** Relations must be preserved across schema transformations
**Rationale:** Tool migration should not break connections
**Related Functions:** F5 (Relating)
**Source:** UC-3

### R12: Schema Evolution Without Data Loss

**Definition:** System must support schema evolution without data loss
**Rationale:** Understanding evolves; schema should evolve with it
**Related Essential:** E5 (Interpretability)
**Source:** UC-3

### R13: Human-Readable Export Format

**Definition:** Export format must be human-readable (outlive the tools)
**Rationale:** Long-term preservation requires readable formats
**Related Telos:** T1 (To Persist)
**Source:** UC-3

### R28: Maturity/Status Annotations

**Definition:** System must support annotation of mnemegrams with maturity/status
**Rationale:** Not all knowledge is equally developed - status matters
**Related Functions:** F2 (Assertion)
**Source:** UC-7

### R29: Presentation-Ready Export

**Definition:** Collections must be exportable in presentation-ready formats
**Rationale:** Knowledge must be shareable beyond the memex
**Related Functions:** F8 (Transmission)
**Source:** UC-7

### R81: Structured Decision Documentation Format

**Definition:** System must support structured decision documentation format
**Rationale:** Some knowledge types benefit from formalization
**Related Functions:** F1 (Inscription), F2 (Assertion)
**Source:** UC-18

### R85: Export for Handoff/Transitions

**Definition:** System must support export for handoff/transitions
**Rationale:** Knowledge transfer requires portable formats
**Related Functions:** F8 (Transmission)
**Source:** UC-18

---

## Multi-Agent & Collaboration Requirements

Requirements for supporting multiple agents and shared knowledge.

### R8: No Duplication for Sharing

**Definition:** Sharing must not require duplicating or forking the memex
**Rationale:** Same knowledge should exist once, with controlled access
**Related Functions:** F8 (Transmission)
**Source:** UC-2

### R18: Multi-Agent Support with Different Roles

**Definition:** System must support multiple agents with different roles
**Rationale:** Families, teams have varied contribution patterns
**Related Functions:** F1 (Inscription), F9 (Protection)
**Related Telos:** T9 (To Commune)
**Source:** UC-5

### R19: Persistence Beyond Agent Lifetime

**Definition:** Mnemegrams must persist beyond creating agent's lifetime
**Rationale:** Generational memory requires surviving individuals
**Related Telos:** T6 (To Transmit), T1 (To Persist)
**Source:** UC-5

### R20: Assertions by Non-Creator Agents

**Definition:** Assertions can be added by agents other than original creator
**Rationale:** Collective memory involves multiple interpretations
**Related Functions:** F2 (Assertion)
**Source:** UC-5

### R61: Multi-Agent Authorship with Attribution

**Definition:** System must support multi-agent authorship with clear attribution
**Rationale:** Collaborative knowledge requires knowing who said what
**Related Functions:** F1 (Inscription)
**Related Telos:** T9 (To Commune), T5 (To Hold Accountable)
**Source:** UC-14

### R62: Personal vs Shared Mnemegrams

**Definition:** System must distinguish between personal and shared mnemegrams
**Rationale:** Not all knowledge in collaboration is collective
**Related Functions:** F9 (Protection)
**Source:** UC-14

### R63: Consensus Mechanisms

**Definition:** System must support consensus mechanisms (this claim is accepted by group)
**Rationale:** Group knowledge involves agreement/disagreement
**Related Functions:** F2 (Assertion)
**Source:** UC-14

### R64: Activity Visibility for Accountability

**Definition:** System must support activity visibility for social accountability
**Rationale:** Collaboration benefits from knowing who's contributing
**Related Telos:** T5 (To Hold Accountable)
**Source:** UC-14

### R65: Merge/Fork Operations

**Definition:** System must support merge/fork operations for diverging interpretations
**Rationale:** Collaborative knowledge sometimes needs to branch
**Related Functions:** F6 (Versioning)
**Source:** UC-14

### R83: Multi-Agent Access for Team Logs

**Definition:** System must support multi-agent access (team decision logs)
**Rationale:** Organizational memory is multi-author
**Source:** UC-18

---

## Generation & Derivation Requirements

Requirements for creating new knowledge from existing content.

### R15: Maintain Provenance to Source Mnemegrams

**Definition:** Generated content must maintain provenance to source mnemegrams
**Rationale:** Derivative work should cite its sources
**Related Functions:** F7 (Generation)
**Related Telos:** T8 (To Generate)
**Source:** UC-4

### R16: Distinguish Captured vs Generative Information

**Definition:** System must distinguish captured vs generative information
**Rationale:** Knowing whether something is observed or derived matters
**Related Functions:** F7 (Generation), F1 (Inscription)
**Source:** UC-4

### R55: Boundary Between AI-Generated and Human Content

**Definition:** System must clearly mark boundary between AI-generated and human-captured content
**Rationale:** Agency and authorship matter
**Related Functions:** F7 (Generation)
**Source:** UC-12

---

## Automation & Integration Requirements

Requirements for low-friction capture and external system integration.

### R36: Automated Multi-Source Capture

**Definition:** System must support automated capture from multiple data sources
**Rationale:** Manual logging doesn't scale; automation enables data exhaust
**Related Functions:** F1 (Inscription)
**Source:** UC-9

### R37: Low-Friction Integration

**Definition:** Integration must be low-friction (ideally zero manual input)
**Rationale:** Capture friction determines what gets captured
**Related Functions:** F1 (Inscription)
**Source:** UC-9

### R45: Communication Platform Integration

**Definition:** System must integrate with communication platforms (email, messaging)
**Rationale:** Conversations are knowledge - need capture from where they happen
**Related Functions:** F1 (Inscription)
**Source:** UC-10

### R46: Platform API Ingestion

**Definition:** System must ingest content from external platforms via APIs
**Rationale:** Knowledge exists across platforms - need ingestion capability
**Related Functions:** F1 (Inscription)
**Source:** UC-11

### R47: Local Content Preservation

**Definition:** Content must be preserved locally (not just links)
**Rationale:** External platforms die - content must survive
**Related Telos:** T1 (To Persist)
**Source:** UC-11

### R48: Preserve Context Structure

**Definition:** Capture must preserve context (thread structure, replies)
**Rationale:** Meaning depends on context - isolated content loses value
**Related Functions:** F1 (Inscription), F2 (Assertion)
**Source:** UC-11

### R49: Handle Platform Shutdown Gracefully

**Definition:** System must handle platform shutdown gracefully
**Rationale:** External dependencies will fail - system must be resilient
**Source:** UC-11

### R51: Programmatic API for Agent Access

**Definition:** System must provide API for programmatic access to memex by agents
**Rationale:** AI assistants, automation require machine-readable access
**Related Essential:** E6 (Agency)
**Source:** UC-12

### R70: Web Archive Integration

**Definition:** System must integrate with web archive/preservation
**Rationale:** External content disappears - archiving essential for provenance
**Source:** UC-15

### R75: Automated Capture with Manual Annotation

**Definition:** System must support automated capture with manual annotation
**Rationale:** Balance automation (scale) with human interpretation (meaning)
**Related Functions:** F1 (Inscription), F2 (Assertion)
**Source:** UC-16

### R76: Behavioral Data Capture

**Definition:** System must support behavioral data capture (usage logs)
**Rationale:** Self-awareness requires tracking behavior
**Related Functions:** F1 (Inscription)
**Source:** UC-17

---

## Relation & Structure Requirements

Requirements for connecting and organizing knowledge.

### R33: Context Assertions

**Definition:** Assertions can indicate "work context" vs "personal context"
**Rationale:** Context is semantic information about mnemegrams
**Related Functions:** F2 (Assertion)
**Source:** UC-8

### R34: Context-Aware Reference Integrity

**Definition:** Deletion of personal context must not break work context references
**Rationale:** Partitioning shouldn't create dangling references
**Related Functions:** F5 (Relating)
**Source:** UC-8

### R38: Temporal Correlation Analysis

**Definition:** System must support temporal correlation analysis
**Rationale:** "What causes what?" requires correlation over time
**Related Functions:** F5 (Relating)
**Source:** UC-9

### R39: Cross-Type Relatability

**Definition:** Different data types (location, biometric, behavioral) must be relatable
**Rationale:** Insights emerge from connecting heterogeneous data
**Related Functions:** F5 (Relating)
**Source:** UC-9

### R41: Entity and Relationship Modeling

**Definition:** System must model entities (people) and their relationships
**Rationale:** Social graph is knowledge structure
**Related Functions:** F5 (Relating)
**Source:** UC-10

### R42: Temporal Decay Functions

**Definition:** System must support temporal decay functions ("relationship half-life")
**Rationale:** Time matters for relationships - need mathematical models
**Related Functions:** F4.1 (Surfacing)
**Source:** UC-10

### R56: Tasks as First-Class Entities

**Definition:** Tasks are first-class entities with rich context
**Rationale:** Tasks aren't separate from knowledge - they're embedded
**Related Functions:** F2 (Assertion)
**Source:** UC-13

### R57: Bidirectional Links Between Tasks and Knowledge

**Definition:** System must support bidirectional links between tasks and knowledge
**Rationale:** Tasks reference knowledge; knowledge implies tasks
**Related Functions:** F5 (Relating)
**Source:** UC-13

### R59: Task Transformation Support

**Definition:** System must support task transformation (research → draft → publish)
**Rationale:** Tasks evolve through states
**Related Functions:** F6 (Versioning)
**Source:** UC-13

### R60: Temporal Data Integration

**Definition:** System must integrate with temporal data (deadlines, schedules)
**Rationale:** Time-based constraints affect knowledge work
**Related Functions:** F5 (Relating)
**Source:** UC-13

### R69: Primary vs Secondary Source Distinction

**Definition:** System must distinguish between primary and secondary sources
**Rationale:** Provenance chains have hierarchies
**Related Functions:** F2 (Assertion)
**Source:** UC-15

### R73: Entity Tracking (People, Places)

**Definition:** System must support entity tracking (people, places)
**Rationale:** Persistent referents enable connection across mnemegrams
**Related Essential:** E3 (Referent Capacity)
**Source:** UC-16

### R88: State to Intervention Pattern Matching

**Definition:** System must support pattern matching: state → helpful intervention
**Rationale:** Conditioning requires learning "when I feel X, Y helps"
**Related Functions:** F5 (Relating), F4.1 (Surfacing)
**Source:** UC-19

---

## Surfacing & Proactivity Requirements

Requirements for system-initiated presentation and recommendations.

### R77: Pattern Detection and Anomaly Alerts

**Definition:** System must support pattern detection and anomaly alerts
**Rationale:** Awareness of patterns requires surfacing them
**Related Functions:** F4.1 (Surfacing)
**Source:** UC-17

### R78: Intervention System

**Definition:** System must support intervention system (notifications, blocks)
**Rationale:** Behavioral change requires active intervention
**Related Functions:** F4.1 (Surfacing)
**Source:** UC-17

### R80: Pattern Visualization Over Time

**Definition:** System must support visualization of patterns over time
**Rationale:** Understanding trends requires temporal views
**Related Functions:** F4.1 (Surfacing)
**Source:** UC-17

### R86: Emotional/Mental State as First-Class Data

**Definition:** System must treat emotional/mental state as first-class data
**Rationale:** Wellbeing is valid knowledge domain
**Related Functions:** F1 (Inscription), F2 (Assertion)
**Source:** UC-19

### R87: Context-Aware Surfacing Rules

**Definition:** System must support context-aware surfacing rules
**Rationale:** "Right content at right time" requires context
**Related Functions:** F4.1 (Surfacing)
**Source:** UC-19

### R89: Time-Based Triggers

**Definition:** System must support time-based triggers (reminders, scheduled surfacing)
**Rationale:** Some content should appear at specific times
**Related Functions:** F4.1 (Surfacing)
**Source:** UC-19

---

## Infrastructure & Longevity Requirements

Requirements for system sustainability and long-term viability.

### R22: Decadal Maintainability

**Definition:** System must be maintainable across decades (not dependent on startup survival)
**Rationale:** Personal knowledge outlives companies
**Related Telos:** T1 (To Persist), T6 (To Transmit)
**Source:** UC-5

### R40: Privacy-Preserving Local Processing

**Definition:** System must support privacy-preserving local processing (sensitive health data)
**Rationale:** Some computation must happen locally for privacy
**Related Functions:** F9 (Protection)
**Source:** UC-9

---

## Summary Statistics

**Total Requirements:** 90 (R1-R90)

**By Functional Domain:**

- Temporal & Provenance: 8 requirements
- Retrieval & Query: 12 requirements
- Access Control & Protection: 19 requirements
- Schema & Interoperability: 8 requirements
- Multi-Agent & Collaboration: 9 requirements
- Generation & Derivation: 3 requirements
- Automation & Integration: 11 requirements
- Relation & Structure: 13 requirements
- Surfacing & Proactivity: 6 requirements
- Infrastructure & Longevity: 2 requirements

**Most Referenced Memex Functions:**

- F9 (Protection): 19 requirements
- F1 (Inscription): 11 requirements
- F4 (Retrieval): 10 requirements
- F5 (Relating): 10 requirements
- F2 (Assertion): 9 requirements

**Most Referenced Teleological Orientations:**

- T1 (To Persist): 5 requirements
- T9 (To Commune): 5 requirements
- T5 (To Hold Accountable): 5 requirements

---

## Next Steps

1. **Derive Principles** - What architectural principles emerge from these requirements?
2. **Identify Conflicts** - Which requirements tension with each other?
3. **Prioritize** - Which requirements are essential vs nice-to-have?
4. **Map to Existing Systems** - How well do current technologies satisfy these requirements?

---

## Cross-References

- [[use-cases]] - Source use cases for these requirements
- [[principles]] - (To be created: architectural principles derived from requirements)
- [[An Ontology of Memex]] - Foundational ontology
