# Onboarding Documentation Reference

## What is an Onboarding Doc?
A guide that helps a new developer get productive in a codebase as fast as possible. The best onboarding docs answer the questions a new dev would ask in their first week — without them having to interrupt senior engineers.

## Minimum Info Needed
Ask the user for:
1. What is this project/repo? (1-2 sentences)
2. What tech stack does it use?
3. How do you run it locally?
4. What are the most important things to understand about the codebase?

Optional but very useful:
- Common gotchas / things that trip people up
- Who owns what (team structure)
- Links to related systems or dependencies

---

## Template

```markdown
# [Project Name] — Developer Onboarding Guide

**Last Updated:** [YYYY-MM-DD]  
**Maintained by:** [Team or person]  
**Repo:** [link]  
**Slack / Discord:** [channel]

> **TL;DR:** [One sentence: what is this service, what does it do, who uses it.]

---

## What Is This?

[2-4 sentences. What problem does this service/project solve? Who are its users (internal team, external customers, other services)? What would break if this went down?]

---

## Architecture Overview

[Brief description of the system's main components and how they interact. A diagram is ideal — describe one if you can't embed one.]

```
[Browser] → [API Gateway] → [This Service] → [Database]
                                          → [External API]
```

**Key components:**
- `src/api/` — Express route handlers
- `src/services/` — Business logic
- `src/db/` — Database models and migrations
- `src/workers/` — Background job processors

---

## Tech Stack

| Layer | Technology | Notes |
|---|---|---|
| Language | [e.g. TypeScript] | [e.g. v5.x, strict mode] |
| Framework | [e.g. Express] | [version] |
| Database | [e.g. PostgreSQL] | [version, hosted where] |
| Cache | [e.g. Redis] | [if applicable] |
| Queue | [e.g. BullMQ] | [if applicable] |
| Hosting | [e.g. AWS ECS] | |
| CI/CD | [e.g. GitHub Actions] | |

---

## Getting Started

### Prerequisites

- [ ] [Tool] v[X.X] or higher — [install link]
- [ ] [Tool] — [install link]
- [ ] Access to [system] — request via [link/person]

### Setup

```bash
# Clone
git clone [repo-url]
cd [project-name]

# Install dependencies
[e.g. npm install]

# Copy env file and fill in values
cp .env.example .env
# See "Environment Variables" section below

# Set up the database
[e.g. npm run db:migrate]

# Start the dev server
[e.g. npm run dev]
```

The app should now be running at `http://localhost:[PORT]`.

### Environment Variables

| Variable | Required | Description | Where to get it |
|---|---|---|---|
| `DATABASE_URL` | Yes | PostgreSQL connection string | Local: see `.env.example` |
| `API_KEY` | Yes | Auth for [external service] | 1Password → "[vault name]" |
| `PORT` | No | Server port (default: 3000) | — |

---

## Common Tasks

### Running Tests

```bash
npm test              # All tests
npm run test:unit     # Unit tests only
npm run test:e2e      # End-to-end tests (needs DB running)
```

Tests use [Jest / Vitest / etc.]. Coverage report: `npm run coverage`.

### Database Migrations

```bash
npm run db:migrate         # Run pending migrations
npm run db:migrate:undo    # Roll back last migration
npm run db:seed            # Seed development data
```

Migrations live in `db/migrations/`. Never edit a migration after it's merged.

### Adding a New API Endpoint

1. Add route in `src/api/routes/[resource].ts`
2. Add handler in `src/api/handlers/[resource].ts`
3. Add business logic in `src/services/[resource].ts`
4. Add tests in `tests/[resource].test.ts`
5. Update API docs in `docs/api.md`

---

## Codebase Conventions

- **Naming:** [e.g. camelCase for vars, PascalCase for classes, kebab-case for files]
- **Error handling:** [e.g. all errors extend `AppError`, use `Result` type pattern]
- **Logging:** [e.g. use `logger.info()` not `console.log`, structured JSON logs]
- **PR process:** [e.g. 1 approval required, squash merge, conventional commits]

---

## Common Gotchas

> Things that trip up new engineers. Add to this list!

- **[Gotcha title]:** [What it is and how to handle it]
- **[Gotcha title]:** [What it is and how to handle it]
- **Local vs. staging env vars:** The `.env.example` uses localhost URLs. Staging uses internal service URLs — don't copy staging env to local.

---

## Key Concepts to Understand

[Explain 2-4 domain or architectural concepts that are non-obvious and critical to understand. Things a new dev won't get from just reading the code.]

### [Concept 1]
[Explanation]

### [Concept 2]
[Explanation]

---

## Who Owns What

| Area | Owner | Contact |
|---|---|---|
| Auth & permissions | [Name/Team] | [Slack handle] |
| Database / data model | [Name/Team] | [Slack handle] |
| Infra & deployments | [Name/Team] | [Slack handle] |
| This service overall | [Name/Team] | [Slack handle] |

---

## Useful Links

- [Production dashboard](#)
- [Staging environment](#)
- [Error tracking (Sentry)](#)
- [CI/CD pipelines](#)
- [Architecture diagram](#)
- [Product spec / PRD](#)
- [API docs](#)

---

## Onboarding Checklist

For the new engineer to track their own progress:

- [ ] Repo cloned and running locally
- [ ] Can run and pass all tests
- [ ] Read this doc and the architecture overview
- [ ] Met with [person] for codebase walkthrough
- [ ] Merged first (small) PR
- [ ] Added to [Slack channel, PagerDuty rotation, etc.]
```

---

## Quality Checklist

Before finishing, verify:
- [ ] New dev can go from zero to running app using only this doc
- [ ] Every prerequisite listed with install link or instructions
- [ ] Env vars documented with where to get secret values
- [ ] At least 3 common gotchas listed (or note that none are known yet)
- [ ] Clear ownership info — who do they ask when stuck?
- [ ] "Useful links" section has real links (or [TBD] placeholders)
- [ ] Onboarding checklist is specific to this project, not generic
