# notion-journal-commands

Claude Code custom slash commands for the HTX AI/ML Lab Intern Journal in Notion.

## Commands

- `/summarize-session [notes]` — run in your AI coding environment at the end of a session. Produces a human-readable summary plus a Notion-ready JSON block.
- `/daily-log <date + JSON>` — creates a new row in the **Daily Logs** database from that JSON.
- `/extract-concepts <JSON or daily log content>` — extracts reusable concepts/tools/patterns into the **Concepts Tracker** database, updating existing entries instead of duplicating them.

Typical flow: `/summarize-session` → copy its JSON → `/daily-log <json>` → `/extract-concepts <json>`.

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
