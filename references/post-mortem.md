# Post-Mortem Reference

## Minimum Info Needed
Ask the user for these if not provided:
1. What happened? (1-2 sentences)
2. When did it start and end?
3. What was the user/business impact?
4. What caused it?
5. What fixed it?

Everything else can be inferred or left as TBD.

---

## Template

```markdown
# Incident Post-Mortem: [Short Title]

**Date:** [YYYY-MM-DD]  
**Duration:** [e.g. 47 minutes — 14:03 to 14:50 UTC]  
**Severity:** [P0 / P1 / P2 / P3]  
**Status:** [Draft / Review / Final]  
**Authors:** [Names]  
**Reviewers:** [Names]

---

## Summary

[2-3 sentences. What broke, how long, who was affected, how it was fixed. Written for someone who wasn't in the room.]

> Example: "On [date], a misconfigured database connection pool caused 100% of API requests to fail for 47 minutes, affecting all [X] production users. The issue was resolved by reverting a deployment and increasing the connection pool limit."

---

## Impact

| Metric | Value |
|---|---|
| Duration | X minutes |
| Users affected | X (or X%) |
| Requests failed | X |
| Revenue impact | $X (if known) |
| SLA breach? | Yes / No |

[Add any qualitative impact: customer complaints, support tickets, trust damage]

---

## Timeline

All times in UTC.

| Time | Event |
|---|---|
| HH:MM | [First sign of trouble — alert, customer report, etc.] |
| HH:MM | [Investigation started] |
| HH:MM | [Root cause identified] |
| HH:MM | [Mitigation applied] |
| HH:MM | [Service restored] |
| HH:MM | [Incident declared resolved] |

---

## Root Cause

[One clear paragraph explaining the technical root cause. Be specific. Avoid "human error" as a root cause — go one level deeper.]

> Example: "A deployment at 13:55 UTC changed the database connection pool max from 100 to 10 via an untested environment variable. Under production load, the pool exhausted within 8 minutes, causing all new connection attempts to throw `ConnectionPoolTimeoutError`."

---

## Contributing Factors

[What made this possible or worse? These are systemic issues, not blame.]

- No staging environment load test before deploy
- Alert threshold for connection errors was set to 500ms delay — missed pool exhaustion
- On-call runbook didn't include connection pool debugging steps

---

## Resolution

[What was done to stop the bleeding? Step by step.]

1. [Action taken]
2. [Action taken]
3. Service restored at HH:MM UTC

---

## Action Items

| Action | Owner | Due Date | Priority |
|---|---|---|---|
| Add connection pool monitoring alert | [Name] | [Date] | High |
| Add load test to staging CI pipeline | [Name] | [Date] | Medium |
| Update runbook with pool debugging steps | [Name] | [Date] | Low |

---

## What Went Well

- [Thing that worked during the incident]
- [Thing that worked during the incident]

---

## What Didn't Go Well

- [Thing that slowed us down or made it worse]
- [Thing that slowed us down or made it worse]

---

## Lessons Learned

[1-3 key takeaways. What does the team now know that it didn't before?]
```

---

## Quality Checklist

Before finishing, verify:
- [ ] Timeline is complete with no gaps > 15 min unexplained
- [ ] Root cause is specific (not "human error" or "misconfiguration")
- [ ] Every action item has an owner and due date
- [ ] No blame language toward individuals
- [ ] Impact section has at least 2 quantitative metrics
- [ ] "What went well" section is genuine, not forced
