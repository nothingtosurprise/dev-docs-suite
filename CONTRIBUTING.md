# Contributing to dev-docs-suite

Thanks for wanting to contribute! This is a small, focused skill — contributions that stay in scope are most likely to get merged quickly.

## What's in scope

- **New document templates** — RFCs, technical runbooks, changelogs, sprint retrospectives, design docs
- **Improvements to existing templates** — better structure, missing sections, clearer examples
- **Better trigger phrases** — if Claude isn't activating the skill when it should, add phrases to the `description` in `SKILL.md`
- **Quality checklist improvements** — things that should be verified before a doc is considered complete

## What's out of scope

- Changing the skill into something that requires an MCP server (it's intentionally standalone)
- Non-developer document types (this skill is focused on software dev)

## How to contribute

1. Fork the repo
2. Make your changes in the `dev-docs-suite/` folder
3. Test by installing your modified skill in Claude.ai and running a few prompts
4. Open a PR with a brief description of what you changed and why

## Adding a new document type

1. Create `dev-docs-suite/references/your-doc-type.md` with:
   - Minimum info needed (what to ask the user)
   - A complete Markdown template
   - A quality checklist

2. Add a row to the routing table in `dev-docs-suite/SKILL.md`

3. Add trigger phrases to the `description` field in the YAML frontmatter of `SKILL.md`

4. Update `README.md` and `llms.txt` to document the new type

## Template quality bar

Good templates in this skill:
- Are **specific** — example values are realistic, not `"string"` or `"value"`
- Are **complete** — a developer can fill in the blanks without needing to invent structure
- Have **quality checklists** that catch the most common mistakes
- Include **at least one realistic example** per major section

## Questions?

Open an issue and we'll figure it out.
