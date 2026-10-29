---
description: End-of-session journal in one go - summarize this session, then (after my OK) file it in Daily Logs and the Concepts Tracker
---

Run my whole journal flow for this session: `/summarize-session`, then `/daily-log`, then `/extract-concepts`, without me copying JSON between them.

1. **Check the link.** Read `~/.claude/notion-journal-config.json`. If it doesn't exist, stop and tell me to run `/link-journal <notion journal page url>` first.
2. **Summarize.** Follow the `/summarize-session` instructions (its command file, `summarize-session.md` in this project's `.claude/commands/` if there is one, otherwise in `~/.claude/commands/`): Part A + Part B JSON. Use my notes below if there are any; otherwise summarize this conversation.
3. **Date.** Use the date in my notes if there is one; otherwise today's date. Say which date you're using.
4. **Show and wait.** Show me Part A, the JSON, the date and the list of concepts you plan to extract (marked new or update-existing after querying the Concepts Tracker). Then stop and ask me to confirm or correct. Nothing goes to Notion before I say yes.
5. **File it.** Once I confirm, create the Daily Logs entry following the `/daily-log` instructions, then the concepts following the `/extract-concepts` instructions (same lookup for their command files), using the confirmed JSON and date.
6. **Report.** Give me the Daily Logs page URL, confirm the sort property was set, and list the concepts created and updated.

My notes (optional; may include a date):
$ARGUMENTS
