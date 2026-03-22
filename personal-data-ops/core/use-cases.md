---
title: Use Cases for Personal Data Operations
status: draft
created: 2025-02-05T00:00:00.000Z
methodology: W3C working group approach
related:
  - "[[An Ontology of Memex]]"
tags:
  - ai-slop
author:
  - Sonnet 4.5
uuid: 988d948f-d844-4a3e-948f-9cdf1c0fbe46
share: true
---
# Use Cases for Personal Data Operations

This document captures concrete scenarios that personal data operations infrastructure must support. Each use case identifies actors, goals, memex functions involved, and implied requirements.

**Approach:** Following W3C working group methodology, we begin with use cases to derive requirements, then principles, then specifications.

---

## UC-1: Researcher Traces Conceptual Evolution

**Actor:** Academic researcher (Agent)

**Goal:** Understand how their thinking about a concept has changed over 3 years

**Scenario:**

- Researcher queries for all mnemegrams related to "distributed systems"
- System surfaces mnemegrams chronologically with context
- Researcher observes shift from "blockchain enthusiasm" to "CRDT pragmatism"
- System reveals which readings, conversations, experiments influenced the shift

**Memex Functions Involved:**

- F4 (Retrieval)
- F4.1 (Surfacing)
- F5 (Relating)
- F6 (Versioning)

**Teleological Orientation:**

- T7 (To Reflect)
- T4 (To Orient)

**Requirements Implied:**

- **R1:** System must preserve temporal ordering of mnemegrams
- **R2:** System must maintain provenance chains (what influenced what)
- **R3:** Retrieval must support semantic queries, not just keyword matching
- **R4:** System must support "time-travel" views (what did I know when?)

---

## UC-2: Knowledge Worker Shares Subset with Collaborators

**Actor:** Knowledge worker with personal memex

**Goal:** Share work-related mnemegrams with colleagues while keeping personal notes private

**Scenario:**

- Worker has 5 years of intermingled personal and professional mnemegrams
- Needs to grant colleagues access to "project X" related content
- Some mnemegrams are purely professional, some are personal, some are both
- Access must be revocable and auditable

**Memex Functions Involved:**

- F8 (Transmission)
- F9 (Protection)

**Teleological Orientation:**

- T9 (To Commune)
- T5 (To Hold Accountable)

**Requirements Implied:**

- **R5:** System must support fine-grained access control (not just all-or-nothing)
- **R6:** Access control must work at mnemegram level, not just collection level
- **R7:** System must handle mnemegrams that belong to multiple contexts
- **R8:** Sharing must not require duplicating or forking the memex
- **R9:** Access grants must be auditable (who saw what, when)

---

## UC-3: Individual Migrates Between Tools

**Actor:** Long-time note-taker

**Goal:** Move 10 years of knowledge from Tool A to Tool B without losing structure

**Scenario:**

- Started with Evernote (2015)
- Moved to Roam (2020)
- Now wants to try Obsidian (2025)
- Each tool has different primitives (notebooks vs blocks vs files)
- Relationships between notes must be preserved
- Doesn't want to be locked into any single tool forever

**Memex Functions Involved:**

- F8 (Transmission)
- F6 (Versioning)

**Teleological Orientation:**

- T1 (To Persist)
- T2 (To Accumulate)

**Essential Properties at Risk:**

- E5 (Interpretability - schemas differ across tools)

**Requirements Implied:**

- **R10:** Mnemegrams must have tool-independent representation
- **R11:** Relations must be preserved across schema transformations
- **R12:** System must support schema evolution without data loss
- **R13:** Export format must be human-readable (outlive the tools)

---

## UC-4: Writer Generates New Work from Archive

**Actor:** Writer with extensive personal archive

**Goal:** Create essay by synthesizing themes across 50+ reading notes

**Scenario:**

- Writer has notes on 50 books about "attention economy"
- Wants to find unexpected connections between texts
- Needs to see which ideas appear repeatedly vs uniquely
- Generated essay should reference source mnemegrams (provenance)
- Original notes remain unchanged; essay is new generative content

**Memex Functions Involved:**

- F7 (Generation)
- F5 (Relating)
- F4.1 (Surfacing)

**Teleological Orientation:**

- T8 (To Generate)
- T3 (To Connect)

**Requirements Implied:**

- **R14:** System must support graph traversal and pattern detection
- **R15:** Generated content must maintain provenance to source mnemegrams
- **R16:** System must distinguish captured vs generative information
- **R17:** Surfacing should help discover non-obvious connections

---

## UC-5: Family Maintains Multi-Generational Memory

