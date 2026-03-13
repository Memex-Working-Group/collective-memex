---
title: Engineering Glossary - Terms Implicated by Analysis
status: draft
created: 2025-02-05
derived_from:
  - "[[system-evaluation]]"
  - "[[gap-analysis]]"
  - "[[principles]]"
note: This glossary contains only terms that emerged as relevant through our requirements and systems analysis
tags:
  - ai-slop
author:
  - Sonnet 4.5
---

# Engineering Glossary

This glossary defines technical terms that matter for personal data operations, identified through systematic analysis of use cases, requirements, principles, and existing systems.

**Organization:** Terms grouped by the architectural pattern or principle they serve.

---

## Temporal Integrity & Provenance (GAP-1, GAP-2, P2, P12)

### Event Sourcing

**Definition:** Architectural pattern where state changes are stored as a sequence of events rather than updating current state in-place.
**Why It Matters:** Solves temporal integrity and provenance. Every change is an event in an immutable log. Current state is derived by replaying events.
**Example:** Banking ledger - transactions are events, balance is derived.
**Applied to Memex:** Each edit, annotation, or connection is an event. Time-travel = replay events up to timestamp.
**Related Terms:** Append-only log, CQRS (Command Query Responsibility Segregation)
**Trade-offs:**

- ✅ Perfect audit trail, time-travel queries
- ❌ Query complexity (need materialized views)
- ❌ Storage grows forever (requires compaction)

---

### Append-Only Log

**Definition:** Data structure where writes only add to the end; existing entries never modified.
**Why It Matters:** Foundation for event sourcing and temporal integrity. Simplifies replication and conflict resolution.
**Example:** Secure Scuttlebutt, Apache Kafka
**Applied to Memex:** Mnemegrams and assertions are entries in append-only log. History is intrinsic.
**Related Terms:** Event sourcing, immutable data structures
**Implementations:** SSB feeds, Hypercore, Git (commit history)

---

### Commit Model

**Definition:** State changes are bundled into signed, immutable commits with pointers to parent commits.
**Why It Matters:** Provides branching, merging, and cryptographic verification. Proven by Git.
**Example:** Git commits form directed acyclic graph (DAG).
**Applied to Memex:** atproto uses this - each change is signed commit pointing to previous state.
**Related Terms:** Merkle tree, DAG, cryptographic signing
**Trade-offs:**

- ✅ Branching and merging possible
- ✅ Cryptographic verification
- ❌ More complex than linear log

---

### Merkle Tree / Merkle Search Tree (MST)

**Definition:** Tree where each node contains hash of its children. Enables efficient verification and deduplication.
**Why It Matters:** Used in atproto for content-addressed repositories. Enables proving "this content existed at this time."
**Example:** Bitcoin blockchain uses Merkle trees for transactions.
**Applied to Memex:** Repository of mnemegrams as MST allows efficient sync and verification.
**Related Terms:** Hash tree, content addressing

---

### Content Addressing (CID - Content Identifier)

**Definition:** Data is referenced by its cryptographic hash rather than location (URL).
**Why It Matters:** Same content always has same address. Enables deduplication, verification, and peer-to-peer distribution.
**Example:** IPFS uses CIDs like `bafybeigdyrzt5sfp7udm7hu76uh7y26nf3efuylqabf3oclgtqy55fbzdi`
**Applied to Memex:** Immutable mnemegrams get CIDs. Provenance chains reference by CID.
**Related Terms:** Content-addressable storage (CAS), IPFS, CAR files
**Trade-offs:**

- ✅ Deduplication, verification, P2P
- ❌ Deletion requires indirection (not true deletion)

---

### CAR Files (Content Addressable aRchives)

**Definition:** File format for storing content-addressed data. Used by IPFS and atproto.
**Why It Matters:** Portable format for immutable content. Can be exported/imported between systems.
**Applied to Memex:** Repository export as CAR file = portable backup with provenance intact.

---

### Temporal Indexing

**Definition:** Index that allows querying data "as of time T" or "between T1 and T2."
**Why It Matters:** Enables time-travel queries. "What did I know on Jan 1, 2023?"
**Applied to Memex:** Index maintains historical states, not just current state.
**Implementations:** Temporal databases (SQL:2011 temporal extensions), Datomic
**Related Terms:** Bitemporal data (valid-time vs transaction-time)

---

## Access Control & Protection (GAP-3, P8, P10)

