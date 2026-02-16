---
title: Access Control Models
domain: engineering architecture
status: analysis-driven
note: Addresses GAP-3 (Contextual Access Control), supports P8 (Protection), P10 (Contextual Access)
related:
  - "[[core/principles]]"
  - "[[analysis/gap-analysis]]"
  - "[[analysis/glossary-engineering]]"
tags:
  - ai-slop
author:
  - Sonnet 4.5
---

# Access Control Models for Personal Data

This document surveys access control architectures relevant to personal data operations. GAP-3 (Contextual Access Control) was identified as a critical weakness across all evaluated systems except Solid and Notion (which has vendor lock-in).

---

## The Access Control Problem in Personal Data

**Core Challenge:** Personal knowledge exists in multiple contexts simultaneously. A mnemegram might be:

- Work-related (shareable with colleagues)
- Personal (private)
- Both (work email with personal reflection)

**Requirements Implicated:**

- R5: Fine-grained access control (not all-or-nothing)
- R6: Mnemegram-level access control (not just collection-level)
- R7: Multi-context mnemegrams (same item, different audiences)
- R32: Context-based partitioning
- R52: Fine-grained AI access permissions

**Principles:**

- P8 (Protection by Default): Security must be foundational
- P10 (Contextual Access): Permissions adapt to context

---

## Access Control List (ACL) Model

**Description:** Each object has a list specifying who can access it and what they can do.

**Structure:**

```
Mnemegram X:
  - User A: read, write
  - User B: read
  - Group C: read
```

**Principle Alignment:**

- Supports P8 (Protection) - explicit permissions
- Partially supports P10 (Contextual Access) - can encode context rules but static
- Weakens P1 (Agent Sovereignty) - requires centralized ACL server

**Requirements Addressed:**

- R5 (Fine-grained access) - yes, per-object
- R6 (Mnemegram-level) - yes
- R9 (Auditable) - server can log access

**Requirements Not Addressed:**

