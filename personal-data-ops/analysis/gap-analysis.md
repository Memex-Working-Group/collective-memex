---
title: Gap Analysis - Universal Weaknesses in Personal Data Operations
status: draft
created: 2025-02-05T00:00:00.000Z
derived_from:
  - "[[system-evaluation]]"
related:
  - "[[principles]]"
  - "[[requirements]]"
tags:
  - ai-slop
author:
  - Sonnet 4.5
uuid: bd28402a-45ea-40dd-bac2-b61010e5d06b
share: false
---
# Gap Analysis

This document identifies systemic gaps in current personal data operations implementations, derived from evaluating 5 major systems against our principles.

**Methodology:** Cross-system analysis identifying principles that _no_ system adequately addresses.

---

## Critical Gaps (P2 Scores Across All Systems)

These are must-have principles where ALL evaluated systems are weak.

### GAP-1: Temporal Integrity (P2)

**Scores:** Obsidian (0), Roam (1), atproto (2), Solid (0), Notion (1)
**Only adequate implementation:** atproto

**The Problem:**
Most personal knowledge systems treat time as an afterthought. Version history is external (git), limited (recent changes only), or non-existent. Understanding how knowledge evolved - "what did I think when?" - is core to reflection but unsupported.

**Why This Matters:**

- Can't trace conceptual evolution (UC-1)
- Can't do time-travel queries (R4)
- Can't maintain provenance chains (R2)
- Reflection (T7) is crippled

**What's Missing:**

- Immutable or append-only storage models
- First-class versioning at mnemegram level
- Temporal indexing for "state at time T" queries
- Automatic timestamp precision

**Engineering Implications:**

- Need event sourcing or commit-based storage
- Need temporal indexes in query layer
- Need UI for time-travel exploration

**Who Gets It Right:**

- **atproto**: MST with signed commits, full history
- **Git** (as external tool): Commit model with branching

---

### GAP-2: Provenance Traceability (P12)

**Scores:** Obsidian (0), Roam (0), atproto (2), Solid (1), Notion (0)
**Only adequate implementation:** atproto

**The Problem:**
Where did this mnemegram come from? What influenced it? What did it influence? These are basic questions, but almost no system tracks provenance automatically. It's left to manual tagging or external tools.

**Why This Matters:**

- Can't trace information genealogy (UC-15)
- Can't distinguish AI-generated vs human content (R55)
- Can't link decisions to outcomes (R82)
- Accountability (T5) is impossible

**What's Missing:**

- Automatic capture of derivation chains
- "Generated from" relationships
- Source attribution for ingested content
- Clear marking of AI vs human authorship

**Engineering Implications:**

- Need graph model with derivation edges
- Need metadata on all mnemegrams: created_by, derived_from, influenced_by
- Need UI for provenance visualization

**Who Gets It Right:**

- **atproto**: Cryptographic commits create provenance chain
- **Scientific notebooks**: Lab notebooks have provenance by practice

---

### GAP-3: Contextual Access Control (P10)

**Scores:** Obsidian (0), Roam (0), atproto (0), Solid (2), Notion (2)
**Adequate implementations:** Solid, Notion (but vendor-locked)

**The Problem:**
Most personal knowledge systems are either all-private (Obsidian) or all-shared (Roam workspace). Mnemegrams that exist in multiple contexts (work/personal) have no way to express "this colleague can see my work notes but not my personal journal."

**Why This Matters:**

- Can't share subsets selectively (UC-2)
- Can't partition work/personal (UC-8)
- Can't do contextual AI access (UC-12)
- Communion (T9) requires trust boundaries

**What's Missing:**

- Fine-grained ACLs at mnemegram level
- Context metadata (work, personal, family, etc.)
- Capability-based delegation
- Temporal access grants (expire after condition)

**Engineering Implications:**

- Need ACL system or capability tokens
- Need context as first-class metadata
- Need policy evaluation engine
- Need audit logs

**Who Gets It Right:**

