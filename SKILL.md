---
name: dev-docs-suite
description: Generates professional software development documents fast from minimal input. Use this skill whenever a developer mentions writing, creating, generating, or drafting any of these: Architecture Decision Records (ADR), post-mortems (incident reports, outage reports, retrospectives), API documentation (API contracts, endpoint docs, OpenAPI specs), or onboarding docs (codebase guides, repo walkthroughs, "how this works" docs for new team members). Trigger even if the user just says "write a post-mortem", "document this API", "create an ADR", "help me onboard devs", or describes an incident/outage/API/decision they need documented. Don't wait for the user to ask explicitly — if they're clearly working on any of these doc types, activate immediately.
---

# Dev Docs Suite

A skill for generating the four most time-consuming developer documents — fast, from minimal input, with consistent structure every time.

## Supported Document Types

| What user says | Document type | Reference file |
|---|---|---|
| "write a post-mortem", "incident report", "outage report" | Post-Mortem | `references/post-mortem.md` |
| "create an ADR", "document this decision", "architecture decision" | ADR | `references/adr.md` |
| "document this API", "API contract", "endpoint docs", "OpenAPI" | API Contract Doc | `references/api-contract.md` |
| "onboarding docs", "readme for new devs", "how this codebase works" | Onboarding Doc | `references/onboarding.md` |

## How to Use This Skill

### Step 1 — Identify the document type
From the user's message, determine which of the four document types they need. If ambiguous, ask one clarifying question.

### Step 2 — Read the reference file
Before generating anything, read the relevant reference file from `references/`. It contains the template, required fields, and quality checklist for that document type.

### Step 3 — Gather missing info (minimal questions)
The goal is to ask as few questions as possible. Extract what you can from context. Only ask for what's truly missing — never ask more than 3-4 questions at once.

### Step 4 — Generate the document
Produce the complete document using the template from the reference file. Output it as a well-formatted Markdown document ready to copy-paste or save.

### Step 5 — Offer follow-ups
After generating, offer:
- Export as `.md` file
- Adjust tone (formal vs. casual)
- Fill in any placeholder sections the user skipped

## General Quality Rules (apply to all doc types)

- **Specific over vague**: "Database connection pool exhausted at 847 connections" not "database issues"
- **Action-oriented**: Every section should help the reader do something or understand something
- **Honest**: Post-mortems especially — no blame, but no hiding what happened either
- **Scannable**: Use headers, bullet points, and tables where they add clarity
- **Complete**: Never leave a required section empty — if info is unknown, say "TBD — owner: [name]"

## Triggering by example

If the user says any of these, activate immediately without asking for permission:
- "We had an outage last night, help me write it up"
- "I need to document why we chose PostgreSQL over MongoDB"
- "Write docs for our `/users` endpoint"
- "New engineer joining next week, help me write something to get them up to speed"
