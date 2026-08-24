---
description: Create today's entry in your linked Notion journal's Daily Logs database, from a session summary JSON
---

Read `~/.claude/notion-journal-config.json` first — it records which Notion database is my "Daily Logs" database and its exact property names. If the file doesn't exist, stop and tell me to run `/link-journal <notion journal page url>` first; don't guess at IDs or property names.

Create a new entry in the **Daily Logs** database.

Set the **Date** title to: the date given below (ask me first if it isn't clearly given — don't guess), formatted as the full month name — e.g. "August 20, 2026", never "Aug 20, 2026". If there's more than one entry for the same calendar date, append a short parenthetical to disambiguate (e.g. "August 3, 2026 (IMC)") rather than creating a duplicate-looking title.

Also set `sort_property` from the config (e.g. "Log Date") to the matching ISO date (YYYY-MM-DD) on this entry. Entries in this database behave like a stack — most recent on top — driven entirely by the linked view's descending sort on that property, not by insertion order, so this step is required every time, not optional. If `sort_property`/`view_id` are missing from the config, stop and tell me to re-run `/link-journal` to set up stack ordering before continuing.

Then set the properties using the JSON below. Each JSON key maps 1:1 to a property in the Daily Logs database (match by name, or closest equivalent recorded in the config):
- What I Built Today
- Key Learnings
- Mistakes & Lessons
- Next Steps
- Questions to Answer

If a JSON value is an array, join it into readable prose rather than leaving raw JSON syntax in the property. If a JSON key has no clear matching property in the config, tell me instead of inventing one. Confirm the new page URL back to me when done, along with confirmation that the sort property was set.

Date and JSON:
$ARGUMENTS
