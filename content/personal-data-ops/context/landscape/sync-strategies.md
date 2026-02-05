---
title: Synchronization Strategies
domain: engineering architecture
status: analysis-driven
note: Addresses P1 (Agent Sovereignty), P15 (Graceful Degradation), local-first requirements
related:
  - "[[core/principles]]"
  - "[[analysis/gap-analysis]]"
  - "[[analysis/glossary-engineering]]"
tags:
  - ai-slop
---

# Synchronization Strategies for Personal Data

This document surveys synchronization architectures for personal data operations. Sync strategy directly impacts P1 (Agent Sovereignty), P15 (Graceful Degradation), and local-first viability.

---

## The Synchronization Challenge

**Core Problem:** Multi-device access to personal knowledge requires sync. How do you keep local copies consistent without sacrificing sovereignty or offline capability?

**Requirements Implicated:**

- R22: Decadal maintainability (not dependent on company)
- R27: Offline and under-duress protection
- R40: Privacy-preserving local processing

**Principles:**

- P1 (Agent Sovereignty): Must work without central authority
- P15 (Graceful Degradation): Must work offline
- P9 (Performance): Sync must be efficient at scale

**Tensions:**

- Offline capability vs real-time collaboration
- Simplicity vs conflict resolution sophistication
- Privacy vs convenience (cloud sync services)

---

## Centralized Server Sync

**Description:** All devices sync through central server. Server holds authoritative state.

**Architecture:**

```
Device A ←→ Central Server ←→ Device B
              (source of truth)
```

**How It Works:**

1. Devices push changes to server
2. Server resolves conflicts (last-write-wins or custom logic)
3. Other devices pull changes from server

**Principle Alignment:**

- Violates P1 (Agent Sovereignty) - requires trust in server
- Violates P15 (Graceful Degradation) - breaks offline
- Supports P9 (Performance) - simple, well-understood

**Requirements Violated:**

- R22 (Decadal maintainability) - depends on company
- R27 (Offline operation) - requires connectivity

**Strengths:**

- Simple mental model
- One source of truth (no conflicts)
- Easy to implement
- Battle-tested (Dropbox, Google Drive)

**Weaknesses:**

- Single point of failure
- Vendor lock-in
- Privacy concerns (data on server)
- Doesn't work offline
- Requires ongoing service

**Examples:**

- Notion, Roam Research (fail on P1)
- Google Drive, Dropbox (convenient but not sovereign)

**Use for Personal Data Ops:**
Not recommended for primary sync. Acceptable only as:

