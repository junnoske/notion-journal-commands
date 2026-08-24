# notion-journal-commands

Claude Code custom slash commands for keeping an internship/learning journal in Notion up to date without copy-pasting the same prompts every time.

## Commands

- `/link-journal <notion journal page url>` — run once per device. Resolves your journal's Daily Logs and Concepts Tracker databases and saves them to `~/.claude/notion-journal-config.json`. Re-run any time to point at a different journal.
- `/summarize-session [notes]` — run in your AI coding environment at the end of a session. Produces a human-readable summary plus a Notion-ready JSON block.
- `/daily-log <date + JSON>` — creates a new row in the linked Daily Logs database from that JSON.
- `/extract-concepts <JSON or daily log content>` — extracts reusable concepts/tools/patterns into the linked Concepts Tracker database, updating existing entries instead of duplicating them.

Typical flow: `/link-journal <url>` once → then per session: `/summarize-session` → copy its JSON → `/daily-log <json>` → `/extract-concepts <json>`.

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