**Actor:** Family collective (multi-agent)

**Goal:** Preserve and share family stories, photos, documents across generations

**Scenario:**

- Grandparent contributes mnemegrams (photos, oral histories)
- Parents add context and assertions (dates, relationships, stories)
- Grandchildren retrieve and ask questions
- Some mnemegrams are private (medical records), some are shared
- System must outlast individual members (generational transmission)

**Memex Functions Involved:**

- F1 (Inscription)
- F2 (Assertion)
- F8 (Transmission)
- F9 (Protection)

**Teleological Orientation:**

- T6 (To Transmit)
- T9 (To Commune)
- T10 (To Identify)

**Requirements Implied:**

- **R18:** System must support multiple agents with different roles
- **R19:** Mnemegrams must persist beyond creating agent's lifetime
- **R20:** Assertions can be added by agents other than original creator
- **R21:** Access control must support "family" as unit, not just individuals
- **R22:** System must be maintainable across decades (not dependent on startup survival)

---

## UC-6: Activist Manages Research Under Threat

**Actor:** Human rights activist

**Goal:** Document abuses while protecting sources and self

**Scenario:**

- Captures sensitive mnemegrams (testimonies, evidence)
- Needs to selectively reveal to journalists/lawyers without exposing sources
- Must be able to prove authenticity (cryptographic verification)
- Must be able to delete if device is seized
- May need to share with future investigators after own death/disappearance

**Memex Functions Involved:**

- F9 (Protection)
- F1 (Inscription)
- F8 (Transmission)

**Teleological Orientation:**

- T5 (To Hold Accountable)
- T6 (To Transmit)

**Tension with:**

- T11 (To Forget - must be able to truly delete)

**Requirements Implied:**

- **R23:** System must support cryptographic verification of mnemegrams
- **R24:** Deletion must be irrevocable (not just tombstones)
- **R25:** Access control must support capability-based delegation
- **R26:** System must support "dead man's switch" transmission
- **R27:** Protection must work offline and under duress

---

## UC-7: Student Builds Learning Portfolio

**Actor:** Graduate student

**Goal:** Track learning journey and demonstrate growth to advisors/employers

**Scenario:**

- Captures reading notes, lecture summaries, project reflections over 5 years
- Wants to show progression from novice to competent
- Needs to export specific collections for applications (portfolio for job)
- Some content is exploratory/rough, some is polished
- System should help identify knowledge gaps

**Memex Functions Involved:**

- F1 (Inscription)
- F2 (Assertion)
- F4.1 (Surfacing)
- F7 (Generation)

**Teleological Orientation:**

- T2 (To Accumulate)
- T7 (To Reflect)
- T4 (To Orient)

**Requirements Implied:**