- R7 (Multi-context) - difficult to express "work context" vs "personal context"
- R25 (Delegatable) - not designed for delegation
- R26 (Dead man's switch) - requires special implementation

**Strengths:**

- Well-understood, mature pattern
- Rich tooling and libraries
- Easy to reason about
- Audit logs straightforward

**Weaknesses:**

- Centralized (need ACL server)
- Not easily delegatable
- Context must be explicitly modeled
- Performance overhead on every access check

**Implementations:**

- File systems (POSIX ACLs)
- Databases (PostgreSQL row-level security)
- Cloud storage (AWS IAM, Google Cloud IAM)

**Use for Personal Data Ops:**
Appropriate when:

- Centralized server acceptable
- Access patterns are relatively static
- Audit requirements are strict

---

## Capability-Based Security

**Description:** Access rights are unforgeable tokens (capabilities) that can be passed between entities. Possession of capability = permission to access.

**Structure:**

```
Token: {
  resource: "mnemegram:abc123",
  permissions: ["read"],
  expires: "2026-03-01",
  signature: "..."
}
```

**Principle Alignment:**

- Strongly supports P1 (Agent Sovereignty) - no central server required
- Strongly supports P10 (Contextual Access) - tokens can encode any context
- Supports P8 (Protection) - cryptographically enforced

**Requirements Addressed:**

- R5, R6 (Fine-grained, mnemegram-level) - yes
- R7 (Multi-context) - tokens can specify context
- R25 (Capability-based delegation) - designed for this
- R26 (Dead man's switch) - can encode conditional access
- R54 (Revoke AI access) - revoke tokens

**Gap Addressed:**

- GAP-3 (Contextual Access Control) - capability model is strongest solution

**Strengths:**

- Decentralized - no ACL server needed
- Naturally delegatable (pass token)
- Fine-grained and flexible
- Temporal access (tokens can expire)
- Conditional access (tokens can have preconditions)

**Weaknesses:**

- UX challenge (users managing tokens)
- Revocation complex (need revocation lists or short-lived tokens)
- Audit trail requires additional infrastructure
- Less familiar to developers

**Implementations:**

- UCAN (User Controlled Authorization Networks) - Web3-style
- Macaroons - Google's capability system
- Object capability languages (E, Pony)

**Example UCAN:**

```json
{
  "iss": "did:key:zAlice...",
  "aud": "did:key:zBob...",
  "att": [
    {
      "with": "storage://alice/mnemegrams/work/*",
      "can": "read"
    }
  ],
  "exp": 1735689600,
  "prf": ["parent-ucan-cid"]
}
```

**Use for Personal Data Ops:**
Appropriate when:

- Decentralization is priority (P1)
- Delegation is common (share with AI, family, colleagues)
- Agent wants control without server
- Context-aware access is critical (P10)

**Challenge:** Need good UX for token management. Most users shouldn't see tokens directly.

---

## Attribute-Based Access Control (ABAC)

**Description:** Access decisions based on attributes of subject (who), resource (what), and context (when/where/how), evaluated via policy.

**Structure:**

```
Policy: GRANT read IF
  subject.role = "colleague" AND
  resource.context = "work" AND
  time.hour BETWEEN 9 AND 17
```

**Principle Alignment:**

- Strongly supports P10 (Contextual Access) - policies express context naturally
- Supports P8 (Protection) - explicit policy evaluation
- Requires infrastructure (policy evaluation engine)

**Requirements Addressed:**

- R7 (Multi-context mnemegrams) - policies can check context attribute
- R32 (Context-based partitioning) - "IF context=work THEN..."
- R33 (Context assertions) - context is attribute on resource
- R42 (Temporal decay) - policies can check time-based attributes

**Strengths:**

- Very expressive (can encode complex rules)
- Context-native (designed for contextual decisions)
- Policies separate from code
- Can reason about access patterns

**Weaknesses:**

- Requires policy evaluation engine
- Performance overhead (evaluate policy on each access)
- Policy language complexity
- Debugging policies can be hard

**Implementations:**

- XACML (eXtensible Access Control Markup Language)
- Open Policy Agent (OPA)
- AWS IAM policy language (attribute-based)

**Example OPA Policy (Rego):**

```rego
allow {
  input.subject.role == "family"
  input.resource.context == "personal"
  input.resource.sensitivity != "private"
}
```

**Use for Personal Data Ops:**
Appropriate when:

- Access rules are complex and contextual
- Context is explicitly modeled (work/personal/family)
- Willing to run policy evaluation engine
- Need to audit/explain access decisions

---

## Web Access Control (WAC) - Solid's Approach

**Description:** RDF-based ACL system where permissions are themselves RDF triples. Per-resource ACLs in linked documents.

**Structure (Turtle):**

```turtle
@prefix acl: <http://www.w3.org/ns/auth/acl#> .

<#authorization1>
  a acl:Authorization;
  acl:agent <https://alice.example/profile#me>;
  acl:accessTo <mnemegram123>;
  acl:mode acl:Read, acl:Write.
```

**Principle Alignment:**

- Strongly supports P3 (Semantic Richness) - ACLs are semantic data
- Strongly supports P10 (Contextual Access) - very expressive
- Supports P8 (Protection) - fine-grained
- Weakens P9 (Performance) - RDF query overhead

**Requirements Addressed:**

- R5, R6 (Fine-grained, per-resource) - yes
- R9 (Auditable) - ACLs are inspectable RDF

**Requirements Challenged:**

- R9 (Performance) - SPARQL queries for permission checks are slow

**Strengths:**

- Maximally expressive (RDF can represent anything)
- Permissions are data (can query, reason about)
- Integrates with Solid's RDF architecture
- Permissions inherit (folder to contained resources)

**Weaknesses:**

- Complex (requires understanding RDF)
- Performance poor (SPARQL on every access check)
- Over-engineered for many use cases
- Steep learning curve

**System Score:**
Solid scores 2/2 on P10 (Contextual Access) - only system besides Notion. But overall 19/30 due to complexity and performance.

**Use for Personal Data Ops:**
Appropriate when:

- Already using RDF/Solid
- Need maximum expressiveness
- Performance is acceptable tradeoff
- Semantic reasoning over permissions is valuable

---

## Role-Based Access Control (RBAC)

**Description:** Users assigned to roles, roles have permissions. Simpler than ABAC, more structured than ACLs.

**Structure:**

```
Roles:
  - family: read personal mnemegrams
  - colleague: read work mnemegrams
  - self: read/write all

User Bob: [colleague]
User Alice: [family, colleague]
```

**Principle Alignment:**

- Partially supports P8 (Protection) - explicit roles
- Weakly supports P10 (Contextual Access) - roles are coarse-grained
- Simplified management vs ACLs

**Requirements Addressed:**

- R21 (Family as access unit) - family can be a role
- R18 (Multi-agent with roles) - natural fit

**Strengths:**

- Simpler than ABAC or capabilities
- Familiar to administrators
- Scales to organizations
- Clear mental model

**Weaknesses:**

- Coarse-grained (role explosion problem)
- Difficult to express context beyond role
- Not naturally delegatable
- Static (role changes require admin)

**Use for Personal Data Ops:**
Limited applicability. Appropriate only for:

- Family/team memex with clear roles
- When context maps cleanly to roles
- Simplicity valued over flexibility

---

## Comparative Analysis

**Expressiveness Spectrum:**

```
RBAC < ACL < ABAC ≈ WAC < Capabilities
(simple)                      (flexible)
```

**Decentralization Spectrum:**

```
ACL/RBAC < ABAC/WAC < Capabilities
(centralized)       (decentralized)
```

**Performance Spectrum:**

```
RBAC > ACL > Capabilities > ABAC > WAC
(fast)                              (slow)
```

**Contextual Access Support:**

```
RBAC < ACL < Capabilities < ABAC ≈ WAC
(weak)                           (strong)
```

---

## Recommendations by Use Case

**For Individual Local-First Memex (Obsidian-like):**

- **No access control needed** - all data is agent's
- If sharing: Simple ACLs or capability tokens

**For Personal Data Server with Selective Sharing:**

- **Capabilities (UCAN)** - Decentralized, delegatable, contextual
- Alternative: ABAC if context rules are complex

**For Family/Team Collaborative Memex:**

- **RBAC + ACLs** - Simple role structure with per-item overrides
- Alternative: ABAC if contexts are fluid

**For Research/Academic Collaboration:**

- **ABAC** - Complex rules (embargo dates, institutional affiliation)
- Alternative: WAC if already using RDF

**For AI Agent Access:**

- **Capabilities** - Delegatable tokens with scope and expiration
- Alternative: ABAC with agent attributes

---

## Hybrid Approaches

Real systems often combine models:

**Capability + ACL:**

- Issue capability tokens for external sharing
- Use ACLs for known internal entities
- Example: Personal notes (no AC) + shared collections (capabilities)

**RBAC + ABAC:**

- Roles for common patterns
- Policies for complex cases
- Example: "Family" role + policy for "no late-night access"

**Capability + Context:**

- Capabilities reference context
- Access granted only in matching context
- Example: Token valid only when "location=home"

---

## Implementation Considerations

**Performance:**

- ACL/RBAC: O(1) with proper indexing
- Capabilities: O(1) token validation
- ABAC/WAC: O(n) policy evaluation, depends on complexity

**Audit:**

- ACL: Centralized server logs all checks
- Capabilities: Requires separate audit log infrastructure
- ABAC: Policy evaluation logs show reasoning

**Revocation:**

- ACL/RBAC: Immediate (update list)
- Capabilities: Hard (need revocation lists or short TTL)
- ABAC: Immediate (update policy)

**Usability:**

- RBAC: Easy (assign roles)
- ACL: Moderate (manage per-resource lists)
- Capabilities: Hard (manage tokens)
- ABAC/WAC: Very hard (write policies)

---

## Open Questions

1. Can capabilities have acceptable UX for non-technical users?
2. How do you express "work context" without explicit tagging?
3. Can AI help with automatic context inference for access control?
4. What's the right granularity - mnemegram-level, assertion-level, field-level?
5. How do you handle "this is private now but becomes public after my death"?
6. Can hybrid approaches (capabilities for external, ACL for internal) work seamlessly?

---

## Cross-References

- [[core/principles]] - P8 (Protection), P10 (Contextual Access)
- [[analysis/gap-analysis]] - GAP-3 (Contextual Access Control)
- [[analysis/system-evaluation]] - How systems score on access control
- [[analysis/glossary-engineering]] - Technical term definitions
- [[context/cases/solid-analysis]] - WAC in practice (to be created)
