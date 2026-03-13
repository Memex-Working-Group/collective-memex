---
title: Query Approaches
domain: engineering architecture
status: analysis-driven
note: Addresses P3 (Semantic Richness), P9 (Performance), supports retrieval requirements
related:
  - "[[principles]]"
  - "[[gap-analysis]]"
  - "[[glossary-engineering]]"
tags:
  - ai-slop
author:
  - Sonnet 4.5
---

# Query Approaches for Personal Knowledge

This document surveys query architectures for personal data operations. Query capability directly impacts P3 (Semantic Richness) and P9 (Performance Pragmatism) - a core tension identified in our analysis.

---

## The Query Challenge in Personal Data

**Core Tension:** Flexibility vs Performance (identified in principles analysis)

- Rich semantic queries require complex data models (slow)
- Fast queries require simple models (limited expressiveness)

**Requirements Implicated:**

- R3: Semantic query support (not just keyword matching)
- R14: Graph traversal and pattern detection
- R17: Non-obvious connection discovery
- R30: Surface knowledge gaps
- R31: Progression queries ("show my development on X")
- R50: Full-text search across heterogeneous content

**Principles:**

- P3 (Semantic Richness): Meaning must be explicit and queryable
- P9 (Performance Pragmatism): Must scale to decades of data

---

## Full-Text Search

**Description:** Keyword-based search using inverted index. Foundation of most search engines.

**How It Works:**

1. Build inverted index: term → documents containing term
2. Query breaks into terms
3. Look up terms in index
4. Rank results by relevance (TF-IDF, BM25)

**Query Examples:**

```
"distributed systems CRDT"
"quantum NOT mechanics"
title:"event sourcing"
```

**Principle Alignment:**

- Supports P9 (Performance) - very fast with proper indexing
- Weakens P3 (Semantic Richness) - keyword only, no relationships
- Excellent for R50 (full-text across content types)

**Requirements Addressed:**

- R50 (Full-text search) - primary solution
- R4 (Time-travel) - can filter by date

**Requirements Not Addressed:**

- R3 (Semantic queries) - no understanding of meaning
- R14 (Graph traversal) - no relationship queries
- R17 (Non-obvious connections) - can't find implicit links

**Strengths:**

- Very fast (O(log n) with indexing)
- Scales to millions of documents
- User-familiar (everyone knows keyword search)
- Works across heterogeneous content

**Weaknesses:**

- No semantic understanding
- Can't query relationships
- Relevance ranking is heuristic
- No inference or reasoning

**Implementations:**

- Elasticsearch, Solr (distributed search)
- Tantivy (Rust, used by some PKM tools)
- SQLite FTS (lightweight, embedded)
- Lunr.js (client-side JavaScript)

**Use for Personal Data Ops:**
Essential baseline. Every system needs full-text search. But insufficient alone for semantic richness.

---

## Graph Traversal Queries

**Description:** Queries that "walk" relationships between nodes. Native to graph databases.

**Query Languages:**

- **Cypher** (Neo4j)
- **Gremlin** (TinkerPop, property graphs)
- **SPARQL** (RDF graphs)

**Query Examples (Cypher):**

```cypher
// Find all mnemegrams 2 hops from "event sourcing"
MATCH (start:Mnemegram {title: "Event Sourcing"})-[*1..2]-(related)
RETURN related

// Find paths between two concepts
MATCH path = shortestPath(
  (a:Mnemegram {title: "CRDT"})-[*]-(b:Mnemegram {title: "Git"})
)
RETURN path

// Find clustering (highly interconnected groups)
CALL gds.louvain.stream('knowledge-graph')
YIELD nodeId, communityId
```

**Principle Alignment:**

- Strongly supports P3 (Semantic Richness) - relationships are first-class
- Good performance for P9 - graph databases optimized for traversal
- Excellent for R14 (graph traversal), R17 (non-obvious connections)

**Requirements Addressed:**

- R14 (Graph traversal and pattern detection) - designed for this
- R17 (Non-obvious connection discovery) - pathfinding algorithms
- R3 (Semantic queries) - can query by relationship type

**Requirements Challenged:**

- R50 (Full-text across content) - requires separate text index

**Strengths:**

- Natural for knowledge graphs
- Expressive relationship queries
- Pathfinding algorithms built-in
- Pattern matching
- Community detection, centrality measures

**Weaknesses:**

- Requires graph data model
- Query complexity can explode
- Performance degrades with very large graphs (millions of edges)
- Different query language per graph database

