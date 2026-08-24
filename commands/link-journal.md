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
4. For the Daily Logs database specifically, entries must behave like a stack (most recent on top):
   - Look for an existing date-type property meant for sorting (e.g. "Log Date", "Date" if it's a real date type rather than the title). If one exists, note its name.
   - If none exists, add one (`ADD COLUMN "Log Date" DATE`) and backfill it on every existing row by best-effort parsing the row's title into an ISO date — the title field is often free text (e.g. "August 3, 2026 (IMC)") and not reliably sortable as text, so don't skip this.
   - Find the database's primary table view and set its sort to that date property, descending, so newest entries always render on top without manual reordering.
   - Record the `view_id` and the sort property name (as `sort_property`) for Daily Logs.
5. Write this to `~/.claude/notion-journal-config.json` (create the `.claude` folder if it doesn't exist). Overwrite the file if one already exists — re-linking replaces the old link. Shape:
   ```json
   {
     "journal_page_url": "<the page URL I gave you>",
     "daily_log": {
       "data_source_id": "...",
       "title_property": "...",
       "title_date_format": "MMMM D, YYYY",
       "sort_property": "...",
       "view_id": "view://...",
       "properties": { "PropertyName": "type", "...": "..." }
     },
     "concepts_tracker": {
       "data_source_id": "...",
       "title_property": "...",
       "properties": { "PropertyName": "type", "...": "..." }
     }
   }
   ```
6. Confirm back to me what got linked — database names, property lists, and the sort property used for the stack ordering — so I can catch a wrong match before it's used for real writes.

This link is permanent on this device: `/daily-log` and `/extract-concepts` read this file automatically from now on. Re-run `/link-journal <url>` any time to point at a different journal.
