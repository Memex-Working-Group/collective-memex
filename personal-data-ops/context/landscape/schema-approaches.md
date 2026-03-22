---
title: Schema and Vocabulary Approaches
domain: engineering architecture
status: exploratory (predates requirements/principles analysis)
note: For requirements-driven evaluation, see analysis/system-evaluation.md and
  analysis/gap-analysis.md
related:
  - "[[principles]]"
  - "[[glossary-engineering]]"
tags:
  - ai-slop
author:
  - Sonnet 4.5
uuid: a5f51030-a649-409f-9253-629270b3fe70
share: true
---
# Schema Approaches for Personal Knowledge

This document surveys approaches to structuring meaning in personal data operations. Each approach represents different tradeoffs between flexibility and queryability, a core tension identified in our principles analysis.

---

## Centralized Ontologies

**What it solves:** Shared semantics, interoperability

**Key implementations:** schema.org, FOAF, Dublin Core

**Description:** Standardized vocabularies where everyone agrees on what entities and relationships mean. Apps can reliably interpret each other's data.

**Principle Alignment:**

- Supports P3 (Semantic Richness) - formal semantics enable inference
- Supports P6 (Interoperability) - shared vocabulary enables portability
- Conflicts with P4 (Schema Pluralism) - assumes single correct schema
- Conflicts with P5 (Friction Minimization) - requires upfront modeling

**Requirements Addressed:**

- R10 (Tool-independent representation)
- R11 (Relation preservation across transformations)

**Tradeoffs:**

- Strengths: Strong interoperability, rich existing vocabularies, tooling support (validators, reasoners)
- Weaknesses: Lowest-common-denominator problem, slow evolution, assumes consensus exists

**Questions:**

- Does personal knowledge need to be interoperable across individuals?
- What if my concept of "importance" differs from schema.org?

**Related Terms:** See [[glossary-engineering]] - RDF, SPARQL, Ontology

---

## Lexicon Systems (Namespaced Schemas)

**What it solves:** Schema evolution without global coordination

**Key implementations:** atproto Lexicons, JSON-LD contexts

**Description:** Schemas are versioned, namespaced documents. Anyone can define new schemas without central approval. Example: `com.myapp.note.v2`

**Principle Alignment:**

- Strongly supports P4 (Schema Pluralism) - multiple concurrent schemas by design
- Supports P6 (Interoperability) - schemas are portable definitions
- Addresses GAP between centralized (too rigid) and emergent (too loose)

**Requirements Addressed:**

- R12 (Schema evolution without data loss)
- R11 (Relation preservation)

**Tradeoffs:**

- Strengths: Fast iteration, no central authority needed, versioning built-in
- Weaknesses: Fragmentation risk (many "note" schemas), apps must handle multiple versions, discovery problem

**System Examples:**

- atproto uses lexicons for all record types
- JSON-LD contexts serve similar function in Solid

**Questions:**

- How do you merge knowledge from different lexicons?
- Who defines vocabulary for personal concepts like "thinking process"?

**Related Terms:** See [[glossary-engineering]] - Lexicon System, JSON-LD

---

## Property Graphs

**What it solves:** Relationships as first-class entities, expressive queries

**Key implementations:** Neo4j, labeled property graph databases, Roam Research

**Description:** Nodes and edges both have properties. Queries traverse relationships naturally using graph query languages.

**Principle Alignment:**

- Strongly supports P3 (Semantic Richness) - typed, directional relationships
- Supports P9 (Performance Pragmatism) - graph databases optimized for traversal
- Better performance than RDF triple stores for many queries

**Gap Addressed:**

- Partially addresses GAP-4 (Proactive Surfacing) - graph algorithms enable discovery

**Requirements Addressed:**

- R14 (Graph traversal and pattern detection)
- R17 (Non-obvious connection discovery)
- R3 (Semantic query support)

**Tradeoffs:**

- Strengths: Natural for knowledge graphs, powerful query languages (Cypher), schema can be emergent
- Weaknesses: Can become unstructured without discipline, version/migration challenges, performance degrades with sprawl

**Questions:**

- How structured should relationship types be?
- Is `[[related-to]]` sufficient or do you need `[[challenges]]`, `[[extends]]`, `[[contradicts]]`?

**Related Terms:** See [[glossary-engineering]] - Property Graph, Graph Traversal

---

## Document-Oriented / Flexible JSON

**What it solves:** Schema flexibility, developer ergonomics

**Key implementations:** MongoDB, JSON-LD, Obsidian frontmatter

**Description:** Documents can have arbitrary structure. Schema validation at use-time, not storage-time. "Schema-on-read" rather than "schema-on-write."

**Principle Alignment:**

