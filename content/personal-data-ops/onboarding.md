---
title: Onboarding - Personal Data Operations Domain
status: draft
created: 2025-02-05
audience: New working group members, guild newcomers
purpose: Orient newcomers to enable effective contribution
tags:
  - ai-slop
author:
  - Sonnet 4.5
---

# Onboarding: Personal Data Operations Domain

Welcome! This document helps you understand what we're doing, why it matters, and how to contribute.

---

## Start Here: The Big Picture

### What Is This Domain?

**Personal Data Operations** is the emerging practice of managing individual knowledge at scale - with the rigor of data engineering, the sovereignty of personal computing, and the richness of semantic knowledge representation.

It sits at the intersection of:

- **Personal Knowledge Management (PKM)** - Tools like Obsidian, Roam, Zettelkasten
- **Decentralized Identity & Data** - Protocols like atproto, Solid, DIDs
- **Data Engineering** - Practices from databases, data ops, event sourcing
- **Semantic Web** - Standards like RDF, linked data, ontologies

### Why Does This Matter?

**The Problem:**

- We generate massive amounts of personal data (notes, messages, locations, health metrics)
- Current tools either lock you in (Notion, Roam) or lack structure (plain files)
- No one system handles: sovereignty + semantics + scale + longevity
- Collaboration is bolted on, not designed in
- Time and provenance are afterthoughts

**The Opportunity:**

- Build infrastructure that outlives any single tool
- Enable true data sovereignty while supporting collaboration
- Make decades of personal knowledge queryable and generative
- Learn from enterprise data ops but adapt for personal scale
- Create foundation for AI assistants that truly know your context

### What Are We Building Toward?

Not a single product, but a **domain of practice** with:

- Shared vocabulary (concepts, principles, patterns)
- Requirements and specifications grounded in real use cases
- Evaluation criteria for existing and future systems
- Experiments and prototypes exploring key tensions
- Community knowledge for practitioners

---

## Essential Concepts

These are the conceptual building blocks you need to understand our work.

### From Memex Ontology

We ground our work in the [[An Ontology of Memex|Memex Ontology]], which defines:

**[[Mnemegram]]:** The shadow of experience cast into information space - the fundamental unit of capture.

**[[Agent]]:** That which interacts with the memex - you, your future self, your family, an AI assistant, etc.