### Capability-Based Security

**Definition:** Access rights represented as unforgeable tokens (capabilities) that can be passed between entities.
**Why It Matters:** Solves contextual access control. "Here's a token giving you read access to these 10 mnemegrams."
**Example:** UCAN (User Controlled Authorization Networks), Macaroons
**Applied to Memex:** Agent gets capability token for specific mnemegrams, can delegate subset to AI agent.
**Related Terms:** Object capabilities, ambient authority (the opposite)
**Trade-offs:**

- ✅ Fine-grained, delegatable, revocable
- ✅ No centralized ACL server needed
- ❌ UX challenge (managing tokens)

---

### UCAN (User Controlled Authorization Networks)

**Definition:** Specific capability-based auth system using JWT-like tokens with cryptographic delegation chains.
**Why It Matters:** Enables decentralized access control without central authority. Used by Fission, explored by Web3 community.
**Applied to Memex:** Agent signs UCAN granting read access to family members, who can further delegate to AI assistant.
**Spec:** https://ucan.xyz/

---

### Web Access Control (WAC)

**Definition:** RDF-based ACL system used by Solid. Permissions defined per-resource.
**Why It Matters:** Shows how fine-grained ACLs can work in decentralized setting, but complex.
**Applied to Memex:** Each mnemegram can have ACL specifying read/write/control permissions.
**Related Terms:** Access Control List (ACL), RDF
**Trade-offs:**

- ✅ Very expressive (RDF flexibility)
- ❌ Complex, RDF learning curve

---

### Access Control List (ACL)

**Definition:** List of permissions attached to object specifying who can access and what they can do.
**Why It Matters:** Standard model for file systems, databases. Familiar to implementers.
**Applied to Memex:** Each mnemegram or collection has ACL (user X: read, user Y: read+write).
**Trade-offs:**

- ✅ Well-understood, lots of tooling
- ❌ Centralized (need ACL server)
- ❌ Not easily delegatable

---

### Attribute-Based Access Control (ABAC)

**Definition:** Access decisions based on attributes of subject, resource, and context rather than identity alone.
**Why It Matters:** Enables "work colleagues can see work-context mnemegrams" without listing every colleague.
**Example:** "Users with attribute role=researcher AND context=work can read documents tagged work."
**Applied to Memex:** Contextual access based on mnemegram tags, time, location.

---

### Cryptographic Signing (K256, Ed25519)

**Definition:** Using public-key cryptography to prove authorship and integrity of data.
**Why It Matters:** Enables verification without trusted authority. "This mnemegram was created by agent X and hasn't been tampered with."
**Applied to Memex:** All mnemegrams signed by creating agent. Provenance chain is cryptographically verified.
**Implementations:** K256 (secp256k1, used by Bitcoin/atproto), Ed25519 (used by SSB, Signal)

---

## Storage & Architecture (P1, P6, P14, P15)

### Local-First Architecture

**Definition:** Software that works primarily with local data, syncing to cloud opportunistically. Network is enhancement, not requirement.
**Why It Matters:** Solves agent sovereignty, graceful degradation, longevity. Works offline, survives server shutdowns.
**Example:** Obsidian, Git
**Applied to Memex:** Mnemegrams stored locally, synced to other devices peer-to-peer or via server.
**Manifesto:** https://www.inkandswitch.com/local-first/
**Trade-offs:**

- ✅ Privacy, performance, reliability
- ❌ Sync complexity (conflicts)

---

### Conflict-Free Replicated Data Types (CRDT)

**Definition:** Data structures that can be replicated across devices and merged without conflicts.
**Why It Matters:** Solves multi-device sync for local-first architecture. No central server needed for conflict resolution.
**Example:** Yjs (used by collaborative editors), Automerge
**Applied to Memex:** Mnemegrams as CRDTs allow offline edits on multiple devices, automatic merge.
**Types:** Last-write-wins (LWW), operation-based, state-based
**Trade-offs:**

- ✅ Automatic conflict resolution
- ❌ Some operations difficult to represent (deletion, constraints)

---

### Operational Transform (OT)

**Definition:** Algorithm for merging concurrent edits to shared data. Alternative to CRDTs.
**Why It Matters:** Used by Google Docs, Notion for real-time collaboration.
**Applied to Memex:** If multiple agents edit same mnemegram simultaneously, OT merges changes.
**Trade-offs (vs CRDT):**

- ✅ More natural for some operations
- ❌ Requires central server or complex algorithm

