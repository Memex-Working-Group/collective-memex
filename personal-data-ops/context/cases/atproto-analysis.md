---
title: atproto Analysis
domain: case study
status: updated with principle/requirement mappings
related:
  - "[[principles]]"
  - "[[system-evaluation]]"
  - "[[glossary-engineering]]"
system_score: 20/30 (see system-evaluation.md)
tags:
  - ai-slop
author:
  - Sonnet 4.5
---

# AT Protocol Case Study

## Overview

AT Protocol (atproto) is the foundation for Bluesky, a decentralized social network. While designed for social media, its architecture provides valuable patterns for personal data operations.

**Core Architecture:** Personal Data Server (PDS) stores user data, apps access via authenticated API, identity is portable via DIDs.

**Key Insight:** atproto scores 20/30 in our evaluation - the highest of any system reviewed - despite not being designed for personal knowledge management.

---

## Architecture Decisions Mapped to Principles

### Storage: Repository Model (Merkle Search Tree)

**Implementation:**

- Git-like commit model with signed history
- Content-addressed blocks referenced by CID
- Mutable repository head pointing to immutable commits
- Full history preserved in commit chain

**Principle Alignment:**

- Strongly supports P2 (Temporal Integrity) - full versioning intrinsic (Score: 2/2)
- Strongly supports P12 (Provenance Traceability) - cryptographic commit chain (Score: 2/2)
- Supports P1 (Agent Sovereignty) - can self-host PDS (Score: 2/2)
- Conflicts with T11 (To Forget) - deletion via tombstones, not removal

**Requirements Satisfied:**

- R1 (Temporal ordering preservation)
- R2 (Provenance chain maintenance)
- R4 (Time-travel views)
- R23 (Cryptographic verification)

**Requirements Violated:**

- R24 (Irrevocable deletion) - content remains in blocks

**Gaps Addressed:**

- GAP-1 (Temporal Integrity) - Only system with adequate temporal tracking
- GAP-2 (Provenance Traceability) - Automatic lineage via commits

**Related Terms:** See [[glossary-engineering]] - Commit Model, Merkle Tree, Content Addressing, CAR Files

---

### Schema: Lexicon System

**Implementation:**

- Namespaced schemas (reverse domain notation: `app.bsky.feed.post`)
- Versioned independently (breaking changes get new namespace)
- Defined in JSON Schema-like format
- No central approval needed for new lexicons

**Example Lexicon:**

```json
{
  "lexicon": 1,
  "id": "app.bsky.feed.post",
  "defs": {
    "main": {
      "type": "record",
      "key": "tid",
      "record": {
        "type": "object",
        "required": ["text", "createdAt"],
        "properties": {
          "text": { "type": "string", "maxLength": 3000 },
          "createdAt": { "type": "string", "format": "datetime" }
        }
      }
    }
  }
}
```

**Principle Alignment:**

- Strongly supports P4 (Schema Pluralism) - multiple schemas coexist (Score: 2/2)
- Supports P6 (Interoperability) - schemas are portable definitions (Score: 2/2)
- Partially supports P3 (Semantic Richness) - structured but not RDF-level (Score: 1/2)

**Requirements Satisfied:**

- R12 (Schema evolution without data loss)
- R11 (Relation preservation across transformations)

**Questions for Personal Knowledge:**

- Can personal lexicons (e.g., `me.myname.thought.v1`) work alongside public ones?
- How would bidirectional links (core to PKM) be represented in lexicons?

**Related Terms:** See [[glossary-engineering]] - Lexicon System, [[schema-approaches]]

---

### Identity: Decentralized Identifiers (DIDs)

**Implementation:**

- Identity as DID (e.g., `did:plc:xyz...`)
- Separate from PDS location (can migrate providers)
- Handle is user-controlled domain or atproto handle

**Principle Alignment:**

- Strongly supports P1 (Agent Sovereignty) - portable identity (Score: 2/2)
- Supports P6 (Interoperability) - standard DID format (Score: 2/2)

**Requirements Satisfied:**

- R10 (Tool-independent representation)
- R22 (Decadal maintainability) - identity outlives provider

**Implication for Personal Data Ops:**
True data portability. Can switch from provider to self-hosting without losing identity or connections.

**Related Terms:** See [[glossary-engineering]] - DID, DID Document

---

### Access Control: Coarse-Grained

**Implementation:**

- App passwords with scopes (read vs write)
- Repository-level permissions
- No fine-grained per-record access control

**Principle Alignment:**

- Weakly supports P8 (Protection by Default) - basic encryption (Score: 1/2)
- Does not support P10 (Contextual Access) - no per-record ACLs (Score: 0/2)

**Requirements Not Satisfied:**

