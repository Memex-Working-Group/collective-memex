---
title: Storage Models Landscape
domain: engineering architecture
status: exploratory (predates requirements/principles analysis)
note: For requirements-driven evaluation, see analysis/system-evaluation.md and analysis/gap-analysis.md
related:
  - "[[core/principles]]"
  - "[[analysis/glossary-engineering]]"
tags:
  - ai-slop
---

# Storage Models for Personal Data

This document surveys storage architectures relevant to personal data operations. Each model has different implications for the principles and requirements identified in our analysis.

---

## Content-Addressed Storage

**What it solves:** Immutability, verifiability, deduplication

**Key implementations:** IPFS, atproto blockstore, Git

**Description:** Data is stored based on its cryptographic hash rather than location. Same content always has same address. Referenced by Content Identifier (CID).

**Principle Alignment:**

- Supports P2 (Temporal Integrity) - immutability enables provenance
- Supports P12 (Provenance Traceability) - content addressing creates verifiable chains
- Conflicts with T11 (To Forget) - deletion requires indirection, not true removal

**Requirements Addressed:**

- R2 (Provenance chain maintenance)
- R23 (Cryptographic verification)

**Requirements Violated:**

- R24 (Irrevocable deletion)

**Tradeoffs:**

- Strengths: Perfect for append-only knowledge capture, natural deduplication, verifiable integrity
- Weaknesses: Deletion/mutation requires indirection layers, GDPR complications, content hash can leak information

**Questions:**

- How do you handle evolving understanding when storage is immutable?
- What is the UX for "I want to update my thinking on X"?

**Related Terms:** See [[analysis/glossary-engineering]] - Content Addressing, CID, CAR Files

---

## Mutable Personal Data Stores

**What it solves:** User control, app portability, familiar mental model

**Key implementations:** Solid Pods, remoteStorage, Fission

**Description:** User owns a data store (pod/vault), apps request permission to read/write specific data. Traditional file/folder paradigm with access control.

**Principle Alignment:**

- Supports P1 (Agent Sovereignty) - user owns and controls data
- Supports P6 (Interoperability) - apps are separate from storage
- Supports P8 (Protection by Default) - access control is built-in
- Weaknesses in P2 (Temporal Integrity) - versioning is add-on, not intrinsic

**Requirements Addressed:**

- R5, R6 (Fine-grained access control)
- R10 (Tool-independent representation)

**Tradeoffs:**

- Strengths: Familiar file/folder mental model, clear ownership boundaries, can actually delete things
- Weaknesses: Sync conflicts in multi-device scenarios, access control complexity, apps must handle schema versioning

**Questions:**

- How fine-grained should access control be?
- What happens when app A and app B have different schemas for "note"?

**Related Terms:** See [[analysis/glossary-engineering]] - Personal Data Server, Pod Architecture

---

## Append-Only Logs / Event Sourcing

**What it solves:** Audit trail, replayability, distributed sync

**Key implementations:** Secure Scuttlebutt, Hypercore, Apache Kafka (enterprise context)

**Description:** All changes are events in an ordered, signed log. Current state is derived by replaying events. Never modifies past events.

**Principle Alignment:**

- Strongly supports P2 (Temporal Integrity) - full history is intrinsic
- Strongly supports P12 (Provenance Traceability) - events form derivation chain
- Supports P11 (Proactive Surfacing) - can analyze patterns across history
- Conflicts with T11 (To Forget) - deletion is "add tombstone event", not removal

**Gap Addressed:**

- GAP-1 (Temporal Integrity) - event sourcing is the primary solution pattern
- GAP-2 (Provenance Traceability) - events create automatic lineage

**Requirements Addressed:**

- R1 (Temporal ordering preservation)
- R2 (Provenance chain maintenance)
- R4 (Time-travel views)

**Requirements Challenged:**

- R24 (Irrevocable deletion)
- R9 (Storage efficiency at scale)

**Tradeoffs:**

- Strengths: Perfect audit trail, time-travel queries possible, natural fit for knowledge evolution
- Weaknesses: Storage grows forever (compaction needed), query complexity (need materialized views), deletion is tombstone not removal

**Questions:**

- Is your thinking process itself valuable to capture, or just current state?
- How do you query across time efficiently?
- Can we have selective amnesia (R24) with append-only architecture?

**Related Terms:** See [[analysis/glossary-engineering]] - Event Sourcing, Append-Only Log, Materialized View

---

## Hybrid Approaches

Real systems often combine multiple models to balance tradeoffs:

**atproto (Bluesky):**

- Content-addressed blocks (immutable) plus mutable pointers (repository head)
- Commit history provides temporal integrity
- Current state is mutable (can update repository)
- Score: 20/30 in [[analysis/system-evaluation]]

**OrbitDB:**

- IPFS (content-addressed) plus CRDT (mutable state)
- Conflict-free replication for multi-device
- Immutable history with mutable current state

**Ceramic:**

- Event streams (append-only) plus content addressing
- Streams provide audit trail
- Content addressing provides verification

**Analysis:** Hybrid approaches attempt to solve the P2 vs T11 tension (temporal integrity vs right to forget) by providing immutable history with mutable current state. However, true deletion remains problematic.

---

## Model Selection Criteria

Based on our principles and requirements:

**Choose Content-Addressed if:**

- Provenance and verification are critical (R23, P12)
- Multi-device sync and deduplication matter
- Deletion is rare or acceptable via indirection

**Choose Mutable Data Store if:**

- Agent sovereignty is paramount (P1)
- Familiar UX is important (adoption)
- True deletion is required (R24, privacy regulations)

**Choose Append-Only/Event Sourcing if:**

- Temporal integrity is essential (P2, GAP-1)
- Audit trail and accountability matter (T5, R2)
- Storage costs are acceptable
- Query complexity can be managed via materialized views

**Choose Hybrid if:**

- You need both history and mutability
- Willing to accept implementation complexity
- Storage model must satisfy conflicting requirements

---

## Open Questions

1. Which model best supports "I changed my mind about this connection"?
2. How do access controls (P8, P10) interact with each storage model?
3. What is the right granularity for personal knowledge - blocks, documents, graphs?
4. Can we have both immutability (for trust, P12) and true deletion (for privacy, R24)?
5. What are acceptable storage costs for decades of append-only personal data?

---

## Cross-References

- [[core/principles]] - How these models satisfy/violate principles
- [[analysis/system-evaluation]] - How real systems score
- [[analysis/gap-analysis]] - GAP-1 (Temporal Integrity)
- [[analysis/glossary-engineering]] - Technical term definitions
- [[context/cases/atproto-analysis]] - Hybrid model case study