---

### Personal Data Server (PDS)

**Definition:** Self-hostable server that stores user's data. User owns, apps connect via API.
**Why It Matters:** Enables agent sovereignty + interoperability. atproto and Solid both use this model.
**Applied to Memex:** Agent's mnemegrams live in their PDS, apps request access.
**Implementations:** atproto PDS, Solid Pod
**Trade-offs:**

- ✅ User control, app portability
- ❌ Requires hosting (even if delegated)

---

### Federation

**Definition:** Multiple independent servers that interoperate using shared protocol.
**Why It Matters:** Enables collective possibility without centralization. Email, atproto are federated.
**Applied to Memex:** Multiple agents' PDS instances can share/query each other's mnemegrams with permission.
**Related Terms:** ActivityPub (Mastodon), atproto relays

---

### Repository Model

**Definition:** User's data as structured repository with commit history, similar to Git.
**Why It Matters:** atproto's approach. Provides versioning, signing, portability.
**Applied to Memex:** Each agent has repository of mnemegrams with signed commit history.
**Components:** Merkle tree of records, commit log, signature chain

---

## Schema & Data Modeling (P3, P4, P13)

### RDF (Resource Description Framework)

**Definition:** Everything is a triple: subject-predicate-object. W3C standard for semantic web.
**Why It Matters:** Maximum semantic richness and interoperability. Used by Solid.
**Example:** `<#me> <knows> <#you> .` (I know you)
**Applied to Memex:** Mnemegrams, assertions, relations all as RDF triples.
**Serializations:** Turtle, JSON-LD, RDF/XML
**Trade-offs:**

- ✅ Maximally expressive and composable
- ✅ Rich tooling (reasoners, validators)
- ❌ Verbose, steep learning curve
- ❌ Performance issues (SPARQL slow)

---

### SPARQL

**Definition:** Query language for RDF graphs. "SQL for RDF."
**Why It Matters:** If you use RDF (Solid), you need SPARQL to query it.
**Example:**

```sparql
SELECT ?note WHERE {
  ?note rdf:type :Mnemegram .
  ?note :about :DistributedSystems .
}
```

**Trade-offs:**

- ✅ Powerful graph queries
- ❌ Performance poor at scale

---

### Lexicon System

**Definition:** Namespaced, versioned schema definitions. Used by atproto.
**Why It Matters:** Enables schema evolution without central coordination. Each app/domain defines its schemas.
**Example:** `app.bsky.feed.post` vs `com.memex.mnemegram`
**Applied to Memex:** Personal knowledge schemas as lexicons. Can extend or version without breaking.
**Trade-offs:**

- ✅ Decentralized schema evolution
- ❌ Fragmentation risk (20 different "note" schemas)

---

### Property Graph

**Definition:** Graph where nodes and edges both have properties. Alternative to RDF.
**Why It Matters:** More natural for many graph queries than triples. Used by Neo4j, graph databases.
**Example:** `(Person {name: "Alice"})-[:KNOWS {since: 2020}]->(Person {name: "Bob"})`
**Applied to Memex:** Mnemegrams as nodes, relations as edges, all with properties.
**Query Language:** Cypher (Neo4j), Gremlin
**Trade-offs (vs RDF):**

- ✅ Better performance for graph traversal
- ✅ More intuitive for developers
- ❌ Less standardized, less interoperable

---

### Triple Store

**Definition:** Database optimized for storing and querying RDF triples.
**Why It Matters:** If you use RDF, you need triple store for performance.
**Implementations:** Apache Jena, Virtuoso, Blazegraph
**Applied to Memex:** Solid pods often use triple stores for RDF data.
**Trade-offs:**

- ✅ Designed for RDF queries
- ❌ Still slower than property graphs for traversal

---

### JSON-LD

**Definition:** JSON with `@context` mapping to RDF semantics. Bridge between JSON and semantic web.
**Why It Matters:** Lets you use familiar JSON while getting RDF benefits.
**Example:**

```json
{
  "@context": "https://schema.org",
  "@type": "Person",
  "name": "Alice"
}
```

**Applied to Memex:** Export mnemegrams as JSON-LD for portability and semantic richness.

---

## Query & Retrieval (P9, P11, GAP-4)

### Vector Embeddings