**Implementations:**

- **Neo4j** (property graph, Cypher) - most mature
- **RDF triple stores** (Blazegraph, Virtuoso) - SPARQL
- **Graph libraries** (NetworkX, igraph) - not databases, in-memory

**Use for Personal Data Ops:**
Essential for semantic richness. Enables queries like:

- "Show me all concepts related to X within 3 degrees"
- "What connects my work on A to my interest in B?"
- "Which concepts am I underexploring?" (low connection density)

**Challenge:** Need to maintain graph structure. Links must be explicit.

---

## Semantic/SPARQL Queries (RDF)

**Description:** Query RDF triples using SPARQL. Maximum semantic expressiveness.

**Query Example (SPARQL):**

```sparql
PREFIX memex: <http://example.org/memex#>
PREFIX dc: <http://purl.org/dc/terms/>

# Find mnemegrams about CRDT with provenance
SELECT ?mnemegram ?source ?date WHERE {
  ?mnemegram memex:about <#CRDT> .
  ?mnemegram dc:source ?source .
  ?mnemegram dc:created ?date .
  FILTER (?date > "2023-01-01"^^xsd:date)
}
ORDER BY ?date
```

**Principle Alignment:**

- Maximum P3 (Semantic Richness) - RDF enables formal reasoning
- Poor P9 (Performance) - SPARQL is slow at scale
- Excellent for P6 (Interoperability) - RDF is standard

**Requirements Addressed:**

- R3 (Semantic queries) - most expressive option
- R2 (Provenance chains) - RDF excels at provenance
- R11 (Relation preservation) - RDF triples are universal

**Requirements Challenged:**

- R9 (Performance) - SPARQL poor at scale
- R50 (Full-text) - need separate text index

**Strengths:**

- Maximally expressive
- Formal semantics (can reason, infer)
- W3C standard (interoperable)
- Can query across federated datasets
- Rich existing vocabularies (schema.org, FOAF)

**Weaknesses:**

- Very slow (SPARQL optimization is hard)
- Steep learning curve
- Verbose (RDF is wordy)
- Requires semantic modeling upfront

**System Performance:**
Solid (using SPARQL) scores 0/2 on P9 (Performance) despite 2/2 on P3 (Semantic Richness). This is the expressiveness/performance tradeoff.

**Use for Personal Data Ops:**
Consider when:

- Already using RDF (e.g., Solid pods)
- Formal reasoning needed
- Interoperability critical
- Willing to accept performance cost
- Data volume is modest (< 100k triples)

**Not recommended when:**

- Performance is priority
- Real-time queries needed
- Users unfamiliar with SPARQL

---

## Vector Similarity Search

**Description:** Semantic search using dense vector embeddings. Find similar content without keyword matching.

**How It Works:**

1. Generate embedding for each mnemegram (OpenAI, sentence transformers)
2. Store embeddings in vector database
3. Query by converting query to embedding
4. Find nearest neighbors in vector space (cosine similarity)

**Query Examples:**

```python
# Find notes similar to this one
similar = vector_db.search(
    embedding=embed("My note about event sourcing"),
    k=10
)

# Semantic query without exact keywords
results = vector_db.search(
    embedding=embed("How do distributed systems handle time?"),
    k=5
)
```

**Principle Alignment:**

- Supports P3 (Semantic Richness) - semantic similarity, not keywords
- Moderate P9 (Performance) - fast with proper indexing (HNSW)
- Excellent for R3 (semantic queries), R17 (non-obvious connections)

**Requirements Addressed:**

- R3 (Semantic query support) - finds conceptually related content
- R17 (Non-obvious connection discovery) - "similar but not linked"
- R30 (Surface knowledge gaps) - clustering can reveal underexplored areas

**Requirements Challenged:**

- R2 (Provenance) - embeddings don't capture provenance
- R14 (Graph traversal) - similarity is not same as explicit relationships

**Strengths:**

- Semantic understanding without explicit modeling
- Finds similar content even if different wording
- Multilingual (embeddings work across languages)
- Can combine with keyword search (hybrid)

**Weaknesses:**

- Requires ML model (embedding generation)
- Embeddings are opaque (hard to explain why similar)
- Recalculate embeddings when content changes
- Quality depends on embedding model

**Implementations:**

- **Pinecone, Weaviate** (managed vector databases)
- **FAISS** (Facebook AI, local library)
- **pgvector** (PostgreSQL extension)
- **Qdrant** (open source vector database)