- **Solid**: WAC (Web Access Control) with per-resource ACLs
- **Notion**: Granular workspace permissions (but proprietary)

---

### GAP-4: Proactive Surfacing (P11)

**Scores:** Obsidian (1), Roam (2), atproto (1), Solid (0), Notion (0)
**Only adequate implementation:** Roam

**The Problem:**
Most systems are query-driven: you ask, system responds. But valuable knowledge often isn't retrieved because you don't know to ask. Proactive surfacing - "here's something relevant you didn't ask for" - is rare.

**Why This Matters:**

- Can't discover non-obvious connections (R17)
- Can't get relationship maintenance reminders (UC-10)
- Can't surface patterns without explicit query (UC-17)
- Orientation (T4) suffers

**What's Missing:**

- Recommendation engines based on context
- Anomaly detection ("this is unusual")
- Time-based triggers ("you haven't reviewed X in 3 months")
- Pattern recognition ("you always feel better after Y")

**Engineering Implications:**

- Need background computation for recommendations
- Need pattern detection algorithms
- Need context awareness (what's the agent doing now?)
- Need push notification system

**Who Gets It Right:**

- **Roam**: Linked references sidebar, query embeds
- **Modern email**: "Smart compose" suggestions

---

## Significant Gaps (Majority of Systems Weak)

### GAP-5: Heterogeneous Integration (P13)

**Scores:** Obsidian (1), Roam (0), atproto (0), Solid (2), Notion (1)

**The Problem:**
Personal knowledge spans text, images, locations, biometrics, communications. Most systems are text-first with media as attachments. Cross-type queries ("where was I when I wrote about X?") are impossible.

**What's Missing:**

- Unified graph across data types
- Entity resolution (same person across systems)
- Spatiotemporal queries
- Biometric-knowledge correlation

**Engineering Implications:**

- Need polymorphic node types in graph
- Need cross-type indexing
- Need query language spanning modalities

---

### GAP-6: Collective Possibility (P7)

**Scores:** Obsidian (0), Roam (1), atproto (2), Solid (1), Notion (2)

**The Problem:**
Personal knowledge systems are designed for individuals. Multi-generational memory (UC-5), collaborative research (UC-14), family archives need multi-agent models but most systems bolt collaboration on afterward.

**What's Missing:**

- Clear attribution (who said what)
- Consensus mechanisms
- Personal vs shared mnemegram distinction
- Generational handoff (beyond creator lifetime)

**Engineering Implications:**

- Need multi-agent authorship model
- Need assertions with agent attribution
- Need merge/fork operations
- Need permission models that include "family" or "team"

---

### GAP-7: Friction Minimization (P5)

**Scores:** Obsidian (1), Roam (2), atproto (1), Solid (0), Notion (2)

**The Problem:**
Comprehensive memex requires capturing everything, but manual entry doesn't scale. Automation and integration are afterthoughts, not core features. Data exhaust goes uncaptured.

**What's Missing:**

- Passive capture from communication platforms
- Automated biometric/location logging
- Browser history integration
- Low-friction mobile capture

**Engineering Implications:**

- Need API integrations as first-class
- Need background capture processes
- Need mobile-first capture UX
- Need tolerance for messy, unstructured input

---

## Architectural Patterns Missing from All Systems

### PATTERN-1: Event Sourcing for Personal Knowledge

**No system uses event sourcing** for personal knowledge management, yet it solves multiple gaps:

- Temporal integrity (GAP-1): Full history by design
- Provenance (GAP-2): Events form derivation chain
- Audit (T5): Every change is event

**Why Not Adopted:**

- Query complexity (need materialized views)
- Storage costs (every edit = new event)
- Unfamiliar to PKM community

**Potential:**

- Combine event stream with current-state cache
- Use CRDTs for multi-device sync
- Enable "replay" for understanding evolution

---

### PATTERN-2: Capability-Based Sharing

**Only atproto hints at this** (with its token model), but nobody does full capability-based access control for personal knowledge.

**What It Would Enable:**

- Granular delegation (R25)
- Time-limited sharing
- Revocable access without centralized server
- "Give this AI access to these 10 mnemegrams for this task"

**Why Not Adopted:**

- Complexity of implementation
- UX challenges (managing capabilities)
- PKM tools prioritize simplicity

**Potential:**

- Use UCAN (User Controlled Authorization Networks)
- Capabilities as shareable tokens
- Eliminates need for centralized ACL server

---

### PATTERN-3: Federated Personal Data Servers

**atproto and Solid both attempt this,** but neither is designed for personal knowledge:

- atproto: Social-first, not knowledge-first
- Solid: Too complex, poor performance

**What's Missing:**

- PDS designed for personal knowledge graph, not social posts
- Efficient query federation
- Standardized personal knowledge schemas (lexicons)

**Potential:**

- Personal data server that speaks both atproto and Solid protocols
- AppViews specialized for personal knowledge (not social feeds)
- Local-first PDS with optional federation

---

### PATTERN-4: Hybrid Storage (Immutable + Mutable)

**atproto does this** (content-addressed blocks + mutable pointers), but others don't:

- Obsidian: Pure mutable (files on disk)
- Roam: Mutable cloud database
- Solid: Mutable pods

**What Hybrid Enables:**

- Immutability for provenance/history
- Mutability for "current state" UX
- Content deduplication
- Cryptographic verification

**Potential:**

- IPFS or similar for immutable content
- Mutable indexes pointing to immutable blocks
- Best of both worlds

---

### PATTERN-5: Context-Aware Indexing

**Nobody does this well.** Indexing is either:

- Full-text (Obsidian, Notion)
- Graph-based (Roam, limited)
- Triple-store (Solid, slow)

**What Context-Aware Would Enable:**

- "Find notes written when I was in NYC"
- "Show me mnemegrams from anxious periods"
- "What was I working on during Q3 2023?"

**Missing Technical Pieces:**

- Spatiotemporal indexes
- Emotional/mental state as index dimension
- Multi-dimensional query language

---

## Priority Gaps for Experimentation

Based on:

1. How many use cases affected
2. How many requirements unsatisfied
3. How many principles violated
4. Feasibility of improvement

### HIGHEST PRIORITY

**P1: Temporal Integrity + Provenance (GAP-1 + GAP-2)**

- Affects: 8 use cases, 15 requirements, 2 principles
- Current state: Only atproto adequate
- Experiment: Event-sourced personal knowledge store
- Technology: Append-only log (SSB-style) or commit model (atproto-style)

### HIGH PRIORITY

**P2: Contextual Access Control (GAP-3)**

- Affects: 5 use cases, 12 requirements, 2 principles
- Current state: Only Solid + Notion (vendor-locked)
- Experiment: Capability-based sharing for personal knowledge
- Technology: UCAN, Macaroons, or custom capability system

### MEDIUM PRIORITY

**P3: Proactive Surfacing (GAP-4)**

- Affects: 4 use cases, 6 requirements, 1 principle
- Current state: Only Roam adequate
- Experiment: Recommendation engine for personal knowledge
- Technology: Graph algorithms, pattern matching, LLM embeddings

### LOWER PRIORITY (But Important)

**P4: Heterogeneous Integration (GAP-5)**
**P5: Friction Minimization (GAP-7)**
**P6: Collective Possibility (GAP-6)**

---

## Questions for the Working Group

1. **Which gaps matter most to your use cases?**
2. **Are there systems we didn't evaluate that address these gaps?**
3. **Which experiments should we prioritize?**
4. **What existing technologies could be adapted?** (e.g., Git for temporal integrity, UCAN for access control)

---

## Cross-References

- [[system-evaluation]] - Detailed scoring of 5 systems
- [[principles]] - 15 principles these gaps violate
- [[requirements]] - Specific requirements unsatisfied
- [[glossary-engineering]] - Technical terms for solutions