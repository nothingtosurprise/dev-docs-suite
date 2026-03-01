# Architecture Decision Record (ADR) Reference

## What is an ADR?
A short document that captures an important architectural decision: what was decided, why, and what alternatives were considered. ADRs are written once and rarely updated — if a decision changes, a new ADR is written superseding the old one.

## Minimum Info Needed
Ask the user for:
1. What decision was made? (e.g. "use PostgreSQL instead of MongoDB")
2. What problem were you solving?
3. What alternatives did you consider?
4. Why did you choose this option?

Optional but useful:
- Who was involved in the decision?
- Are there known downsides or trade-offs?

---

## Numbering Convention
ADRs are typically numbered sequentially: ADR-001, ADR-002, etc. Ask the user what number this is, or default to ADR-XXX.

---

## Template

```markdown
# ADR-[NUMBER]: [Short Title of Decision]

**Date:** [YYYY-MM-DD]  
**Status:** [Proposed / Accepted / Deprecated / Superseded by ADR-XXX]  
**Deciders:** [Names or team]  
**Technical Area:** [e.g. Database, Auth, Infrastructure, API Design]

---

## Context

[What is the problem or situation that forced this decision? What constraints exist? What is the current state of the system? Write this as if explaining to someone who wasn't in the room — 2-4 sentences.]

> Example: "We need to persist user-generated content with complex nested relationships. Our current in-memory store doesn't survive restarts, and we're growing to a point where we need a real database. The team has experience with both relational and document databases."

---

## Decision

**We will [action] because [primary reason].**

[1-3 sentences expanding on the decision. Be direct — this is the most important sentence in the document.]

> Example: "We will use PostgreSQL as our primary database because it best supports our relational data model, the team has strong existing expertise, and it scales to our projected 5-year load without architectural changes."

---

## Alternatives Considered

### Option 1: [Name of option chosen — mark as CHOSEN]
**Pros:**
- [Pro]
- [Pro]

**Cons:**
- [Con]
- [Con]

**Verdict:** ✅ Chosen

---

### Option 2: [Name of alternative]
**Pros:**
- [Pro]

**Cons:**
- [Con]
- [Con]

**Verdict:** ❌ Rejected — [one sentence why]

---

### Option 3: [Name of alternative, if applicable]
**Pros:**
- [Pro]

**Cons:**
- [Con]

**Verdict:** ❌ Rejected — [one sentence why]

---

## Consequences

### Positive
- [What gets better as a result of this decision]
- [What gets better]

### Negative / Trade-offs
- [What gets worse or becomes harder]
- [Known limitation or risk accepted]

### Neutral
- [Things that change but aren't clearly better or worse]

---

## Implementation Notes

[Optional. Any specific guidance on how to implement this decision, or links to relevant docs/tickets.]

---

## References

- [Link to relevant RFC, ticket, PR, or doc]
- [Link to relevant RFC, ticket, PR, or doc]
```

---

## Quality Checklist

Before finishing, verify:
- [ ] Decision statement is a single clear sentence starting with "We will..."
- [ ] At least 2 alternatives were considered (even if one was "do nothing")
- [ ] Pros/cons are specific, not generic
- [ ] At least one negative consequence is listed (no decision is cost-free)
- [ ] Status is set correctly
- [ ] Context explains the *problem*, not just the solution