- Supports P4 (Schema Pluralism) - accommodates unexpected properties
- Supports P5 (Friction Minimization) - low cognitive overhead to start
- Weakens P3 (Semantic Richness) - relationships less explicit
- Weakens P9 (Performance Pragmatism) - query optimization difficult

**Requirements Addressed:**

- R37 (Low-friction integration)
- R12 (Schema evolution)

**Tradeoffs:**

- Strengths: Easy to start, accommodates unexpected properties, familiar to developers
- Weaknesses: Query optimization difficult, schema drift over time, validation is optional

**Questions:**

- How do you prevent vault from becoming junk drawer?
- When do you need schema discipline?

**System Examples:**

- Obsidian uses Markdown with YAML frontmatter
- Notion uses flexible block-based documents

---

## Schema-less / Emergent Structure

**What it solves:** Pure flexibility, structure emerges from use

**Key implementations:** Roam Research, Obsidian (in practice), Zettelkasten method

**Description:** No predefined structure. Meaning emerges from links, backlinks, and tags. Structure is implicit, not explicit.

**Principle Alignment:**

- Maximizes P4 (Schema Pluralism) - no schema at all
- Maximizes P5 (Friction Minimization) - zero upfront modeling
- Strongly conflicts with P3 (Semantic Richness) - relationships are untyped
- Conflicts with P9 (Performance Pragmatism) - structured queries difficult

**Requirements Challenged:**

- R3 (Semantic query support) - no formal semantics
- R14 (Graph traversal) - relationships are implicit
- R29 (Presentation-ready export) - structure must be inferred

**Tradeoffs:**

- Strengths: Zero cognitive overhead, organic evolution, resists premature optimization
- Weaknesses: Structured queries difficult, consistency hard to enforce, export/migration pain

**Philosophy:** Classic Zettelkasten - let structure emerge from connections rather than imposing hierarchy.

**Questions:**

- Can you have emergence AND queryability?
- What is minimal structure needed for useful computation?

**Related Terms:** Zettelkasten, emergent order

---

## Comparative Analysis

**Flexibility vs Queryability Spectrum:**

```
Schema-less ← Document-Oriented ← Property Graph ← Lexicons ← Centralized Ontologies
  (max flex)                                                    (max queryability)
```

**Which Approach for Which Principle:**

- **P3 (Semantic Richness):** Centralized Ontologies, Property Graphs
- **P4 (Schema Pluralism):** Lexicons, Document-Oriented, Schema-less
- **P5 (Friction Minimization):** Schema-less, Document-Oriented
- **P9 (Performance):** Property Graphs, Lexicons

**System Scores by Approach:**

- Solid (Centralized Ontologies via RDF): 19/30 - semantics but poor performance
- atproto (Lexicons): 20/30 - good balance, designed for evolution
- Obsidian (Schema-less): 18/30 - low friction but weak semantics
- Roam (Property Graph-ish): 11/30 - good surfacing but vendor lock-in

---

## Cross-Domain Term Mapping

Understanding how different communities name similar concepts:

| Concept              | Semantic Web         | Data Ops          | PKM             |
| -------------------- | -------------------- | ----------------- | --------------- |
| Structure definition | Ontology             | Schema            | Template        |
| Relationship         | Predicate/Property   | Foreign key/Edge  | Link/Connection |
| Validation           | SHACL/ShEx           | Schema validation | Linting         |
| Evolution            | Versioned namespaces | Migration scripts | Refactoring     |

---

## Selection Criteria

Based on our principles and requirements:

**Choose Centralized Ontologies if:**

- Interoperability with external systems is critical (P6)
- Formal reasoning and inference are needed (P3)
- Willing to accept upfront modeling cost

**Choose Lexicons if:**

- Schema evolution is frequent (P4, R12)
- Multiple concurrent schemas needed
- Decentralized schema development required

**Choose Property Graphs if:**

- Relationship queries are primary use case (R14, R17)
- Performance at scale matters (P9)
- Willing to impose some schema discipline

**Choose Document-Oriented if:**

- Rapid iteration and experimentation (P5)
- Schema is still emerging
- Developer ergonomics priority

**Choose Schema-less if:**

- Absolute minimum friction required (P5)
- User base is non-technical
- Structure can emerge organically

---

## Open Questions

1. Should personal schemas be standardized or bespoke?
2. How do you balance expressive power with query performance?
3. What is the right level of formality for "notes to self" versus shared knowledge?
4. Can AI help with schema suggestion/emergence?
5. Can hybrid approaches combine flexibility and queryability effectively?

---

## Cross-References

- [[principles]] - P3 (Semantic Richness), P4 (Schema Pluralism)
- [[system-evaluation]] - How real systems score on these dimensions
- [[gap-analysis]] - GAP-3 (Semantic richness vs performance tradeoff)
- [[glossary-engineering]] - Technical term definitions
- [[atproto-analysis]] - Lexicon system in practice