---
title: Design Tensions
domain: unresolved questions
status: ongoing
tags:
  - ai-slop
author:
  - Sonnet 4.5
uuid: e5e63169-f498-4394-a924-d6b7bbf62a47
share: true
---
# Core Design Tensions in Personal Data Operations

These are the fundamental tradeoffs that make this domain hard. No "right" answer - different use cases need different balances.

## 1. Flexibility vs Queryability

**The tension:** The more flexible your data model, the harder it is to write efficient queries.

**Examples:**

- **RDF:** Can represent anything, but SPARQL queries can be slow/complex
- **Strict schema:** Fast queries, but breaks when understanding evolves
- **Property graphs:** Middle ground, but can become soup

**Who's wrestling with this:**

- Roam/Logseq: Very flexible (everything is a block), hard to do structured queries
- Notion/Airtable: More structured, better queries, but rigid

**For personal knowledge:**

- Your thinking evolves - you need flexibility
- But you also want to find things - you need structure
- Can AI help bridge this gap? (LLMs can query unstructured data)

---

## 2. Privacy vs Discoverability

**The tension:** Fine-grained access control makes it hard to index and search.

**Examples:**

- **Full encryption:** Totally private, but can't search without decrypting
- **Plaintext indexing:** Searchable, but exposes metadata
- **Homomorphic encryption:** Search on encrypted data, but slow/complex

**Who's wrestling with this:**

- Solid: RDF lets you specify access per-triple, but querying across permissions is hard
- atproto: Public-first design, privacy is bolted on

**For personal knowledge:**

- Some notes are private, some shareable
- You want full-text search across everything
- How do you index without revealing?

---

## 3. Portability vs Performance

**The tension:** Generic formats let you switch tools, but optimized formats are faster.

**Examples:**

- **Plain markdown:** Portable, but slow for graph queries
- **SQLite:** Fast, but tool-specific
- **RDF:** Portable, but verbose

**Who's wrestling with this:**

- Obsidian: Markdown (portable) + graph (in-memory, fast but not portable)
- Roam: Proprietary graph, vendor lock-in

**For personal knowledge:**

- You want to outlive any single app
- But you also want instant search/traversal
- Hybrid: store in portable format, index in tool-specific cache?

---

## 4. Immutability vs Right-to-Delete

**The tension:** Content addressing needs immutable data, but privacy law requires deletion.

**Examples:**

- **IPFS:** Content addressed, but you can't unpublish
- **Git:** History is permanent (without rewriting)
- **Event sourcing:** Append-only, deletion is "add tombstone"

**Who's wrestling with this:**

- GDPR compliance in blockchains
- Content moderation on decentralized platforms

**For personal knowledge:**

- You want a record of how your thinking evolved
- But you also want to truly delete embarrassing old takes
- Can you have append-only history with selective amnesia?

---

## 5. Single-User Optimization vs Multi-User Potential

**The tension:** Personal knowledge is mostly for you, but sometimes you want to share/collaborate.

**Examples:**

- **Single-user:** Simpler sync, no permission complexity
- **Multi-user:** Need ACLs, conflict resolution, federation

**Who's wrestling with this:**

- Obsidian: Great for individuals, publish is afterthought
- Notion: Built for teams, personal use is almost accidental

**For personal knowledge:**

- 90% of notes are just for you
- But 10% you want to share/collaborate on
- Do you design for the 90% or the 10%?

---

## 6. Rich Semantics vs Adoption Friction

**The tension:** Powerful ontologies enable reasoning, but have steep learning curves.

**Examples:**

- **OWL/RDFS:** Can infer relationships, but complex
- **Plain links:** Everyone understands `[[wikilinks]]`
- **Typed relations:** More precise, but requires thinking about edge types

**Who's wrestling with this:**

- Semantic web community: Powerful standards, low adoption
- PKM tools: Simple models, high adoption, less power

**For personal knowledge:**

- Do you need formal semantics for "notes to self"?
- Or is emergence from simple links enough?
- Can defaults handle 80% while allowing power users to opt into complexity?

---

## 7. Capture Friction vs Data Quality

**The tension:** Making capture easy means messy data; enforcing structure means less gets captured.

**Examples:**

- **Quick capture:** Voice notes, screenshots, "inbox" - high volume, low structure
- **Structured entry:** Forms, templates - clean data, but slow

**Who's wrestling with this:**

- Every notes app ever
- Scientists: lab notebooks vs structured databases

**For personal knowledge:**

- Ideas arrive messy - need low friction to capture
- But querying requires structure
- Hybrid: capture messy, structure later? (AI-assisted?)

---

## 8. Current State vs Historical Evolution

**The tension:** Do you want to see what you think NOW, or trace how you got here?

**Examples:**

- **Snapshot model:** Current state, overwrite on change
- **Event sourcing:** Full history, derive current state
- **Git model:** History preserved, but "current" is HEAD

**Who's wrestling with this:**

- Researchers: Version control for papers vs final draft
- Personal journals: Daily entries (temporal) vs evergreen notes (timeless)

**For personal knowledge:**

- Some thoughts are timeless (principles)
- Some are timestamped (observations)
- Can one system handle both?

---

## 9. Schema-First vs Schema-Emergent

**The tension:** Define structure upfront (schema-first) or let it emerge from use (schema-emergent)?

**Examples:**

- **Schema-first:** Databases, Notion databases - think before you build
- **Schema-emergent:** Zettelkasten, tags - structure appears from patterns

**Who's wrestling with this:**

- Data modeling best practices
- PKM philosophies (top-down vs bottom-up)

**For personal knowledge:**

- You don't know what you'll learn in advance
- But some structure helps thinking
- Progressive formalization?

---

## 10. Local-First vs Cloud-Native

**The tension:** Local = privacy + offline, Cloud = sync + access from anywhere.

**Examples:**

- **Local-first:** Obsidian, files on disk - you own it, but sync is hard
- **Cloud-native:** Notion, Roam - seamless sync, but vendor dependency

**Who's wrestling with this:**

- Ink & Switch research on local-first software
- Every SaaS vs self-hosted debate

**For personal knowledge:**

- You want it available everywhere
- But you want to own your data
- CRDTs help, but add complexity

---

## Meta-Tension: Premature Optimization vs Technical Debt

Building perfect infrastructure before you have knowledge → over-engineering
Building no infrastructure and just capturing → future query/migration hell

How much structure is "just enough"?

---

## Questions for the Working Group

1. Which tensions matter most for our use cases?
2. Are there existing systems that balance these well?
3. What experiments would help us understand tradeoffs?
4. Can we build hybrid systems that let users choose their balance?