- **R28:** System must support annotation of mnemegrams with maturity/status
- **R29:** Collections must be exportable in presentation-ready formats
- **R30:** System should surface gaps (what's underexplored)
- **R31:** Retrieval should support "show my progression on X"

---

## UC-8: Organization Decommissions Employee Memex

**Actor:** Company IT managing employee departure

**Goal:** Preserve work product while respecting employee privacy

**Scenario:**

- Employee leaves company, has 3 years of work in personal memex
- Company needs access to work deliverables and decisions
- Employee's personal thoughts/notes should remain private
- Some mnemegrams are ambiguous (work email with personal commentary)
- Need to cleanly separate without destroying either

**Memex Functions Involved:**

- F9 (Protection)
- F8 (Transmission)

**Teleological Orientation:**

- T11 (To Forget - selective)
- T5 (To Hold Accountable)

**Requirements Implied:**

- **R32:** System must support context-based partitioning
- **R33:** Assertions can indicate "work context" vs "personal context"
- **R34:** Deletion of personal context must not break work context references
- **R35:** Audit trail must show what was preserved/deleted

---

## Status and Next Steps

**Current Status:** Initial use case collection (8 cases documented)

**Potential Additional Use Cases:**

- Multi-device sync scenarios
- AI-augmented annotation and surfacing
- Cross-memex federation (multiple people's personal memexes interacting)
- Compliance with data regulations (GDPR, etc.)
- Performance at scale (decades of daily capture)

**Next Steps:**

1. Review and refine existing use cases
2. Extract consolidated requirements document
3. Derive architectural principles from requirements
4. Map existing technologies against requirements

---

## Cross-References

- [[An Ontology of Memex]] - Foundational ontology these use cases implement
- [[requirements]] - (To be created: consolidated requirements extracted from use cases)
- [[principles]] - (To be created: architectural principles derived from requirements)

## UC-9: Quantified Self with Data Exhaust Capture

**Actor:** Individual practicing deep quantified self

**Goal:** Automatically capture and correlate all personal data streams for insights

**Scenario:**

- System captures location data, health metrics (heart rate, sleep), digital activity
- User wants to discover correlations ("I sleep better when I walk >10k steps")
- Data comes from multiple sources (phone, watch, apps, browser)
- Analysis should surface unexpected patterns
- Must work with near-zero friction - manual logging fails

**Memex Functions Involved:**

- F1 (Inscription - automated)
- F4.1 (Surfacing)
- F5 (Relating)
- F7 (Generation - insight creation)

**Teleological Orientation:**

- T7 (To Reflect)
- T4 (To Orient)
- T2 (To Accumulate)

**Requirements Implied:**

- **R36:** System must support automated capture from multiple data sources
- **R37:** Integration must be low-friction (ideally zero manual input)
- **R38:** System must support temporal correlation analysis
- **R39:** Different data types (location, biometric, behavioral) must be relatable
- **R40:** Privacy-preserving local processing (sensitive health data)

**Source:** Workshop Round 1 (Sasha/Zoravur), use-cases/quantified self.md

---

## UC-10: Relationship Management and Social Graph Tracking

**Actor:** Individual maintaining personal and professional relationships

**Goal:** Track relationship history, communication patterns, and maintenance needs

**Scenario:**

- System captures interactions with people (meetings, messages, calls)
- User wants reminders ("haven't talked to X in 3 months - relationship half-life expiring")
- Should surface context before meetings ("last talked about their job search")
- Tracks relationship categories (family, close friends, professional, acquaintances)
- Supports "grouping" communications for efficiency
- Private data - cannot leak to third parties

**Memex Functions Involved:**

- F1 (Inscription)
- F2 (Assertion - relationship metadata)
- F4 (Retrieval - pre-meeting context)
- F4.1 (Surfacing - maintenance reminders)
- F5 (Relating - social graph)

**Teleological Orientation:**

- T9 (To Commune)
- T4 (To Orient)
- T6 (To Transmit - maintaining connections)

**Requirements Implied:**

- **R41:** System must model entities (people) and their relationships
- **R42:** Temporal decay functions ("relationship half-life")
- **R43:** Context retrieval based on agent queries
- **R44:** Privacy: relationship data is especially sensitive
- **R45:** Integration with communication platforms (email, messaging)

**Source:** Workshop Rounds 1-3 (Erin/Paul, Alex/Subline, Dave/Zoravur)

---

## UC-11: Social Media and Bookmark Ingestion

**Actor:** Individual consuming content across platforms

**Goal:** Preserve bookmarks, saved posts, and annotations from social platforms

**Scenario:**

- User saves Twitter threads, Reddit posts, YouTube videos
- Platforms change/die, links rot, accounts get suspended
- Wants full-text searchable archive of saved content
- Should preserve context (why did I save this? what was I thinking about then?)
- Needs to work across multiple platforms

**Memex Functions Involved:**

- F1 (Inscription)
- F2 (Assertion - personal annotations)
- F4 (Retrieval)
- F6 (Versioning - content may change/disappear)

**Teleological Orientation:**

- T1 (To Persist)
- T2 (To Accumulate)

**Requirements Implied:**

- **R46:** System must ingest content from external platforms via APIs
- **R47:** Content must be preserved locally (not just links)
- **R48:** Capture must preserve context (thread structure, replies)
- **R49:** System must handle platform shutdown gracefully
- **R50:** Full-text search across heterogeneous content types

**Source:** use-cases/social media ingestion.md, use-cases/bookmarks.md

---

## UC-12: AI Assistant with Personal Context

**Actor:** Individual with comprehensive personal memex

**Goal:** AI assistant that knows personal context and can act on user's behalf

**Scenario:**

- AI has access to user's full memex (with permission)
- Can answer questions using personal knowledge ("where did I read about X?")
- Can execute tasks ("schedule meeting with person Y, avoid times when I'm low energy")
- Must respect privacy boundaries (what AI can access/share)
- User wants control over what AI learns and remembers

**Memex Functions Involved:**

- F4 (Retrieval - AI queries memex)
- F4.1 (Surfacing - AI proactively offers context)
- F7 (Generation - AI creates summaries, drafts)
- F9 (Protection - granular AI access control)

**Teleological Orientation:**

- T4 (To Orient)
- T7 (To Reflect)
- T8 (To Generate)

**Requirements Implied:**

- **R51:** API for programmatic access to memex by agents
- **R52:** Fine-grained permission model for AI access
- **R53:** Audit trail of AI queries and actions
- **R54:** Ability to revoke AI access to specific mnemegrams
- **R55:** Clear boundary between AI-generated and human-captured content

**Source:** use-cases/ai assistant.md, Workshop (Erin's "hyper competent personal assistant")

---

## UC-13: Task and Project Management with Context

**Actor:** Individual managing multiple projects and commitments

**Goal:** Todo lists that integrate with broader personal knowledge context

**Scenario:**

- Tasks are not isolated - they connect to notes, research, decisions
- "Write blog post" task should link to research notes, drafts, references
- System should surface relevant context when working on task
- Tasks evolve - what started as "research X" becomes "write paper on X"
- Needs to integrate with calendar, energy levels, deadlines

**Memex Functions Involved:**

- F1 (Inscription - task creation)
- F2 (Assertion - task metadata: priority, status, context)
- F4 (Retrieval - context for task)
- F5 (Relating - tasks to mnemegrams)
- F6 (Versioning - task evolution)

**Teleological Orientation:**

- T4 (To Orient)
- T5 (To Hold Accountable)

**Requirements Implied:**

- **R56:** Tasks are first-class entities with rich context
- **R57:** Bidirectional links between tasks and knowledge
- **R58:** Task queries should surface relevant mnemegrams
- **R59:** Support for task transformation (research → draft → publish)
- **R60:** Integration with temporal data (deadlines, schedules)

**Source:** use-cases/todo lists.md, Workshop (Ryan: "task and project management")

---

## UC-14: Collaborative Knowledge Building

**Actor:** Study group or research collective

**Goal:** Shared knowledge space with individual contributions and attribution

**Scenario:**

- Multiple people contribute mnemegrams to shared space
- Each person's contributions remain attributable
- Can distinguish "consensus knowledge" from "individual interpretation"
- Some content is shared, some remains private
- Group can build on each other's work
- Social accountability: "group members can see if you're not contributing"

**Memex Functions Involved:**

- F1 (Inscription - multi-agent)
- F2 (Assertion - attribution, consensus)
- F8 (Transmission - controlled sharing)
- F9 (Protection - hybrid private/shared)

**Teleological Orientation:**

- T2 (To Accumulate - collective)
- T9 (To Commune)
- T5 (To Hold Accountable)

**Requirements Implied:**

- **R61:** Multi-agent authorship with clear attribution
- **R62:** Distinction between personal and shared mnemegrams
- **R63:** Consensus mechanisms (this claim is accepted by group)
- **R64:** Activity visibility for social accountability
- **R65:** Merge/fork operations for diverging interpretations

**Source:** Workshop Round 3 (Dave/Alex: "collaborative accountable research management")

---

## UC-15: News and Information Provenance Tracking

**Actor:** Individual consuming news and analysis

**Goal:** Track source and evolution of claims across information ecosystem

**Scenario:**

- Sees claim repeated across multiple outlets
- Wants to trace back to original source
- Documents how claim evolved/mutated as it spread
- Distinguishes primary sources from commentary
- Can query "who else reported on this? how did framing differ?"

**Memex Functions Involved:**

- F1 (Inscription)
- F2 (Assertion - provenance metadata)
- F5 (Relating - claim genealogy)
- F6 (Versioning - claim evolution)

**Teleological Orientation:**

- T3 (To Connect - tracing relationships)
- T5 (To Hold Accountable)
- T7 (To Reflect - media literacy)

**Requirements Implied:**

- **R66:** Graph queries for provenance chains
- **R67:** Support for "same claim, different framings"
- **R68:** Temporal ordering of claim appearance
- **R69:** Distinction between primary and secondary sources
- **R70:** Integration with web archive/preservation

**Source:** Workshop Round 3 (Sasha/Ryan F: "news information provenance system")

---

## UC-16: Event and Location Context Logging

**Actor:** Individual tracking lived experience spatially and temporally

**Goal:** Automatic capture of where/when/with-whom for life events

**Scenario:**

- System logs location, time, people present
- User adds annotations ("had great conversation about X")
- Can query "where was I when Y happened?"
- Can query "who was I with when we discussed Z?"
- Location data enables serendipity discovery ("I was near that place before")
- Privacy: location history is sensitive

**Memex Functions Involved:**

- F1 (Inscription - automated)
- F2 (Assertion - context annotations)
- F4 (Retrieval - spatiotemporal queries)
- F5 (Relating - events, people, places)

**Teleological Orientation:**

- T1 (To Persist - memory preservation)
- T7 (To Reflect)
- T10 (To Identify - life continuity)

**Requirements Implied:**

- **R71:** Geospatial indexing and query support
- **R72:** Temporal indexing (when)
- **R73:** Entity tracking (people, places)
- **R74:** Privacy-preserving location storage
- **R75:** Automated capture with manual annotation

**Source:** Workshop Round 2 (Jordy/Erin: "event log, GIS")

---

## UC-17: Algorithmic Reflection and Usage Analysis

**Actor:** Individual concerned about digital behavior patterns

**Goal:** Understand and control own usage patterns and algorithmic influences

**Scenario:**

- Track screen time, app usage, content consumption
- Identify patterns ("I doom-scroll when anxious")
- Set interventions ("remind me if I've been on Twitter >30 min")
- Understand algorithmic influence ("am I in a filter bubble?")
- Want agency over attention and behavior

**Memex Functions Involved:**

- F1 (Inscription - usage tracking)
- F4.1 (Surfacing - pattern alerts)
- F7 (Generation - insight creation)

**Teleological Orientation:**

- T7 (To Reflect)
- T4 (To Orient - behavioral awareness)

**Requirements Implied:**

- **R76:** Behavioral data capture (usage logs)
- **R77:** Pattern detection and anomaly alerts
- **R78:** Intervention system (notifications, blocks)
- **R79:** Privacy: usage data stays local
- **R80:** Visualization of patterns over time

**Source:** Workshop (Sasha: "algorithmic reflection"), 2025-01-29 Notes

---

## UC-18: Decision and Product Management Log

**Actor:** Product manager or decision-maker

**Goal:** Document decisions, rationale, and outcomes over time

**Scenario:**

- Records decision made, options considered, reasoning
- Months later: review what was decided and why
- Can query "what decisions did we make about feature X?"
- Links decisions to outcomes (was it the right call?)
- Organizational memory: survives personnel changes

**Memex Functions Involved:**

- F1 (Inscription)
- F2 (Assertion - decision metadata)
- F4 (Retrieval - decision history)
- F5 (Relating - decisions to outcomes)
- F6 (Versioning - evolution of thinking)

**Teleological Orientation:**

- T5 (To Hold Accountable)
- T7 (To Reflect - learning from decisions)
- T2 (To Accumulate - organizational knowledge)

**Requirements Implied:**

- **R81:** Structured decision documentation format
- **R82:** Link decisions to outcomes (retroactive evaluation)
- **R83:** Multi-agent access (team decision logs)
- **R84:** Temporal queries ("what did we decide when?")
- **R85:** Export for handoff/transitions

**Source:** Workshop Round 3 (Ryan K/Erin: "Product Management / Decision logs")

---

## UC-19: Personal Meta-Management and Life Conditioning

**Actor:** Individual managing mental/emotional states

**Goal:** System adapts to user's current state and provides appropriate support

**Scenario:**

- System detects emotional state (via self-report, biometrics, patterns)
- Surfaces appropriate content ("feeling down? here are mnemegrams that help")
- Proactive suggestions ("you usually feel better after a walk")
- Can condition future self ("what do I want to read when I wake up feeling anxious?")
- Mementos: positive memories surfaced when needed

**Memex Functions Involved:**

- F1 (Inscription - state logging)
- F4.1 (Surfacing - context-aware)
- F5 (Relating - states to interventions)
- F7 (Generation - personalized recommendations)

**Teleological Orientation:**

- T4 (To Orient - self-knowledge)
- T7 (To Reflect)
- T9 (To Commune - with future/past self)

**Requirements Implied:**

- **R86:** Emotional/mental state as first-class data
- **R87:** Context-aware surfacing rules
- **R88:** Pattern matching: state → helpful intervention
- **R89:** Time-based triggers (reminders, scheduled surfacing)
- **R90:** Privacy: deeply personal mental health data

**Source:** Workshop Round 3 (Paul/Jordy: "conditioning, mementos"), Workshop (Subline/Paul^n/Zoravur: "personal meta management")

---

## Updated Status

**Current Status:** Expanded use case collection (19 cases documented)

**Cases Added from Workshop and Existing Use Cases:**

- UC-9: Quantified Self
- UC-10: Relationship Management (CRM)
- UC-11: Social Media Ingestion
- UC-12: AI Assistant
- UC-13: Task Management
- UC-14: Collaborative Knowledge
- UC-15: News Provenance
- UC-16: Location Logging
- UC-17: Algorithmic Reflection
- UC-18: Decision Logs
- UC-19: Life Conditioning

**Requirements Count:** R1-R90 (90 distinct requirements identified)