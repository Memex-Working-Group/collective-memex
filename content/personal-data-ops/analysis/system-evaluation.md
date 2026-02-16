---
title: System Evaluation Against Principles
status: draft
created: 2025-02-05
evaluated_systems: Obsidian, Roam Research, atproto, Solid, Notion
scoring: 0 (not addressed), 1 (partially), 2 (fully)
related:
  - "[[principles]]"
  - "[[requirements]]"
tags:
  - ai-slop
author:
  - Sonnet 4.5
---

# System Evaluation Against Principles

This document evaluates existing personal knowledge and data systems against the 15 architectural principles derived from our requirements analysis.

**Scoring:** 0 (not addressed), 1 (partially addressed), 2 (fully addressed)
**Minimum Viable:** P1, P6, P8 must score ≥2
**High Quality:** ≥12/15 principles score ≥1

---

## Systems Evaluated

1. **Obsidian** - Local-first markdown notes with graph view
2. **Roam Research** - Cloud-based networked thought tool
3. **atproto (Bluesky)** - Decentralized social protocol with personal data servers
4. **Solid** - Decentralized data pods with RDF
5. **Notion** - Cloud-based workspace/database hybrid

---

## Obsidian Evaluation

### Scores by Principle

| Principle                      | Score | Rationale                                               |
| ------------------------------ | ----- | ------------------------------------------------------- |
| P1: Agent Sovereignty          | 2     | Full control - local files, no vendor lock              |
| P2: Temporal Integrity         | 0     | No built-in versioning, relies on git                   |
| P3: Semantic Richness          | 1     | Links exist but untyped, no formal relations            |
| P4: Schema Pluralism           | 2     | Markdown = schema-on-read, frontmatter flexible         |
| P5: Friction Minimization      | 1     | Manual capture, some plugins for automation             |
| P6: Interoperability           | 2     | Plain markdown, portable by design                      |
| P7: Collective Possibility     | 0     | Single-user focused, publish is afterthought            |
| P8: Protection by Default      | 1     | Local files = private, but no encryption, no ACLs       |
| P9: Performance Pragmatism     | 2     | Fast local search and graph rendering                   |
| P10: Contextual Access         | 0     | No access control system                                |
| P11: Proactive Surfacing       | 1     | Backlinks, graph view, but no proactive recommendations |
| P12: Provenance Traceability   | 0     | No automatic provenance tracking                        |
| P13: Heterogeneous Integration | 1     | Plugins for various data types, but not unified         |
| P14: Longevity Over Features   | 2     | Markdown will outlive Obsidian                          |
| P15: Graceful Degradation      | 2     | Fully offline, no dependencies                          |

**Total Score: 18/30 (60%)**
**Essential Principles (P1, P6, P8):** 5/6 (P8 only partial)

**Strengths:**

- True agent sovereignty (local files)
- Maximum interoperability (plain text)
- Offline-first
- Long-term viable format

**Weaknesses:**

- No temporal tracking without external tools
- Relations are implicit, not semantic
- No collaboration model
- No automatic provenance
- No access control

**Engineering Terms Implicated:**

- Local-first architecture
- Markdown serialization
- Graph rendering (in-memory)
- File-system-based storage

---

## Roam Research Evaluation

### Scores by Principle

| Principle                      | Score | Rationale                                             |
| ------------------------------ | ----- | ----------------------------------------------------- |
| P1: Agent Sovereignty          | 0     | Cloud-dependent, vendor lock-in, export limited       |
| P2: Temporal Integrity         | 1     | Has version history but not comprehensive             |
| P3: Semantic Richness          | 1     | Block-level granularity, but relations untyped        |
| P4: Schema Pluralism           | 2     | Highly flexible, attributes emergent                  |
| P5: Friction Minimization      | 2     | Excellent quick capture, daily notes                  |
| P6: Interoperability           | 0     | Proprietary format, export is JSON/markdown but lossy |
| P7: Collective Possibility     | 1     | Multi-user but same workspace, not selective sharing  |
| P8: Protection by Default      | 1     | Encrypted at rest, but coarse access control          |
| P9: Performance Pragmatism     | 1     | Can slow with large graphs                            |
| P10: Contextual Access         | 0     | Workspace-level permissions only                      |
| P11: Proactive Surfacing       | 2     | Excellent - linked references, sidebar, queries       |
| P12: Provenance Traceability   | 0     | No explicit provenance chains                         |
| P13: Heterogeneous Integration | 0     | Primarily text, limited media handling                |
| P14: Longevity Over Features   | 0     | Company-dependent, proprietary                        |
| P15: Graceful Degradation      | 0     | Cannot work offline                                   |

