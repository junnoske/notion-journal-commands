---
description: Link the journal commands to a specific Notion journal (run once per device — persists after that)
---

Resolve and save the Notion database IDs that `/daily-log` and `/extract-concepts` should target, so they don't need to be specified again on this device.

Input: $ARGUMENTS should be the URL of your journal's Notion page — the page containing your daily-log-style database and your concepts/technology-tracker-style database. If empty, ask me for it before doing anything else.

Steps:
1. Fetch the given page with the Notion fetch tool.
2. Find the child databases on that page. If it's unclear which one is the "daily log" style database (dated entries with free-text fields like what-I-built / learnings / mistakes / next-steps) versus the "concepts tracker" style database (a title field plus a category/select and a short-definition field), ask me to confirm which is which — don't guess.
3. For each of the two databases, fetch its data source schema and record:
   - `data_source_id`
   - the title property name
   - every other property name and its type
4. Write this to `~/.claude/notion-journal-config.json` (create the `.claude` folder if it doesn't exist). Overwrite the file if one already exists — re-linking replaces the old link. Shape:
   ```json
   {
     "journal_page_url": "<the page URL I gave you>",
     "daily_log": {
       "data_source_id": "...",
       "title_property": "...",
       "properties": { "PropertyName": "type", "...": "..." }
     },
     "concepts_tracker": {
       "data_source_id": "...",
       "title_property": "...",
       "properties": { "PropertyName": "type", "...": "..." }
     }
   }
   ```
5. Confirm back to me what got linked — database names plus their property lists — so I can catch a wrong match before it's used for real writes.

This link is permanent on this device: `/daily-log` and `/extract-concepts` read this file automatically from now on. Re-run `/link-journal <url>` any time to point at a different journal.