- R5, R6 (Fine-grained, mnemegram-level access control)
- R7 (Multi-context mnemegrams)
- R32 (Context-based partitioning)

**Gap:**

- GAP-3 (Contextual Access Control) - atproto scores 0/2 here
- Major weakness for personal knowledge with mixed work/personal content

**What Would Be Needed:**

- Per-record ACLs or capability-based access
- Context metadata (work/personal/family)
- Field-level permissions

---

### Federation Model: PDS + Relay + AppView

**Implementation:**

- Personal Data Server (PDS) - stores user data
- Relay - aggregates data from many PDS instances
- AppView - builds indexes for specific applications

**Principle Alignment:**

- Supports P7 (Collective Possibility) - federation enables collaboration (Score: 2/2)
- Weakly supports P11 (Proactive Surfacing) - AppViews can surface content (Score: 1/2)
- Complexity challenges P15 (Graceful Degradation) (Score: 1/2)

**Architectural Insight:**
Separation of storage (PDS) from indexing (AppView) is powerful pattern. Could enable:

- Personal AppView for private analytics
- Different AppViews for different contexts (work vs personal)
- Shared AppViews for collaborative research

**Question:** Can personal knowledge benefit from this pattern even without public federation?

---

## System Evaluation Summary

**Overall Score:** 20/30 (highest of evaluated systems)

**Essential Principles (P1, P6, P8):** 5/6

- P1 (Agent Sovereignty): 2/2
- P6 (Interoperability): 2/2
- P8 (Protection): 1/2

**Strengths:**

1. Temporal integrity and provenance (only adequate system)
2. Portable identity via DIDs
3. Schema evolution via lexicons
4. Open protocol ensures longevity

**Weaknesses:**

1. Public-first design (privacy is add-on)
2. Coarse access control (GAP-3)
3. Not designed for personal knowledge semantics
4. Complex infrastructure (relay/AppView overhead)

**Key Takeaway:** atproto solves GAP-1 and GAP-2 (temporal integrity, provenance) better than any other system, but fails on GAP-3 (contextual access). This suggests hybrid approaches may be needed.

---

## Patterns Applicable to Personal Data Ops

**Adopt from atproto:**

1. Repository model with signed commits for temporal integrity
2. Lexicon system for schema evolution
3. Content addressing for verification and deduplication
4. DID-based identity for portability
5. Separation of storage from indexing/query

**Adapt for personal knowledge:**

1. Add fine-grained access control (per-mnemegram, not per-repository)
2. Support private-first with optional sharing (inverse of atproto)
3. Semantic richness beyond lexicons (typed relations, inference)
4. Personal AppViews without requiring public federation
5. True deletion capability for sensitive content

**What atproto Teaches:**

- Commit model solves temporal integrity (GAP-1)
- Cryptographic signing solves provenance (GAP-2)
- Hybrid storage (content-addressed + mutable pointers) balances needs
- Infrastructure complexity is acceptable tradeoff for sovereignty

---

## Open Questions

1. Can personal PDS run with private lexicons unknown to public network?
2. How would bidirectional links (essential for PKM) work in atproto?
3. Can AppView pattern work for purely local personal analytics?
4. What would fine-grained access control look like in this architecture?
5. Can repository model accommodate true deletion (R24) while preserving history?

---

## Technical Specifications

**Storage Format:** CAR files (Content Addressable aRchives)
**Signing:** K256 elliptic curve signatures  
**Synchronization:** WebSocket firehose + repository checkout
**API:** XRPC (HTTP-based RPC)
**Query:** AppView-specific, no standard query language

---

## References

**Protocol Documentation:**

- Main docs: https://atproto.com/
- Lexicon guide: https://atproto.com/guides/lexicon
- Repository spec: https://atproto.com/specs/repository

**Related Analysis:**

- [[system-evaluation]] - Complete scoring methodology
- [[gap-analysis]] - Which gaps atproto addresses
- [[storage-models]] - Repository as hybrid storage
- [[schema-approaches]] - Lexicons as schema approach
- [[glossary-engineering]] - Technical terms used

---

## Comparison with Other Systems

**vs Solid (19/30):**

- atproto: Better temporal integrity, worse semantic richness
- Solid: Better access control (WAC), worse performance

**vs Obsidian (18/30):**

- atproto: Better provenance/versioning, more complex infrastructure
- Obsidian: Better sovereignty (local files), simpler

**vs Roam (11/30):**

- atproto: Portable identity, open protocol
- Roam: Better proactive surfacing, vendor lock-in

**Conclusion:** atproto demonstrates that temporal integrity and provenance (GAP-1, GAP-2) can be solved, but at cost of infrastructure complexity. Personal data ops needs similar patterns adapted for private-first, semantically-rich knowledge management.