**Total Score: 11/30 (37%)**
**Essential Principles (P1, P6, P8):** 1/6 - **Fails minimum viability**

**Strengths:**

- Excellent capture friction
- Strong proactive surfacing
- Schema flexibility
- Block-level granularity

**Weaknesses:**

- Vendor lock-in (critical failure)
- No true portability
- No offline mode
- No individual sovereignty
- Requires company survival

**Engineering Terms Implicated:**

- Block-based storage
- Graph database (proprietary)
- Real-time sync
- Workspace model

---

## atproto (Bluesky) Evaluation

### Scores by Principle

| Principle                      | Score | Rationale                                              |
| ------------------------------ | ----- | ------------------------------------------------------ |
| P1: Agent Sovereignty          | 2     | Can host own PDS, portable identity                    |
| P2: Temporal Integrity         | 2     | Commit history, signed records, full provenance        |
| P3: Semantic Richness          | 1     | Lexicons provide structure but not RDF-level semantics |
| P4: Schema Pluralism           | 2     | Lexicon system designed for schema evolution           |
| P5: Friction Minimization      | 1     | Good for posting, less for general capture             |
| P6: Interoperability           | 2     | DID-based identity, CAR file exports, open protocol    |
| P7: Collective Possibility     | 2     | Federation model, multi-user by design                 |
| P8: Protection by Default      | 1     | Public-first design, privacy is add-on                 |
| P9: Performance Pragmatism     | 1     | Relay/AppView model scales, but complex                |
| P10: Contextual Access         | 0     | Coarse permissions (public/private/mentions)           |
| P11: Proactive Surfacing       | 1     | AppViews can surface, but not personal context         |
| P12: Provenance Traceability   | 2     | Cryptographic commits, full history                    |
| P13: Heterogeneous Integration | 0     | Designed for social, not general knowledge             |
| P14: Longevity Over Features   | 2     | Open protocol, decentralized                           |
| P15: Graceful Degradation      | 1     | PDS can run locally but relay-dependent for discovery  |

**Total Score: 20/30 (67%)**
**Essential Principles (P1, P6, P8):** 5/6

**Strengths:**

- True decentralization with portable identity
- Excellent temporal integrity (commits, signatures)
- Schema evolution built-in (lexicons)
- Open protocol ensures longevity
- Strong provenance model

**Weaknesses:**

- Public-first, not designed for personal/private knowledge
- Coarse access control
- Not designed for heterogeneous personal data
- Complex infrastructure (relay, AppView)

**Engineering Terms Implicated:**

- Content-addressed storage (CID, CAR files)
- Merkle Search Tree (MST)
- Decentralized Identifiers (DID)
- Lexicon system
- Repository model
- Federation architecture
- Cryptographic signing (K256)

---

## Solid Evaluation

### Scores by Principle

| Principle                      | Score | Rationale                                          |
| ------------------------------ | ----- | -------------------------------------------------- |
| P1: Agent Sovereignty          | 2     | Pod ownership, can self-host                       |
| P2: Temporal Integrity         | 0     | No built-in versioning                             |
| P3: Semantic Richness          | 2     | RDF enables full semantic web                      |
| P4: Schema Pluralism           | 2     | RDF accommodates any schema                        |
| P5: Friction Minimization      | 0     | High friction, complex to use                      |
| P6: Interoperability           | 2     | RDF is maximally interoperable                     |
| P7: Collective Possibility     | 1     | Multi-user but complex permission model            |
| P8: Protection by Default      | 2     | Fine-grained ACLs, per-resource permissions        |
| P9: Performance Pragmatism     | 0     | RDF query performance is poor at scale             |
| P10: Contextual Access         | 2     | WAC (Web Access Control) supports contextual rules |
| P11: Proactive Surfacing       | 0     | No surfacing mechanisms                            |
| P12: Provenance Traceability   | 1     | Can be modeled in RDF but not automatic            |
| P13: Heterogeneous Integration | 2     | RDF handles any data type                          |
| P14: Longevity Over Features   | 2     | W3C standard, open                                 |
| P15: Graceful Degradation      | 1     | Can work offline but complex                       |

**Total Score: 19/30 (63%)**
**Essential Principles (P1, P6, P8):** 6/6 - **Meets minimum viability**

**Strengths:**

- True agent sovereignty (pod ownership)
- Maximum semantic richness (RDF)
- Fine-grained access control
- Standard-based interoperability
- Handles all data types

