---
title: Personal Data Operations - Domain Exploration
status: draft
created: 2025-02-04
updated: 2025-02-05
tags:
  - ai-slop
---

# Personal Data Operations - Domain Exploration

## New Here? Start With Onboarding

**👉 Read [[onboarding]] first** - It explains what we're doing, why it matters, and how to contribute.

---

## Purpose

This collection maps the engineering landscape of personal data operations - the practices, patterns, and primitives for managing individual knowledge stores at scale with proper access control, portability, and semantic richness.

## What is Personal Data Operations?

Personal data operations sits at the intersection of:

- **Personal Knowledge Management (PKM)** - individual sense-making and knowledge capture
- **Data Operations (DataOps)** - engineering practices for data lifecycle management
- **Decentralized Identity** - user sovereignty over data and access
- **Semantic Web** - meaning-preserving data representation

Unlike enterprise data operations (focused on organizational analytics) or traditional PKM (focused on note-taking), personal data ops addresses:

- How individuals manage large-scale personal knowledge graphs
- How access control works when you are both data owner and primary user
- How schemas evolve with personal understanding
- How data moves between contexts without vendor lock-in

---

## Quick Navigation

### Start Here

- **[[onboarding]]** - Complete newcomer guide (READ THIS FIRST)
- **[[An Ontology of Memex]]** - Foundational ontology (Essential, Functional, Teleological)

### Core Work Products

- **[[use-cases]]** - 19 scenarios from individual to collective use
- **[[requirements]]** - 90 requirements organized by functional domain
- **[[principles]]** - 15 architectural principles with interdependencies
- **[[system-evaluation]]** - How Obsidian, Roam, atproto, Solid, Notion score
- **[[gap-analysis]]** - 7 critical gaps where all systems fail
- **[[glossary-engineering]]** - Technical terms that actually matter

### Deep Dives

- **[[storage-models]]** - Content-addressed, mutable, append-only, hybrid
- **[[schema-approaches]]** - Ontologies, lexicons, property graphs
- **[[atproto-analysis]]** - Bluesky architecture through memex lens
- **[[design-tradeoffs]]** - 10 core tensions in the domain

---

## Methodology: W3C Working Group Approach

We follow systematic domain development:

1. ✅ **Use Cases** → Concrete scenarios from real needs
2. ✅ **Requirements** → What systems must do (90 requirements identified)
3. ✅ **Principles** → Architectural guidelines (15 principles derived)
4. ✅ **System Evaluation** → How existing tools measure up
5. ✅ **Gap Analysis** → What's universally missing
6. 🔄 **Specifications** → Concrete designs (in progress)
7. 🔄 **Implementations** → Working prototypes (future)

**Current Phase:** Moving from analysis to specification and experimentation.

---

## Key Findings

### Critical Gaps (All Systems Weak)

1. **Temporal Integrity** - Only atproto tracks full history properly
2. **Provenance Traceability** - Almost no automatic lineage tracking
3. **Contextual Access Control** - Work/personal boundaries poorly supported
4. **Proactive Surfacing** - Recommendations rare, mostly query-driven

### Essential Principles (Must-Have)

- **P1: Agent Sovereignty** - Individual control over data
- **P6: Interoperability by Design** - Must outlive any tool
- **P8: Protection by Default** - Security is foundational

### System Scores (out of 30)

- **atproto:** 20/30 (best, but not designed for personal knowledge)
- **Solid:** 19/30 (meets minimum viability, but complex)
- **Obsidian:** 18/30 (good sovereignty, weak on time/provenance)
- **Notion:** 13/30 (fails minimum viability - vendor lock-in)
- **Roam:** 11/30 (fails minimum viability - vendor lock-in)

---

## For the Working Group

This material should help us:

1. **Identify knowledge gaps** worth exploring
2. **Build shared vocabulary** across different backgrounds
3. **Prioritize experiments** and learning labs
4. **Orient newcomers** to the domain space
5. **Evaluate technologies** systematically

---

## Contributing

See **[[onboarding]]** for detailed contribution guide.

**Quick ways to contribute:**

- Add use cases from your experience
- Evaluate a system we haven't covered
- Research solutions to priority gaps (GAP-1, GAP-2, GAP-3)
- Document your personal knowledge practice
- Expand glossary with terms you encounter

---

## Status & Roadmap

### Completed (Phase 1-2)

- ✅ 19 use cases documented
- ✅ 90 requirements extracted
- ✅ 15 principles derived with interdependencies
- ✅ 5 major systems evaluated
- ✅ 7 critical gaps identified
- ✅ Engineering glossary (40+ terms)
- ✅ Onboarding guide

### In Progress (Phase 3)

- 🔄 Additional system evaluations
- 🔄 Experiments addressing priority gaps
- 🔄 Technical specifications
- 🔄 Prototype architectures

### Future (Phase 4+)

- ⏭️ Reference implementations
- ⏭️ Interoperability specifications
- ⏭️ Community tooling
- ⏭️ Integration patterns

---

## Open Questions

High-priority questions needing exploration:

**Q1:** Can event sourcing work for personal knowledge at scale?
**Q2:** What's the right balance of semantic richness vs performance?
**Q3:** How do we enable collective memory while preserving individual sovereignty?
**Q4:** What should a "personal data server" for knowledge look like?
**Q5:** Can we have comprehensive automation without losing agency?

See [[onboarding#Key Questions We're Exploring]] for complete list.

---

## Community

**Discord:** [Link to your Discord]
**Contributing:** See [[onboarding]]
**License:** [Your license choice]

---

## Document History

**Created:** 2025-02-04
**Major Update:** 2025-02-05 (Added onboarding, system evaluation, gap analysis, glossary)
**Status:** Draft - Initial exploration phase
**Next Review:** After first round of experiments

---

## Cross-References

- **Memex Working Group:** [[index]] (main vault)
- **Foundational Ontology:** [[An Ontology of Memex]]
- **Start Here for Newcomers:** [[onboarding]]