**Use for Personal Data Ops:**
Powerful complement to other approaches. Enables:

- "Find notes similar to this, even if different terms"
- Semantic clustering (group related concepts)
- Anomaly detection (what doesn't fit anywhere?)

**Challenge:** Need to regenerate embeddings as knowledge evolves. Cost of embedding generation.

---

## Temporal/Time-Travel Queries

**Description:** Queries that ask "what did I know when?" Essential for P2 (Temporal Integrity).

**Query Examples:**

```sql
-- What did I know about X on date Y?
SELECT * FROM mnemegrams
WHERE about = 'CRDT'
  AND created_at <= '2024-01-01'

-- How did my understanding of X evolve?
SELECT created_at, content FROM mnemegrams
WHERE about = 'event-sourcing'
ORDER BY created_at

-- What changed this week?
SELECT * FROM mnemegrams
WHERE updated_at >= NOW() - INTERVAL '7 days'
```

**Principle Alignment:**

- Essential for P2 (Temporal Integrity)
- Supports P12 (Provenance Traceability)
- Enables R4 (time-travel views), R31 (progression queries)

**Requirements Addressed:**

- R4 (Time-travel views) - primary solution
- R1 (Temporal ordering) - queries respect time
- R31 (Show progression on X) - evolution queries

**Implementation Approaches:**

**A. Temporal Databases:**

- SQL:2011 temporal extensions
- Datomic (point-in-time queries built-in)
- Store valid-time and transaction-time

**B. Event Sourcing:**

- Replay events up to timestamp
- Natural time-travel
- atproto uses this (commit history)

**C. Versioning Layer:**

- Git-style snapshots
- Query specific commit/version

**Strengths:**

- Essential for reflection (T7)
- Enables provenance queries
- Audit trail intrinsic

**Weaknesses:**

- Storage overhead (keep all history)
- Query complexity (need to specify time)
- Indexes must be temporal-aware

**Use for Personal Data Ops:**
Non-negotiable for systems addressing GAP-1 (Temporal Integrity). Should be combined with other query approaches.

---

## Spatial/Geospatial Queries

**Description:** Queries based on location. "Where was I when X?"

**Query Examples (PostGIS):**

```sql
-- Find mnemegrams created within 1km of location
SELECT * FROM mnemegrams
WHERE ST_DWithin(
    location,
    ST_MakePoint(-122.4194, 37.7749),  -- San Francisco
    1000  -- meters
)

-- What was I thinking about in this city?
SELECT * FROM mnemegrams
WHERE ST_Contains(
    (SELECT boundary FROM cities WHERE name = 'Tokyo'),
    location
)
```

**Principle Alignment:**

- Supports P13 (Heterogeneous Integration) - location as first-class data
- Moderate P9 (Performance) - spatial indexes efficient

**Requirements Addressed:**

- R71 (Geospatial indexing and query)
- R72 (Temporal indexing) - combine with time for "where/when"
- R73 (Entity tracking - places)

**Implementations:**

- PostGIS (PostgreSQL extension)
- S2 geometry (Google)
- H3 (Uber's hexagonal grid)
- GeoJSON + turf.js (JavaScript)

**Use for Personal Data Ops:**
Relevant for:

- Location-aware capture (UC-16)
- Travel journals
- Context: "what was I thinking about in that place?"

**Challenge:** Location privacy (R74). Geospatial data is sensitive.

---

## Aggregation and Analytics Queries

**Description:** Queries that compute over collections. "What are my patterns?"

**Query Examples:**

```sql
-- Most referenced concepts
SELECT referent, COUNT(*) as count
FROM relations
GROUP BY referent
ORDER BY count DESC

-- My output over time
SELECT DATE_TRUNC('month', created_at) as month,
       COUNT(*) as mnemegrams_created
FROM mnemegrams
GROUP BY month

-- Concept co-occurrence
SELECT a.concept, b.concept, COUNT(*) as frequency
FROM mnemegrams m
  JOIN concepts a ON m.id = a.mnemegram_id
  JOIN concepts b ON m.id = b.mnemegram_id
WHERE a.concept < b.concept
GROUP BY a.concept, b.concept
ORDER BY frequency DESC
```

**Principle Alignment:**

- Supports P11 (Proactive Surfacing) - analytics reveal patterns
- Supports P9 (Performance) - with proper indexes

**Requirements Addressed:**

- R30 (Surface knowledge gaps) - find underexplored concepts
- R77 (Pattern detection) - identify trends
- R42 (Temporal decay) - measure activity over time

**Implementation:**

- SQL aggregations (standard databases)
- Graph analytics (Neo4j, NetworkX)
- Time series databases (InfluxDB, TimescaleDB)

**Use for Personal Data Ops:**
Enables:

- "What am I thinking about most this year?"
- "Which connections am I neglecting?" (relationship half-life)
- "Am I more productive in mornings or evenings?"

**Challenge:** Privacy - aggregate patterns can be revealing.

---

## Comparative Analysis

**Query Expressiveness:**

```
Full-text < Vector < Graph < SPARQL
(keywords)               (semantic reasoning)
```

**Query Performance:**

```
Full-text > Vector > Graph > SPARQL
(fast)                      (slow)
```

**Ease of Use:**

```
Full-text > SQL > Vector > Graph > SPARQL
(familiar)                      (specialist)
```

**Semantic Richness:**

```
Full-text < SQL < Vector < Graph < SPARQL
(surface)                        (deep)
```

---

## Hybrid Query Strategies

Real systems need multiple query approaches:

**Common Combinations:**

**1. Full-text + Graph (Most Common)**

- Keyword search to find candidates
- Graph traversal to explore connections
- Example: Roam, Obsidian graph view

**2. Vector + Full-text (Emerging)**

- Keyword for precise matching
- Vector for semantic similarity
- Hybrid ranking combines both

**3. Graph + Temporal**

- Graph for relationships
- Temporal for evolution
- atproto does this well

**4. Full-text + Spatial + Temporal**

- Where + When + What
- UC-16 (Event logging) requires all three

**Implementation Strategy:**

- Primary index: Full-text (essential baseline)
- Secondary: Graph (if explicit links exist)
- Optional: Vector (if semantic similarity valuable)
- Always: Temporal (for P2 compliance)
- Conditional: Spatial (if location-aware)

---

## Query Interface Design

**Natural Language Queries (with LLM):**

```
"Show me what I was thinking about CRDTs last summer"
  ↓ LLM translates to:
SELECT * FROM mnemegrams
WHERE content LIKE '%CRDT%'
  AND created_at BETWEEN '2024-06-01' AND '2024-08-31'
```

Strengths: User-friendly, no query language needed
Weaknesses: LLM reliability, cost, privacy (if cloud)

**Visual Query Builder:**
Graph-based query construction (like Roam's query builder)

**DSL (Domain-Specific Language):**
Custom query syntax for common patterns
Example: `tag:work created:last-week about:strategy`

---

## Performance Considerations

**Indexing Strategies:**

- Full-text: Inverted index
- Graph: Adjacency lists
- Vector: HNSW (Hierarchical Navigable Small World)
- Spatial: R-tree, quadtree
- Temporal: B-tree on timestamp

**Materialized Views:**
Pre-compute common queries for speed
Example: "Most referenced concepts" updated nightly

**Caching:**
Cache frequent queries
Invalidate on data change

**Query Optimization:**

- Index selection crucial
- Query planning (SPARQL needs this badly)
- Limit result sets
- Pagination for large results

---

## Recommendations by Use Case

**For Daily Note-Taking (Obsidian-like):**

- Full-text (essential)
- Simple graph (backlinks, forward links)
- Optional: Vector for "similar notes"

**For Research/Academic:**

- Full-text + Graph (citations, concepts)
- Temporal (track evolution of thinking)
- Optional: SPARQL if formal ontology needed

**For Quantified Self:**

- Temporal + Aggregation (patterns over time)
- Spatial (location context)
- Full-text (find by content)

**For AI-Augmented:**

- Vector (semantic similarity)
- Full-text (keyword fallback)
- Graph (explicit relationships)

---

## Open Questions

1. Can vector similarity replace explicit linking?
2. How do you query across multiple temporal versions efficiently?
3. What's the right balance of indexes (storage cost vs query speed)?
4. Can LLMs generate reliable queries from natural language?
5. How do you explain why a query returned these results (explainability)?
6. Can federated queries work across personal memexes?

---

## Cross-References

- [[principles]] - P3 (Semantic Richness), P9 (Performance)
- [[gap-analysis]] - Query approaches address multiple gaps
- [[glossary-engineering]] - Technical term definitions
- [[storage-models]] - Storage affects query capability
- [[atproto-analysis]] - Graph + temporal queries