**Weaknesses:**

- Performance issues at scale (SPARQL is slow)
- Extremely high friction for users
- No temporal tracking built-in
- No proactive surfacing
- Complexity barrier

**Engineering Terms Implicated:**

- RDF (Resource Description Framework)
- SPARQL query language
- Web Access Control (WAC)
- Linked Data Platform (LDP)
- Turtle/JSON-LD serialization
- Pod architecture
- Triple store

---

## Notion Evaluation

### Scores by Principle

| Principle                      | Score | Rationale                                          |
| ------------------------------ | ----- | -------------------------------------------------- |
| P1: Agent Sovereignty          | 0     | Cloud-only, vendor lock-in                         |
| P2: Temporal Integrity         | 1     | Has version history but limited                    |
| P3: Semantic Richness          | 1     | Databases have relations but proprietary           |
| P4: Schema Pluralism           | 2     | Flexible databases, properties evolve              |
| P5: Friction Minimization      | 2     | Excellent capture UX                               |
| P6: Interoperability           | 0     | Proprietary, export is lossy                       |
| P7: Collective Possibility     | 2     | Strong collaboration features                      |
| P8: Protection by Default      | 1     | Enterprise security but trust required             |
| P9: Performance Pragmatism     | 1     | Good for documents, struggles with large databases |
| P10: Contextual Access         | 2     | Granular permissions, contextual sharing           |
| P11: Proactive Surfacing       | 0     | Static, no recommendations                         |
| P12: Provenance Traceability   | 0     | No provenance tracking                             |
| P13: Heterogeneous Integration | 1     | Multiple content types but siloed                  |
| P14: Longevity Over Features   | 0     | Company-dependent                                  |
| P15: Graceful Degradation      | 0     | Cannot work offline                                |

**Total Score: 13/30 (43%)**
**Essential Principles (P1, P6, P8):** 1/6 - **Fails minimum viability**

**Strengths:**

- Excellent collaboration
- Low friction capture
- Flexible schema (databases)
- Good contextual access control

**Weaknesses:**

- Complete vendor lock-in (critical failure)
- No portability
- Company dependency
- No offline mode
- No provenance

**Engineering Terms Implicated:**

- Document-database hybrid
- Real-time collaboration (operational transform)
- Block-based content model
- Workspace hierarchy

---

## Comparative Summary

| System       | Total Score | Essential (P1,P6,P8) | Min Viable? | Key Strength             | Critical Weakness          |
| ------------ | ----------- | -------------------- | ----------- | ------------------------ | -------------------------- |
| **Obsidian** | 18/30 (60%) | 5/6                  | Almost      | Sovereignty + Longevity  | No temporal tracking       |
| **Roam**     | 11/30 (37%) | 1/6                  | ❌ No       | Capture friction         | Vendor lock-in             |
| **atproto**  | 20/30 (67%) | 5/6                  | Almost      | Provenance + Portability | Not for personal knowledge |
| **Solid**    | 19/30 (63%) | 6/6                  | ✅ Yes      | Semantic richness + ACLs | Performance + Complexity   |
| **Notion**   | 13/30 (43%) | 1/6                  | ❌ No       | Collaboration + UX       | Vendor lock-in             |

---

## Key Observations

### Pattern 1: The Sovereignty Gap

**Roam and Notion fail minimum viability** due to vendor lock-in. No matter how good their features, building life knowledge on company-dependent infrastructure is unacceptable.

### Pattern 2: The Temporal Integrity Gap

**Only atproto has strong temporal tracking built-in.** Most systems treat versioning as afterthought or external concern. This is a universal weakness.

### Pattern 3: The Semantic Richness vs Performance Tradeoff

- **Solid** has maximum semantics (RDF) but terrible performance
- **Obsidian** has fast performance but weak semantics
- No system balances both well

### Pattern 4: The Friction vs Control Tradeoff

- **Roam/Notion** have low friction but no control
- **Solid** has full control but high friction
- **Obsidian** balances reasonably well

### Pattern 5: The Provenance Desert

**Almost no system tracks provenance automatically.** Only atproto's commit model provides this. This is a major gap across all personal knowledge tools.

### Pattern 6: Nobody Solves Multi-Context

**P10 (Contextual Access) is universally weak.** Work/personal boundaries, contextual sharing, time-limited access - these are barely addressed.

---

## Cross-References

- [[principles]] - The 15 principles used for evaluation
- [[gap-analysis]] - Detailed gap analysis from this evaluation
- [[glossary-engineering]] - Engineering terms that matter based on this analysis