**[[An Ontology of Memex#Essential Properties|Essential Properties]] (E1-E6):** What something must be to qualify as memex.

**[[An Ontology of Memex#Functional Capacities|Functions]] (F1-F9):** What memex does

**[[An Ontology of Memex#Teleological Orientations|Telos]] (T1-T11):** What memex is _for_

**Key Insight:** Essential properties, functions, and telos **co-determine** each other. No layer is foundational - they shape each other.

### Core Tensions

Personal data operations involves navigating inherent tradeoffs:

**Flexibility vs Queryability:** More flexible schemas make querying harder
**Privacy vs Discoverability:** Encryption limits what can be indexed
**Portability vs Performance:** Generic formats are slower than optimized ones
**Immutability vs Right-to-Delete:** Append-only conflicts with true deletion
**Capture Friction vs Data Quality:** Easy capture means messier data

We don't "solve" these tensions - we understand them and make informed tradeoffs.

### Adjacent Domains You Should Know

**Personal Knowledge Management (PKM):**

- Zettelkasten method
- Tools: Obsidian, Roam, Logseq, Notion
- Community: r/Zettelkasten, r/ObsidianMD
- Key figures: Niklas Luhmann, Sönke Ahrens

**Decentralized Web / Web3:**

- atproto (Bluesky)
- Solid (Tim Berners-Lee)
- IPFS, Dat/Hypercore
- DIDs (Decentralized Identifiers)

**Data Engineering:**

- Event sourcing
- CQRS (Command Query Responsibility Segregation)
- CRDTs (Conflict-Free Replicated Data Types)
- Data lineage and provenance

**Semantic Web:**

- RDF (Resource Description Framework)
- SPARQL query language
- Linked data principles
- Schema.org, FOAF, Dublin Core

You don't need to be expert in all these, but knowing they exist helps you see where ideas come from.

---

## How We Work: The Methodology

We follow **W3C working group methodology**:

1. **Use Cases** - Concrete scenarios from real needs
2. **Requirements** - What must systems do to satisfy use cases
3. **Principles** - Architectural guidelines derived from requirements
4. **Specifications** - (Future) Concrete designs that satisfy principles
5. **Implementations** - (Future) Working prototypes and systems

**Current Status:** We've completed use cases → requirements → principles. Now moving to gap analysis and experiments.

---

## What We've Built So Far

### Core Documents

**[[use-cases]]** - 19 scenarios covering individual to collective use

- Read UC-1 (Researcher traces evolution) and UC-6 (Activist under threat) for range

**[[requirements]]** - 90 requirements organized by domain

- Scan the functional domains, note which resonate with your interests

**[[principles]]** - 15 architectural principles with interdependencies

- Start with the "Essential" principles (P1, P6, P8)
- Note which principles conflict (these are key tensions)

**[[system-evaluation]]** - How existing systems score against principles

- Reveals what's missing from current tools
- Shows why no single system is adequate

**[[gap-analysis]]** - Systematic identification of universal weaknesses

- GAP-1 (Temporal Integrity) and GAP-2 (Provenance) are highest priority
- Shows where innovation is most needed

**[[glossary-engineering]]** - Technical terms that actually matter

- Only terms implicated by our analysis, not generic survey
- Organized by which gaps/principles they address

### Supplemental Documents

**[[storage-models]]** - Content-addressed, mutable, append-only, hybrid
**[[schema-approaches]]** - Ontologies, lexicons, property graphs, emergent
**[[atproto-analysis]]** - Deep dive on Bluesky's architecture
**[[design-tradeoffs]]** - 10 core tensions in the domain

---

## How to Contribute

### Phase 1: Understand the Domain (First 1-2 weeks)

**Essential Reading** (in order):

1. Read [[An Ontology of Memex]]]] - The foundation
2. Skim [[use-cases]] - Pick 2-3 that resonate with your experience
3. Read [[principles]] - Focus on Essential and Core principles
4. Skim [[gap-analysis]] - Understand what's missing

**Optional Depth:**

- [[system-evaluation]] if you use Obsidian/Roam/Notion and want to understand their limitations
- [[glossary-engineering]] for terms you encounter and don't recognize
- [[atproto-analysis]] if decentralized protocols interest you

**Check Your Understanding:**

- Can you explain what a "mnemegram" is to someone unfamiliar?
- Can you name 3 of the 7 gaps and why they matter?
- Can you articulate one core tension (e.g., flexibility vs queryability)?

### Phase 2: Find Your Angle (Weeks 2-4)

**Identify what draws you:**

- **User perspective:** Which use cases match your needs? What's missing?
- **Technical perspective:** Which gaps could you help address?
- **Domain expertise:** What adjacent knowledge do you bring? (PKM, decentralization, databases, semantic web?)
- **Practical:** Do you want to build, research, document, or test?

**Exploration Activities:**

- Try scoring your current tool(s) against the 15 principles
- Pick one gap (GAP-1 through GAP-7) and research solutions
- Add a use case we missed
- Find a system we didn't evaluate and score it

### Phase 3: Active Contribution (Ongoing)

**Ways to Contribute:**

**1. Documentation & Analysis**

- Evaluate additional systems against principles
- Write deep-dives on specific technologies (like atproto-analysis)
- Expand glossary with terms you encounter
- Document case studies from your own practice

**2. Requirements & Use Cases**

- Add use cases from your experience
- Refine existing requirements
- Map requirements to real-world systems
- Identify conflicts between requirements

**3. Technical Exploration**

- Prototype solutions to priority gaps
- Research emerging technologies (new protocols, tools)
- Performance benchmarking of approaches
- Write proof-of-concept code

**4. Community Building**

- Orient new members
- Facilitate discussions
- Synthesize working group conversations
- Connect to adjacent communities

**5. Specification Work** (Future phase)

- Help design concrete architectures
- Write technical specifications
- Define interfaces and protocols
- Create reference implementations

---

## Key Questions We're Exploring

These are open questions where we need thinking and experimentation:

### Architectural Questions

**Q1: Can event sourcing work for personal knowledge?**

- It solves temporal integrity and provenance
- But query complexity and storage costs are concerns
- Need: Prototype and measure

**Q2: What's the right level of semantic richness?**

- RDF gives maximum expressiveness but poor performance
- Plain links are fast but lose meaning
- Need: Middle-ground approaches

**Q3: How do we balance agent sovereignty with collective memory?**

- Individuals should control their data
- But families/teams need shared memory
- Need: Multi-agent models that respect both

**Q4: Can we have comprehensive automation without losing control?**

- Friction minimization requires automation
- But automation risks agency loss
- Need: Permission models for automated capture

### Domain-Specific Questions

**Q5: What should a "personal data server" for knowledge look like?**

- atproto has PDS for social data
- Solid has pods for general data
- Need: PDS designed specifically for knowledge graphs

**Q6: How do we make proactive surfacing helpful, not intrusive?**

- Recommendations require background computation
- But surprises can be jarring
- Need: Context-aware surfacing that respects agency

**Q7: What does portable provenance look like?**

- Provenance chains must survive tool migration
- Need: Standards for representing derivation

### Practical Questions

**Q8: Can individuals realistically self-host?**

- Local-first is ideal for sovereignty
- But most people won't run servers
- Need: Models that work for non-technical users

**Q9: How do we handle the "past self embarrassment" problem?**

- Full history enables reflection
- But people want to forget/delete
- Need: Graceful forgetting with integrity

**Q10: What's the migration path from existing tools?**

- People have years of notes in Obsidian, Roam, Notion
- Need: Import tools that preserve structure

---

## Resources for Going Deeper

### Communities

**Personal Knowledge Management:**

- r/Zettelkasten
- r/ObsidianMD

**Decentralized Tech:**

- atproto Discord
- Solid Community Forum
- IPFS Community

**Data Engineering:**

- Martin Kleppmann's "Designing Data-Intensive Applications"
- Event Sourcing patterns (EventStore documentation)

**Semantic Web:**

- W3C Semantic Web Activity
- RDF 1.1 Primer

### Key Papers & Articles

**Local-First Software** (Ink & Switch)
https://www.inkandswitch.com/local-first/

**As We May Think** (Vannevar Bush, 1945) - Original memex vision
https://www.theatlantic.com/magazine/archive/1945/07/as-we-may-think/303881/

**atproto Documentation**
https://atproto.com/

**Solid Specification**
https://solidproject.org/

**Event Sourcing** (Martin Fowler)
https://martinfowler.com/eaaDev/EventSourcing.html

---

## Vocabulary Quick Reference

**Terms from Memex Ontology:**

- **Mnemegram** - Unit of captured experience
- **Agent** - Who/what interacts with memex
- **Assertion** - Claim about mnemegram or relation
- **Referent** - Persistent entity referenced across mnemegrams
- **Provenance** - Origin-tracking chain

**Terms from Personal Data Ops:**

- **Temporal Integrity** - Preserving time as first-class dimension
- **Agent Sovereignty** - Individual control over data
- **Schema Pluralism** - Multiple concurrent schemas
- **Contextual Access** - Permissions adapted to context
- **Proactive Surfacing** - System-initiated recommendations

**Key Technical Terms:**

- **Event Sourcing** - State as sequence of events
- **CRDT** - Conflict-free replicated data types
- **Content Addressing** - Reference by hash, not location
- **Capability-Based Security** - Access as unforgeable tokens
- **RDF** - Resource Description Framework (triples)
- **DID** - Decentralized Identifier

See [[glossary-engineering]] for complete technical glossary.

---

## Working Group Norms

### Communication

- **Asynchronous first** - Document in digital garden, discuss in Discord
- **Show, don't just tell** - Prototypes and examples over pure theory
- **Cite sources** - Link to use cases, requirements, principles that inform your thinking
- **Be specific** - "This violates P8 (Protection)" is better than "This seems insecure"

### Decision Making

- **Requirements-driven** - Proposals should satisfy identified requirements
- **Principle-aligned** - Designs should score well against our 15 principles
- **Tension-aware** - Acknowledge tradeoffs explicitly
- **Experiment-friendly** - Try things, measure, learn

### What We Value

- **First principles thinking** - Why, not just what
- **Intellectual humility** - "I don't know" is valid
- **Adjacent expertise** - Bringing insights from other domains
- **Practical grounding** - Use cases from lived experience
- **Long-term thinking** - Decades, not quarters

### What We Avoid

- **Technology solutionism** - Starting with "what if we used X?" without grounding in requirements
- **Perfect-is-enemy-of-good** - Prototypes > perfection
- **Bikeshedding** - Focus on high-impact gaps, not minutiae
- **Gatekeeping** - All backgrounds welcome, meet people where they are

---

## Your First Contribution

**Easiest Onramp:**

1. **Add a use case** - What do YOU need from personal data operations? Write it up following the UC template in [[use-cases]]

2. **Score your current tool** - Use Obsidian/Roam/Notion/etc? Score it against our 15 principles in your own doc. What did you learn?

3. **Pick a term** - Choose one from [[glossary-engineering]] that's new to you. Research it deeper. Write a tutorial or example.

4. **Find a gap** - Look at [[gap-analysis]]. Pick GAP-1 through GAP-7. Research how it could be solved. What technologies exist? What's missing?

5. **Document your practice** - How do you currently manage personal knowledge? What works? What's broken? This lived experience is valuable.

**Share your contribution in Discord and we'll help integrate it into the digital garden.**

---

## FAQ for Newcomers

**Q: Do I need to be technical to contribute?**
A: No. Use case documentation, domain analysis, and conceptual work are equally valuable. We need both builders and thinkers.

**Q: What if I disagree with a principle or requirement?**
A: Great! Document your reasoning, link to which use cases you think are misunderstood, propose alternatives. Productive disagreement strengthens the work.

**Q: Can I just lurk and learn?**
A: Absolutely. Many people benefit from following along. Contribute when ready.

**Q: I use [tool X], is it doomed?**
A: No tool is perfect. Our evaluation helps you understand tradeoffs and inform your choices. Use what works for you.

**Q: Is this academic or practical?**
A: Both. We want rigorous foundations AND working implementations. Theory informs practice; practice tests theory.

**Q: What's the timeline?**
A: Open-ended. This is a long-term domain-building effort, not a product launch. Contribute at your pace.

**Q: Who leads this?**
A: The working group is collaborative. Different people drive different efforts. Leadership is earned through contribution.

---

## Next Steps

1. **Read the essentials** (memex ontology, use cases, principles)
2. **Introduce yourself in Discord** - What brings you here? What's your background?
3. **Pick one contribution** from the "Your First Contribution" section
4. **Ask questions** - If something's unclear, others probably wonder too

Welcome to the Personal Data Operations working group. We're glad you're here.

---

## Document Status

**Last Updated:** 2025-02-05
**Maintained By:** Working group members
**Feedback:** Suggest improvements in Discord or via pull request

---

## Related Documents

- [[An Ontology of Memex]] - Foundational ontology
- [[use-cases]] - 19 scenarios we're addressing
- [[principles]] - 15 architectural principles
- [[gap-analysis]] - What's missing from current systems
- [[glossary-engineering]] - Technical vocabulary
