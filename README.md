# notion-journal-commands

Claude Code custom slash commands for keeping an internship/learning journal in Notion up to date without copy-pasting the same prompts every time.

**Why this exists:** the source template is designed around a Notion AI Agent, which requires a paid Notion plan. If you don't have Notion premium, these commands get you the same workflow — summarizing a coding session and filing it into your Daily Logs / Concepts Tracker databases — using Claude Code's [Notion MCP integration](https://developers.notion.com/guides/mcp/get-started-with-mcp) instead, which only needs a free Notion account.

## Commands

- `/link-journal <notion journal page url>` — run once per device. Resolves your journal's Daily Logs and Concepts Tracker databases and saves them to `~/.claude/notion-journal-config.json`. Re-run any time to point at a different journal.
- `/summarize-session [notes]` — run in your AI coding environment at the end of a session. Produces a human-readable summary plus a Notion-ready JSON block.
- `/daily-log <date + JSON>` — creates a new row in the linked Daily Logs database from that JSON.
- `/extract-concepts <JSON or daily log content>` — extracts reusable concepts/tools/patterns into the linked Concepts Tracker database, updating existing entries instead of duplicating them.
- `/log-session [notes]` — the whole per-session flow in one command: summarizes the session, shows you the summary, JSON, date and planned concepts, and only after you confirm creates the Daily Logs entry and the concepts.

Typical flow: `/link-journal <url>` once → then per session: `/log-session`. Or step by step: `/summarize-session` → copy its JSON → `/daily-log <json>` → `/extract-concepts <json>`.

Project-specific versions of these commands can live in a project's `.claude/commands/`; `/log-session` uses a project's `summarize-session.md` (and the others) when one exists there, otherwise the ones in `~/.claude/commands/`.

## How the link persists

`/link-journal` writes the resolved database IDs and property schemas to `~/.claude/notion-journal-config.json`. `/daily-log` and `/extract-concepts` read that file automatically, so once you've linked a journal on a device you don't need to repeat the URL or IDs again. The config file is local (not tracked in this repo) — run `/link-journal` again on each new device, or copy `notion-journal-config.json` over manually since the underlying IDs don't change per device.

## Install

Claude Code loads commands from `~/.claude/commands/`. Clone this repo anywhere, then copy or symlink its `commands/` files into place:

**Windows (PowerShell):**
```powershell
Copy-Item .\commands\*.md "$env:USERPROFILE\.claude\commands\" -Force
```

**Mac/Linux:**
```bash
cp commands/*.md ~/.claude/commands/
# or, to keep them auto-updating on `git pull`:
ln -s "$(pwd)"/commands/*.md ~/.claude/commands/
```

After editing a command here, re-copy (or `git pull` if symlinked) on each device to pick up the change.

## Reference

These commands are built around [zero2sudo's SWE Intern Learning Journal](https://www.notion.com/templates/swe-intern-learning-journal-by-zero2sudo) Notion template (Daily Logs + Concepts Tracker structure). `/link-journal` works with any Notion journal that follows a similar shape, not just this exact template.
