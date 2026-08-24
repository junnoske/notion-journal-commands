---
description: Extract reusable concepts from today's daily log into your linked Notion journal's Concepts Tracker
---

Read `~/.claude/notion-journal-config.json` first — it records which Notion database is my "Concepts Tracker" database and its exact property names. If the file doesn't exist, stop and tell me to run `/link-journal <notion journal page url>` first; don't guess at IDs or property names.

From the Daily Log JSON below, extract reusable concepts (frameworks, tools, patterns, gotchas) and add them to the **Concepts Tracker** database.

Before creating anything, query the existing entries to check for duplicates — match on the same concept, not just a shared keyword (e.g. "Elasticsearch" and "Elasticsearch index templates" are distinct concepts, don't collapse them).

For each concept:
- Create a new concept if it doesn't exist.
- If it already exists, update **When I Used It** with today's context — append on a new line, never overwrite or delete prior history.

Set these fields:
- Concept/Technology (short title)
- Category (Frontend, Backend, Database, DevOps, Language, Framework, Tool, Other)
- What It Is (1–3 sentence definition)
- When I Used It (today + where it appeared)
- Resources (optional link — only if you're confident it's real; never fabricate one)

Skip generic process/deliverable items (e.g. "wrote a requirements doc") — only extract genuine reusable technical concepts, tools, frameworks, or patterns. Report back a short list of what was created vs. updated.

Daily Log JSON:
$ARGUMENTS
