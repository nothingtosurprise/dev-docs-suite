# 🛠️ dev-docs-suite — Claude Skill

> Generate professional developer documents in seconds. No more staring at a blank page.

A [Claude Skill](https://www.anthropic.com/news/introducing-agent-skills) that handles the four most time-consuming documents in software development — from minimal input, with consistent structure every time.

---

## What it does

| Just say... | You get... |
|---|---|
| "Write a post-mortem for last night's outage" | Full incident report with timeline, root cause, action items |
| "Create an ADR for switching to PostgreSQL" | Architecture Decision Record with alternatives compared |
| "Document our `/users` API endpoint" | Complete API contract with request/response examples, error codes |
| "Write onboarding docs for the new engineer joining Monday" | Full developer onboarding guide with setup steps and gotchas |

Claude reads the context, picks the right doc type, asks minimal follow-up questions, and produces a complete, copy-paste-ready Markdown document.

---

## Install as a Claude Skill

### Option 1 — Upload directly (Claude.ai)

1. Download [`dev-docs-suite.zip`](https://github.com/yourusername/dev-docs-suite/releases/latest)
2. Go to **Claude.ai → Settings → Capabilities → Skills**
3. Click **Upload skill** and select the zip

### Option 2 — Connect via MCP (Claude Code / any MCP client)

Use [gitMCP.io](https://gitmcp.io) to turn this repo into a live MCP server instantly:

```json
{
  "mcpServers": {
    "dev-docs-suite": {
      "url": "https://gitmcp.io/yourusername/dev-docs-suite"
    }
  }
}
```

No server to run. No API key. Just point and connect.

---

## Repo structure

```
dev-docs-suite/          ← The actual skill folder (upload this)
├── SKILL.md             ← Skill instructions + trigger logic
└── references/
    ├── post-mortem.md   ← Incident report template
    ├── adr.md           ← Architecture Decision Record template
    ├── api-contract.md  ← API documentation template
    └── onboarding.md    ← Developer onboarding guide template
README.md                ← You're here (not part of the skill)
llms.txt                 ← AI-readable summary for MCP/gitMCP
```

---

## Supported document types

### 📋 Post-Mortem / Incident Report
Structured incident report with impact metrics, full timeline, root cause analysis, contributing factors, and action items with owners and due dates. Blameless by design.

### 🏛️ Architecture Decision Record (ADR)
Captures what was decided, why, and what alternatives were rejected. Follows the standard ADR format. Numbered and statusable (Proposed / Accepted / Deprecated / Superseded).

### 📡 API Contract Documentation
Full endpoint documentation with path/query/body parameters, request/response examples, error codes, and a changelog. Structured for developer consumption.

### 🚀 Developer Onboarding Guide
Everything a new engineer needs to go from zero to productive: prerequisites, setup steps, env var table, common tasks, codebase conventions, gotchas, ownership map, and a personal onboarding checklist.

---

## Example usage

```
You: We had a database outage yesterday from 2pm to 3pm. The connection pool hit its limit
     after a bad deploy. About 2,000 users were affected. Write a post-mortem.

Claude: [reads references/post-mortem.md, asks 2 follow-up questions, produces full report]
```

```
You: Document our POST /orders endpoint. It takes a user_id, items array, and shipping_address.
     Returns an order object. Can fail with 400, 401, 404, 429.

Claude: [reads references/api-contract.md, generates complete API doc with examples]
```

---

## Contributing

PRs welcome! Especially:
- New document type templates (RFCs, changelogs, runbooks)
- Improvements to existing templates
- Additional trigger phrases in `SKILL.md`

See [CONTRIBUTING.md](./CONTRIBUTING.md) for guidelines.

---

## License

MIT — free to use, modify, and distribute.