- Backup destination (in addition to local)
- Optional convenience (not required)
- Encrypted blob storage (server can't read)

---

## Peer-to-Peer Sync

**Description:** Devices sync directly with each other, no central server.

**Architecture:**

```
Device A ←→ Device B
    ↕           ↕
Device C ←→ Device D
```

**How It Works:**

1. Devices discover each other (mDNS, DHT, manual)
2. Exchange changes directly
3. Merge using CRDT or OT algorithm

**Principle Alignment:**

- Strongly supports P1 (Agent Sovereignty) - no central authority
- Strongly supports P15 (Graceful Degradation) - works offline, syncs when possible
- Moderate P9 (Performance) - discovery overhead, variable network

**Requirements Addressed:**

- R22 (Decadal maintainability) - no company dependency
- R27 (Offline operation) - fully functional offline
- R40 (Privacy-preserving) - data never leaves devices

**Strengths:**

- True agent sovereignty
- No vendor dependency
- Works offline
- Privacy (data on your devices only)
- No recurring costs

**Weaknesses:**

- Discovery complexity
- NAT traversal challenges
- Sync only when devices can reach each other
- No "sync while I'm away from all devices"
- Complex conflict resolution

**Examples:**

- Syncthing (file sync)
- Secure Scuttlebutt (social, append-only)
- BitTorrent Sync (files)

**Use for Personal Data Ops:**
Strong candidate for P1/P15 compliance. Challenges:

- Mobile devices (battery, intermittent connectivity)
- Discovery (how do devices find each other?)
- Initial sync for new device

**Enhancement:** Hybrid P2P + optional relay server

---

## CRDT-Based Sync (Conflict-Free Replicated Data Types)

**Description:** Data structures that can be modified concurrently on multiple devices and merged without conflicts.

**How It Works:**

1. Each edit generates CRDT operation
2. Operations commute (order doesn't matter)
3. Devices exchange operations
4. Merge is automatic and deterministic

**CRDT Types:**

- **State-based (CvRDT):** Send entire state, merge function
- **Operation-based (CmRDT):** Send operations, apply in any order
- **Delta-based:** Send state changes (efficient)

**Principle Alignment:**

- Strongly supports P1 (Agent Sovereignty) - no central authority needed
- Strongly supports P15 (Graceful Degradation) - offline-first by design
- Good P9 (Performance) - efficient for most operations

**Requirements Addressed:**

- R27 (Offline operation) - designed for offline-first
- R22 (Decadal maintainability) - algorithm-based, not service

**Strengths:**

- Automatic conflict resolution
- Mathematical correctness (convergence guaranteed)
- Offline-first by design
- No coordination needed
- Well-understood algorithms

**Weaknesses:**

- Cannot represent all operations (constraints hard)
- Deletion is complex (tombstones)
- Some CRDTs have large overhead
- Merge can produce unexpected results
- Not intuitive for users

**CRDT Flavors:**

**Last-Write-Wins (LWW):**

- Simplest CRDT
- Each field has timestamp
- Latest write wins
- Problem: Concurrent edits lose data

**Observed-Remove Set (OR-Set):**

- For sets (tags, links)
- Add wins over remove
- Preserves concurrent adds

**Conflict-Free Replicated JSON (Automerge, Yjs):**

- Full document CRDTs
- Handle complex data structures
- Used by collaborative editors

**Examples:**

- Automerge (CRDT library for JSON)
- Yjs (CRDT for text and rich data)
- Roshi (Twitter's CRDT store)

**Use for Personal Data Ops:**
Excellent for:

- Text documents (Yjs handles collaborative editing)
- Sets (tags, links)
- Counters (reference counts)

Challenging for:

- Constraints ("this field must be unique")
- Complex validation
- Operations needing coordination

**Recommendation:** Use CRDTs for data layer, add validation layer above if needed.

---

## Operational Transform (OT)

**Description:** Algorithm for merging concurrent edits by transforming operations relative to each other.

**How It Works:**

1. Device A makes edit op1
2. Device B makes concurrent edit op2
3. Transform op1 relative to op2 (and vice versa)
4. Apply transformed operations

**Principle Alignment:**

- Supports P1 (Agent Sovereignty) - can work decentralized
- Moderate P15 (Graceful Degradation) - typically needs coordination
- Good P9 (Performance) - efficient for text

**Strengths:**

- Natural for text editing
- Used by Google Docs (proven at scale)
- Intention-preserving (maintains user intent)

**Weaknesses:**

- Requires central server (typical implementation)
- Complex algorithm (correctness hard to prove)
- Doesn't naturally generalize beyond text

**Examples:**

- Google Docs
- ShareDB (OT framework)
- Etherpad

**Use for Personal Data Ops:**
Less suitable than CRDTs because:

- Most implementations require server
- CRDTs have better theoretical foundation
- CRDTs handle more data types

Consider OT only if:

- Real-time collaborative editing is priority
- Text is primary data type
- Willing to accept server dependency

---

## Git-Style Sync (Merkle DAG)

**Description:** Commit-based sync with branching and merging, like version control.

**How It Works:**

1. Changes bundled into signed commits
2. Commits form directed acyclic graph (DAG)
3. Devices exchange commits
4. Merge creates new commit with multiple parents
5. Conflicts handled explicitly (user resolves)

**Principle Alignment:**

- Strongly supports P2 (Temporal Integrity) - full history preserved
- Strongly supports P12 (Provenance) - commits are provenance
- Supports P1 (Agent Sovereignty) - decentralized by design
- Supports P15 (Graceful Degradation) - offline-first

**Requirements Addressed:**

- R1, R2, R4 (Temporal, provenance, time-travel) - Git excels here
- R23 (Cryptographic verification) - commits are signed
- R22 (Decadal maintainability) - Git outlives companies

**Strengths:**

- Full history (addresses GAP-1)
- Branching and merging
- Cryptographic verification
- Proven at massive scale
- Offline-first
- No vendor dependency

**Weaknesses:**

- Conflicts require manual resolution
- Complex for non-technical users
- Text-oriented (binary diffs poor)
- Merge conflicts in concurrent edits

**Examples:**

- Git (version control)
- atproto (social, uses MST + commits)
- Fossil (distributed VCS with additional features)

**Use for Personal Data Ops:**
Excellent for:

- Knowledge as text files (Markdown, Org-mode)
- When history is important
- Technical users comfortable with Git

Challenging for:

- Rich data structures (JSON, databases)
- Non-technical users
- Real-time collaboration (conflicts)

**Enhancement:** Git + CRDT (use CRDT for conflict resolution)

---

## Event Sourcing Sync

**Description:** Sync events (not state). Replay events to reconstruct state.

**How It Works:**

1. All changes are events in append-only log
2. Each device has event log
3. Devices exchange events
4. Replay events to derive current state
5. Events are immutable, totally ordered per device

**Principle Alignment:**

- Strongly supports P2 (Temporal Integrity) - events are history
- Strongly supports P12 (Provenance) - event chains
- Supports P1 (Agent Sovereignty) - decentralized
- Supports P15 (Graceful Degradation) - offline replay

**Requirements Addressed:**

- GAP-1 (Temporal Integrity) - event sourcing is primary solution
- R1, R2, R4 (Temporal, provenance, time-travel)

**Strengths:**

- Perfect audit trail
- Time-travel built-in
- Natural for multi-device (events are facts)
- Can rebuild state from events

**Weaknesses:**

- Storage grows forever (need compaction)
- Query complexity (need materialized views)
- Eventual consistency (not immediate)
- Events cannot be deleted (tombstones only)

**Examples:**

- Secure Scuttlebutt (social, gossip protocol)
- Apache Kafka (enterprise event streaming)
- EventStore (event sourcing database)

**Use for Personal Data Ops:**
Excellent when:

- Temporal integrity is priority (GAP-1)
- Audit trail needed
- Willing to manage storage
- Can handle eventual consistency

**Challenge:** Compaction (how do you prune old events without losing history?)

---

## Hybrid Approaches

Real systems often combine strategies:

**Git + CRDT:**

- Git for commit history
- CRDT for automatic conflict resolution
- Example: Could enhance Obsidian

**P2P + Optional Relay:**

- P2P when devices can reach each other
- Relay server when direct connection fails
- Example: Syncthing supports relays

**Local + Cloud Backup:**

- Primary: Local sync (CRDT or Git)
- Backup: Encrypted blobs to cloud
- Example: Keybase file system

**Event Sourcing + Snapshots:**

- Events for precision
- Periodic snapshots for performance
- Compact old events
- Example: Some CQRS systems

---

## Comparison Matrix

| Strategy       | P1 Sovereignty | P15 Offline | P2 Temporal | Complexity | Conflict Handling    |
| -------------- | -------------- | ----------- | ----------- | ---------- | -------------------- |
| Centralized    | Low            | Low         | Low         | Low        | Server decides       |
| P2P            | High           | High        | Medium      | High       | Manual/CRDT          |
| CRDT           | High           | High        | Medium      | Medium     | Automatic            |
| OT             | Medium         | Medium      | Low         | High       | Transformation       |
| Git            | High           | High        | High        | High       | Manual merge         |
| Event Sourcing | High           | High        | High        | High       | Eventual consistency |

---

## Recommendations by Context

**For Solo User, Multiple Devices:**

- **Git** (if technical, text-focused)
- **CRDT** (if non-technical, rich data)
- Avoid: Centralized (unnecessary dependency)

**For Family/Small Group:**

- **CRDT** (automatic conflict resolution)
- **P2P + Relay** (privacy + convenience)
- Avoid: Manual merge (non-technical users)

**For Research Collaboration:**

- **Git** (academic norm, branching useful)
- **Event Sourcing** (audit trail matters)
- Consider: Hybrid Git+CRDT

**For Maximum Sovereignty:**

- **P2P + CRDT** (no servers, automatic merge)
- **Git** (if willing to manage conflicts)
- Must avoid: Centralized

**For Maximum History/Provenance:**

- **Event Sourcing** (perfect audit trail)
- **Git** (commit history)
- **CRDT** (less history detail)

---

## Implementation Considerations

**Network Assumptions:**

- Reliable: Can use state-based CRDTs
- Unreliable: Need operation-based or event-based
- Offline-first: CRDT, Git, Event Sourcing

**Conflict Philosophy:**

- Avoid conflicts: Centralized
- Automatic resolution: CRDT
- Manual resolution: Git
- Eventual consistency: Event Sourcing

**Storage Costs:**

- Low (state only): Centralized, CRDT (state-based)
- Medium (recent history): CRDT (op-based)
- High (full history): Git, Event Sourcing

**Performance:**

- Initial sync: Large for full history (Git, Event Sourcing)
- Ongoing: Efficient for ops-based (CRDT, Event)
- Conflict resolution: Expensive for OT, cheap for CRDT

---

## Open Questions

1. Can CRDT handle rich knowledge graph operations reliably?
2. How do you compact event logs without losing essential provenance?
3. What's the right sync granularity (document, assertion, field)?
4. Can Git-style sync work for non-technical users with better UX?
5. How do you sync across decades (storage implications)?
6. What's the migration path from centralized to sovereign sync?

---

## Cross-References

- [[core/principles]] - P1 (Sovereignty), P15 (Graceful Degradation), P2 (Temporal)
- [[analysis/gap-analysis]] - GAP-1 (Event sourcing addresses temporal integrity)
- [[analysis/glossary-engineering]] - CRDT, OT, Event Sourcing definitions
- [[context/landscape/storage-models]] - Storage affects sync strategy
- [[context/cases/atproto-analysis]] - Git-style sync in practice
