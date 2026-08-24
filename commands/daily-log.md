---
description: Create today's entry in your linked Notion journal's Daily Logs database, from a session summary JSON
---

Read `~/.claude/notion-journal-config.json` first — it records which Notion database is my "Daily Logs" database and its exact property names. If the file doesn't exist, stop and tell me to run `/link-journal <notion journal page url>` first; don't guess at IDs or property names.

Create a new entry in the **Daily Logs** database.

Set the **Date** title to: the date given below (ask me first if it isn't clearly given — don't guess). If the schema also has a separate sortable date-type property (e.g. "Log Date"), set that too to the matching ISO date so views stay sortable.

Then set the properties using the JSON below. Each JSON key maps 1:1 to a property in the Daily Logs database (match by name, or closest equivalent recorded in the config):
- What I Built Today
- Key Learnings
- Mistakes & Lessons
- Next Steps
- Questions to Answer

If a JSON value is an array, join it into readable prose rather than leaving raw JSON syntax in the property. If a JSON key has no clear matching property in the config, tell me instead of inventing one. Confirm the new page URL back to me when done.

Date and JSON:
$ARGUMENTS
