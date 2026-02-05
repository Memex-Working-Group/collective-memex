---
title: Solid Analysis
domain: case study
status: rigorous analysis using evaluation framework
related:
  - "[[core/principles]]"
  - "[[analysis/system-evaluation]]"
  - "[[analysis/glossary-engineering]]"
system_score: 19/30 (meets minimum viability but complex)
tags:
  - ai-slop
author:
  - Sonnet 4.5
---

# Solid Protocol Case Study

## Overview

Solid (Social Linked Data) is Tim Berners-Lee's project for decentralized personal data storage. Users control their data in "pods" (personal online datastores), apps request permission to access specific data.

**Core Architecture:** RDF-based data in pods, Web Access Control (WAC) for permissions, apps are separate from storage, Linked Data Platform (LDP) for standard operations.

**Key Insight:** Solid scores 19/30 in our evaluation - meets minimum viability (P1, P6, P8 all adequate) but has significant weaknesses. The guild's skepticism has merit, but the reasons matter.

---

## Architecture Decisions Mapped to Principles

### Storage: RDF in Pods (Mutable Personal Data Store)

**Implementation:**

- Each user has a pod (web server hosting their data)
- All data stored as RDF triples
- Files and resources accessed via HTTP/LDP
- Can self-host or use pod provider

**Principle Alignment:**

- Strongly supports P1 (Agent Sovereignty) - user owns pod (Score: 2/2)
- Strongly supports P3 (Semantic Richness) - RDF enables formal semantics (Score: 2/2)
- Strongly supports P6 (Interoperability) - RDF is W3C standard (Score: 2/2)
- Fails P9 (Performance Pragmatism) - RDF queries are slow (Score: 0/2)

**Requirements Addressed:**

- R10 (Tool-independent representation) - RDF is universal
- R11 (Relation preservation) - triples preserve relationships
- R13 (Human-readable export) - Turtle serialization is readable

**Requirements Violated:**

- R9 (Performance at scale) - SPARQL is prohibitively slow
- R37 (Low-friction integration) - RDF has steep learning curve

**Gap Analysis:**

- Does NOT address GAP-1 (Temporal Integrity) - no built-in versioning
- Partially addresses GAP-3 (Contextual Access) - WAC enables fine-grained control but complexity barrier

**Why the Guild Might Dismiss:**
Performance is genuinely poor. SPARQL queries on even modest datasets (10k+ triples) are slow. For decades of personal knowledge, this is prohibitive.

**What's Actually Good:**
RDF does provide maximum semantic richness. If performance weren't an issue, the expressiveness is unmatched. The question is whether that expressiveness is worth the cost for personal knowledge.

**Related Terms:** See [[analysis/glossary-engineering]] - RDF, Triple Store, SPARQL

---

### Schema: RDF Vocabularies (Centralized Ontologies)

**Implementation:**

- Use existing vocabularies (schema.org, FOAF, Dublin Core)
- Create custom vocabularies if needed
- Everything is RDF, so vocabularies compose naturally
- No namespace collision (URIs are global)

**Principle Alignment:**

- Strongly supports P3 (Semantic Richness) - formal ontologies (Score: 2/2)
- Supports P6 (Interoperability) - shared vocabularies (Score: 2/2)
- Conflicts with P4 (Schema Pluralism) - assumes centralized ontology (Score: 2/2 but philosophically problematic)
- Conflicts with P5 (Friction Minimization) - requires upfront modeling (Score: 0/2)

**Requirements Addressed:**

- R12 (Schema evolution without data loss) - RDF accommodates new properties
- R11 (Relation preservation) - relationships are first-class

**Why the Guild Might Dismiss:**
The "choose your ontology" problem. Either:

1. Use existing vocabularies (lowest-common-denominator, doesn't fit personal knowledge)
2. Create custom vocabulary (now you need to be ontology engineer)
3. Mix vocabularies (complexity explosion)

For personal note-taking, having to think "is this schema:Thing or foaf:Agent or should I create my:Thought?" is friction.

**What's Actually Good:**
If you DO model properly, the interoperability is real. Your data can be consumed by any RDF-aware tool. This is P6 (Interoperability) at its best.

**Comparison to atproto:**

- atproto Lexicons: Namespaced, versioned, decentralized evolution
- Solid Vocabularies: Global URIs, centralized standards, immediate interoperability

Different tradeoff: atproto optimizes for evolution, Solid for immediate compatibility.

---

### Access Control: Web Access Control (WAC)

**Implementation:**

- ACL documents specify permissions per resource
- ACLs are themselves RDF
- Can grant read, write, append, control
- Supports inheritance (folder to contents)
- Agent-based (specific users) or class-based (anyone, authenticated users)

**Example ACL (Turtle):**

```turtle
<#authorization1>
  a acl:Authorization;
  acl:agent <https://alice.example/profile#me>;
  acl:accessTo <mnemegram123>;
  acl:mode acl:Read, acl:Write.
```

**Principle Alignment:**

- Strongly supports P8 (Protection by Default) - explicit ACLs (Score: 2/2)
- Strongly supports P10 (Contextual Access) - very expressive (Score: 2/2)
- Weakens P9 (Performance) - checking RDF ACLs on every request (Score: 0/2)

**Requirements Addressed:**

- R5 (Fine-grained access control) - per-resource ACLs
- R6 (Mnemegram-level access) - yes, per-resource
- R9 (Auditable access grants) - ACLs are inspectable RDF

**Gap Analysis:**

- Addresses GAP-3 (Contextual Access Control) - One of only two systems (with Notion) that score 2/2 on P10

**Why the Guild Might Dismiss:**
WAC is complex. To use Solid effectively, you need to:

1. Understand RDF
2. Understand LDP (Linked Data Platform)
3. Understand ACL model
4. Write ACL documents for every resource
5. Debug permission issues (SPARQL queries on ACL triples)

This is not "just use your notes." This is "be a semantic web engineer."

**What's Actually Good:**
WAC is probably the most expressive access control system in existence. You can encode almost any permission rule. The problem is that expressiveness comes with complexity.

**Comparison:**

- Solid WAC: Maximum expressiveness, high complexity
- atproto: Simple permissions, limited expressiveness
- Obsidian: No access control (local files)
- Capabilities: Medium expressiveness, UX challenge

Solid chose maximum expressiveness. Reasonable choice IF you have semantic web expertise. Poor choice for general population.

---

### Identity: WebID

**Implementation:**

- Each user has WebID (URI pointing to profile document)
- Profile is RDF describing user
- WebID used for authentication
- Can be self-hosted or on pod provider

**Principle Alignment:**

- Supports P1 (Agent Sovereignty) - self-hostable identity (Score: 2/2)
- Supports P6 (Interoperability) - standard profile format (Score: 2/2)

**Requirements Addressed:**

- R10 (Tool-independent representation) - WebID is URI
- R22 (Decadal maintainability) - web-based, not company-dependent

**Note:** Solid is transitioning to DIDs (Decentralized Identifiers) in newer specs. This would align with atproto's approach.

---

### Query: SPARQL (The Performance Killer)

**Implementation:**

- Query pods using SPARQL
- Can federate queries across multiple pods
- Rich graph queries, inference, reasoning

**Example Query:**

```sparql
PREFIX memex: <http://example.org/memex#>
SELECT ?thought ?date WHERE {
  ?thought memex:about <#DistributedSystems> .
  ?thought memex:created ?date .
  FILTER (?date > "2024-01-01"^^xsd:date)
}
ORDER BY ?date
```

**Principle Alignment:**

- Maximizes P3 (Semantic Richness) - can reason over data (Score: 2/2)
- Catastrophically fails P9 (Performance Pragmatism) (Score: 0/2)

**Why the Guild Should Dismiss (Legitimately):**
SPARQL performance at scale is genuinely bad. For personal knowledge spanning decades:

- 100k triples: Slow
- 1M triples: Very slow
- 10M triples: Unusable

atproto has millions of records per active user and performs well. Solid can't handle this scale.

**The Fundamental Problem:**
RDF triple stores are not optimized for the query patterns personal knowledge requires. Graph databases (Neo4j) are much faster for graph traversal because they use different indexes.

**What Would Fix This:**

- Use property graph database instead of triple store
- Add SPARQL → Cypher translation layer
- But then you're not really using RDF anymore

**This Is The Real Reason To Dismiss Solid:**
Not the complexity (that can be abstracted). Not the friction (that can be reduced). The performance ceiling is too low for personal data operations at scale.

---

## System Evaluation Summary

**Overall Score:** 19/30 (63%)

**Essential Principles (P1, P6, P8):** 6/6 - Meets minimum viability

**Detailed Scores:**
| Principle | Score | Rationale |
|-----------|-------|-----------|
| P1: Agent Sovereignty | 2/2 | Full pod ownership, self-hostable |
| P2: Temporal Integrity | 0/2 | No built-in versioning |
| P3: Semantic Richness | 2/2 | RDF enables formal semantics |
| P4: Schema Pluralism | 2/2 | RDF accommodates any schema |
| P5: Friction Minimization | 0/2 | High learning curve |
| P6: Interoperability | 2/2 | W3C standards throughout |
| P7: Collective Possibility | 1/2 | Can share but complex |
| P8: Protection by Default | 2/2 | WAC fine-grained ACLs |
| P9: Performance Pragmatism | 0/2 | SPARQL too slow |
| P10: Contextual Access | 2/2 | WAC very expressive |
| P11: Proactive Surfacing | 0/2 | No surfacing mechanisms |
| P12: Provenance Traceability | 1/2 | Can model in RDF, not automatic |
| P13: Heterogeneous Integration | 2/2 | RDF handles any data type |
| P14: Longevity Over Features | 2/2 | W3C standard, open |
| P15: Graceful Degradation | 1/2 | Can work offline but complex |

**Strengths:**

1. Maximum semantic richness (P3: 2/2)
2. Best access control (P10: 2/2)
3. True interoperability (P6: 2/2)
4. Agent sovereignty (P1: 2/2)
5. W3C standard (P14: 2/2)

**Critical Weaknesses:**

1. Performance (P9: 0/2) - This is the killer
2. No temporal integrity (P2: 0/2) - Gap-1 unaddressed
3. High friction (P5: 0/2) - Semantic web expertise required
4. No proactive surfacing (P11: 0/2) - Query-only

---

## Should the Guild Dismiss Solid?

**Legitimate Reasons to Dismiss:**

1. **Performance is genuinely inadequate** (P9: 0/2)
   - SPARQL doesn't scale to personal knowledge volumes
   - This isn't fixable without abandoning RDF
   - For decades of daily capture, this is disqualifying

2. **No temporal integrity** (GAP-1 not addressed)
   - Versioning is external (git or similar)
   - Core weakness for reflective knowledge work

3. **Complexity barrier prevents adoption**
   - Requires semantic web expertise
   - Friction kills actual use
   - Designed by/for researchers, not general population

**Illegitimate Reasons to Dismiss:**

1. **"RDF is overkill"** - Maybe, but semantic richness IS valuable
   - The problem is performance cost, not expressiveness itself
   - If fast RDF existed, it would be excellent for personal knowledge

2. **"Too complex"** - Complexity can be abstracted
   - Apps can hide RDF from users
   - WAC could have better UX
   - This is solvable with better tooling

3. **"Nobody uses it"** - Chicken-egg problem
   - Low adoption partially due to performance
   - Also due to lack of compelling apps
   - Network effects matter, but doesn't invalidate architecture

**Nuanced Position:**

Solid's architecture makes principled choices:

- Maximize semantic richness → RDF
- Maximize expressiveness → WAC
- Maximize interoperability → W3C standards

These are GOOD choices for certain values. The problem is the performance tradeoff is too severe for personal data operations at scale.

**The Correct Dismissal:**
"Solid's RDF architecture cannot achieve the performance needed for personal data operations at scale (P9). While its semantic richness (P3) and access control (P10) are excellent, SPARQL's performance ceiling makes it unsuitable for decades of knowledge. We need Solid's expressiveness with Neo4j's performance."

**Not:** "Solid is overengineered academic nonsense"
**But:** "Solid made a reasonable bet on RDF that performance data doesn't support"

---

## What Personal Data Ops Can Learn from Solid

**Adopt from Solid:**

1. Fine-grained access control philosophy (even if not WAC specifically)
2. Semantic richness as goal (even if not RDF specifically)
3. Pod model (user-owned storage, app separation)
4. Agent sovereignty as non-negotiable
5. Standards-based interoperability

**Avoid from Solid:**

1. Triple stores for primary storage (too slow)
2. SPARQL for queries (too slow)
3. Requiring users to understand ontologies
4. Complexity without abstraction layer

**The Hybrid Approach:**
What if you had:

- Solid's pod model (user-owned storage)
- Solid's WAC philosophy (fine-grained contextual access)
- Property graphs instead of RDF (faster queries)
- Capabilities instead of ACL documents (simpler UX)
- Lexicons instead of ontologies (easier evolution)

You'd get Solid's benefits without its performance penalty.

---

## Comparison with atproto

| Dimension          | Solid           | atproto               | Winner  |
| ------------------ | --------------- | --------------------- | ------- |
| Semantic Richness  | RDF (maximum)   | Lexicons (good)       | Solid   |
| Performance        | Poor (SPARQL)   | Good (custom indexes) | atproto |
| Access Control     | Excellent (WAC) | Basic (app-level)     | Solid   |
| Temporal Integrity | None            | Excellent (commits)   | atproto |
| Interoperability   | Maximum (RDF)   | Good (open protocol)  | Solid   |
| Complexity         | Very high       | Medium                | atproto |
| Adoption           | Very low        | Growing               | atproto |

**Synthesis:**
Neither is perfect for personal data operations:

- Solid: Right goals, wrong implementation (performance)
- atproto: Right implementation, wrong goals (social not knowledge)

**Ideal system:**
atproto's architecture (commits, performance) + Solid's goals (semantics, access control) + neither's current implementation.

---

## Open Questions

1. Can property graphs provide Solid-level semantics with better performance?
2. Could SPARQL be optimized for personal knowledge query patterns?
3. Is there a "RDF without the slowness" solution?
4. Can Solid's pod model work with non-RDF storage?
5. Would capabilities provide WAC's expressiveness with better UX?

---

## Conclusion: Was the Guild Right to Dismiss Solid?

**Short answer:** Partially.

**Long answer:**
The guild is right that Solid, as currently implemented, is not suitable for personal data operations at scale. The performance issues (P9: 0/2) are genuine and disqualifying.

However, Solid's design philosophy is sound:

- Agent sovereignty (P1)
- Semantic richness (P3)
- Fine-grained access control (P10)
- Interoperability (P6)

The mistake was betting on RDF/SPARQL for the implementation layer. The principles are correct; the technology stack can't deliver the performance.

**Recommendation:**
Don't dismiss Solid's GOALS. Dismiss Solid's IMPLEMENTATION (specifically RDF triple stores and SPARQL).

Build something with:

- Solid's pod model and sovereignty principles
- atproto's commit model for temporal integrity
- Property graphs (not RDF) for semantic richness with performance
- Capabilities (not WAC documents) for access control
- Lexicons (not ontologies) for schema evolution

**Final Assessment:**
Solid is a noble failure. It aimed for the right goals but chose an implementation stack that cannot deliver the performance required. The guild should learn from Solid's principles while avoiding its architectural choices.

---

## References

**Protocol Documentation:**

- Main docs: https://solidproject.org/
- Specification: https://solidproject.org/TR/protocol
- WAC: https://solidproject.org/TR/wac

**Related Analysis:**

- [[analysis/system-evaluation]] - Full scoring
- [[analysis/gap-analysis]] - GAP-3 (Solid is one of two adequate solutions)
- [[context/landscape/access-control-models]] - WAC in depth
- [[context/landscape/query-approaches]] - SPARQL performance issues
- [[context/cases/atproto-analysis]] - Comparison system
