---
title: Saved searches
description: Save and reuse your filter criteria for Find companies, Find
  people, and Find jobs sources in Clay.
last_synced: 2026-04-26T01:40:36.947Z
---

# Saved searches

Save and reuse your filter criteria for Find companies, Find people, and Find jobs sources in Clay.

Saved searches let you save and reuse your filter criteria for `Find companies`, `Find people`, and `Find jobs` sources in Clay, so you don't have to retype the same search parameters repeatedly.

This feature is especially useful when you're building lists with similar criteria across multiple tables or workbooks, or when you want to quickly recreate a search you've run before.

## Save a search

1.  When creating a `Find companies`, `Find people`, or `Find jobs` source, configure your search filters (industry, headcount, location, job titles, etc.).
2.  Click `Save search` before importing.
3.  Add a name and description for your search to help you remember what the search is for.
4.  Your saved search will now be available to reuse in future tables.

**Note:** For `Find companies` and `Find people` sources, if you navigate away with unsaved filter changes — via browser navigation, switching to a different source type, or switching search modes — Clay will prompt you to save or discard your changes before leaving.

## Use a saved search

1.  When setting up a new `Find companies`, `Find people`, or `Find jobs` source, click `Browse past searches` in the modal.
2.  Click `Saved by you` to find your saved searches (ones you explicitly saved), `Recents` to find your last 5-10 searches, or `Workspace` to find searches saved by anyone.
3.  Select a saved search to load its filter criteria.
4.  Make any adjustments if needed, or use it as-is.
5.  Click `Next` through the remaining setup steps, then click `Save` (the button may read `Save and run N rows`) to add the results to your table. If you're running the search outside an existing table, the save menu offers `Save to new table` (when you're in a workbook) or `Save to new workbook and table` instead.

## FAQs

### What's the difference between saved searches and recent searches?

Recent searches automatically track your last 5-10 searches and are temporary. Saved searches are ones you explicitly save with a name and description for long-term reuse.

### How do I add people from a saved search or my People audience to a Clay table?

Clay Audiences doesn't have an "add to table" or "send to table" action on a People or Companies segment. The segment's **Send** menu offers options such as **Send to workflow** and **Sync to ad platforms**, but none of them copy the segment's records into a Clay table. If you ran a people search, saved it, and then saved the results to **People** in Audiences, use one of the options below to get the same people into a Clay table.

**Option 1 — Import your saved search into a table.** Because the people came from a saved people search, you can pull the same search results directly into a table, including an existing table that already has your enrichment columns set up:

1.  Open the table and add a `Find people` source.
2.  Click `Browse past searches`.
3.  Open `Saved by you` (or `Workspace` for searches your teammates saved) and select your saved search.
4.  Click `Next` through the setup steps, then click `Save` (the button may read `Save and run N rows`) to import the search results into the table.

If you run the search outside an existing table, the save menu offers `Save to new table` (when you're in a workbook) or `Save to new workbook and table` instead.

**Option 2 — Create an enrichment table from the Audiences segment.** This option is only available if your workspace has created a bulk enrichment before.

1.  Open the People segment in Audiences, click `Enrich`, then click the `+` button in the Enrich sidebar.
2.  Select `Create enrichment table` (described as "Legacy bulk enrichment").
3.  Go through the setup steps: **Audience fields** → **Add enrichments** → **Field mapping** → **Review**. Adding enrichment columns is optional. Turn **Field mapping** off if you don't want anything written back to Audiences.

If your workspace has never created a bulk enrichment, the `+` menu shows only `Create enrichment workflow` (marked Beta) and the `Create enrichment table` option isn't available — use Option 1 instead.

**Note:** A Clay table holds up to 50,000 rows, while Audiences holds millions of records. For large or ongoing lists, keep the people in Audiences and use **Send** → **Send to workflow** to run your steps on them — see [Connecting a workflow to a segment](audiences.md#connecting-a-workflow-to-a-segment).

### Who can see my saved searches?

Based on your workspace settings, saved searches can be visible to just you or shared across your workspace. When looking for a saved search, you can filter by ones you created or ones available in your workspace.

### Can I edit a saved search after creating it?

Yes. Load a saved search and modify the filters before importing. If you want to save the modified version, save it as a new search with a different name.

### When should I use saved searches?

Saved searches are ideal when you:

-   Run the same search criteria across multiple tables or workbooks.
-   Work with specific ICPs or segments repeatedly (e.g., "Enterprise SaaS companies in EMEA" or "Marketing directors at Series B startups").
-   Want to maintain consistency in how your team builds lists.
-   Need to quickly recreate a complex search with many filters.

### Best practices

**Use descriptive names:** Instead of "Search 1" or "Test," use names like "Enterprise fintech companies UK" or "CMOs at Series A-B startups" so you and your team can quickly identify the right search.

**Add context in descriptions:** Include notes about why this search exists or what it's used for, especially if sharing with your team.

**Start with templates:** For searches your team uses frequently, save them as go-to templates that everyone can access and modify as needed.

**Combine with functions:** Save your enrichment workflow as a [function](functions.md) alongside your saved search criteria for even faster setup — recreate the search, then call the function to run your standard enrichments.