**Definition:** Dense numerical representations of text (or other data) that capture semantic meaning.
**Why It Matters:** Enables semantic search beyond keyword matching. "Find notes similar to this one."
**Example:** OpenAI embeddings, sentence transformers
**Applied to Memex:** Each mnemegram gets embedding. Semantic queries by vector similarity.
**Trade-offs:**

- ✅ Semantic search, similarity ranking
- ❌ Requires ML model, computing embeddings
- ❌ Less explainable than keyword search

---

### Full-Text Search Index

**Definition:** Inverted index mapping terms to documents for fast text search.
**Why It Matters:** Basic requirement for any knowledge system. "Find notes containing X."
**Implementations:** Elasticsearch, Tantivy, SQLite FTS
**Applied to Memex:** All mnemegrams indexed for full-text queries.

---

### Graph Traversal

**Definition:** Query pattern that explores relationships by "walking" the graph.
**Why It Matters:** "Find all mnemegrams connected to X within 3 hops" requires graph traversal.
**Algorithms:** BFS, DFS, Dijkstra's
**Query Languages:** Cypher, Gremlin, SPARQL
**Applied to Memex:** Discovering non-obvious connections (R17) requires traversal.

---

### Materialized View

**Definition:** Pre-computed query result stored for fast access. Trade space for speed.
**Why It Matters:** "Most-referenced notes" could be expensive to compute on-demand. Materialize it.
**Applied to Memex:** Dashboard views (tag clouds, graph overviews) as materialized views.
**Trade-offs:**

- ✅ Fast reads
- ❌ Staleness (need refresh strategy)

---

## Decentralized Identity (P1, P6, P7)

### DID (Decentralized Identifier)

**Definition:** Globally unique identifier that doesn't depend on central authority. W3C standard.
**Why It Matters:** Portable identity. Can change data provider without losing identity.
**Example:** `did:plc:z72i7hdynmk6r22z27h6tvur` (atproto), `did:key:z6Mk...` (key-based)
**Applied to Memex:** Agent's identity is DID. Can switch PDS providers, keep identity.
**Methods:** `did:plc` (atproto), `did:web` (web-based), `did:key` (public key)

---

### DID Document

**Definition:** JSON document associated with DID specifying how to verify agent, where their data lives.
**Why It Matters:** Maps DID to PDS location, public keys, service endpoints.
**Applied to Memex:** "Agent with DID X has their mnemegrams at PDS Y."

---

## Performance & Scale (P9)

### Geospatial Index

**Definition:** Index structure for efficiently querying location-based data (lat/lon).
**Why It Matters:** "Where was I when X happened?" queries require spatial indexing.
**Implementations:** PostGIS, S2 (used by Google), H3 (Uber)
**Applied to Memex:** Location-tagged mnemegrams indexed for spatial queries (R71).
**Algorithms:** R-tree, quadtree, geohashing

---

### Inverted Index

**Definition:** Index mapping from content (words, tags) to documents. Foundation of search engines.
**Why It Matters:** Makes full-text search fast. Without it, search requires scanning all documents.
**Applied to Memex:** Essential for R50 (full-text search across heterogeneous content).

---

## Summary by Gap Priority

**For GAP-1 (Temporal Integrity):**

- Event sourcing, append-only log, commit model, temporal indexing

**For GAP-2 (Provenance):**

- Commit model, cryptographic signing, content addressing, Merkle trees

**For GAP-3 (Contextual Access):**

- Capability-based security, UCAN, WAC, ABAC

**For GAP-4 (Proactive Surfacing):**

- Vector embeddings, materialized views, graph traversal

**For P1 (Agent Sovereignty):**

- Local-first, CRDTs, PDS, DID

**For P3 (Semantic Richness):**

- RDF, property graphs, SPARQL/Cypher

**For P6 (Interoperability):**

- JSON-LD, lexicons, CAR files

---

## Terms Explicitly Excluded

These appeared in earlier glossaries but are NOT relevant based on our analysis:

- **OLTP/OLAP** - Too enterprise-specific, not implicated by use cases
- **Data mesh** - Interesting analogy but no concrete implementation need
- **Normalization** - Database theory, but personal knowledge is inherently denormalized
- **ETL pipelines** - Mentioned casually but not a core pattern we need
- **Schema-on-write vs schema-on-read** - We chose schema pluralism (P4) instead

---

## Cross-References

- [[gap-analysis]] - Which gaps these terms address
- [[system-evaluation]] - Where we found these terms in existing systems
- [[principles]] - Which principles these terms serve
