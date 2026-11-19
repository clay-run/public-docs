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

By default, Clay Audiences doesn't have an "add to table" or "send to table" action on a People or Companies segment. The segment's **Send** menu offers options such as **Send to workflow** and **Sync to ad platforms**, but none of them copy the segment's records into a Clay table. Sending a segment to a table with **Add to workbook** is turned off by default and is enabled for individual workspaces on request — contact support to ask about enabling it for your workspace. If you ran a people search, saved it, and then saved the results to **People** in Audiences, import the saved search into a Clay table.

**Import your saved search into a table.** Because the people came from a saved people search, you can pull the same search results directly into a table, including an existing table that already has your enrichment columns set up:

1.  Open the table and add a `Find people` source.
2.  Click `Browse past searches`.
3.  Open `Saved by you` (or `Workspace` for searches your teammates saved) and select your saved search.
4.  Click `Next` through the setup steps, then click `Save` (the button may read `Save and run N rows`) to import the search results into the table.

If you run the search outside an existing table, the save menu offers `Save to new table` (when you're in a workbook) or `Save to new workbook and table` instead.

**Note:** A Clay table holds up to 50,000 rows, while Audiences holds millions of records. For large or ongoing lists, keep the people in Audiences and use **Send** → **Send to workflow** to run your steps on them — see [Connecting a workflow to a segment](audiences.md#connecting-a-workflow-to-a-segment).

### Why didn't the rows I deleted from a segment-connected table come back?

A Clay table that you created from an Audiences segment with **Add to workbook** doesn't refill itself after you delete its rows. **Add to workbook** is turned off by default and is enabled for individual workspaces on request. A segment-connected table gets records from its segment in two ways only:

-   **When the table is created**, all of the segment's current records are imported into the table once, up to 50,000 rows.
-   **After that**, only records that newly join the segment are added to the table, within about 15 minutes of joining.

Records that were already sent to the table aren't sent again. So if you delete rows from a segment-connected table, those rows don't come back from the segment, however long you wait. The table has no resync, re-run, or backfill button for the segment. The table's source settings only show a **View [segment name]** link back to the segment.

Duplicating a segment-connected table doesn't help. The copy doesn't get its own feed from the segment: the segment stays connected to the original table only, and the duplicate gets no new segment records.

**To start over with all of the segment's records in a table:**

1.  Open the segment in Audiences and click **Send** in the top right.
2.  In the **Send** sidebar, click **Export action** → **Add to workbook**. If **Add to workbook** is the only export option for your workspace, the button shows that label directly.
3.  Complete the **Send to workbook** dialog. Clay creates a new table and imports the segment's current records into it.
4.  Add your enrichment and formula columns to the new table again.

### Can I add another segment to an existing segment-connected table?

No. A Clay table created from an Audiences segment with **Add to workbook** receives records from that one segment only. You can't add a second segment as a source to the existing table, and **Add to workbook** always creates a new table rather than adding records to an existing one. **Add to workbook** is turned off by default and is enabled for individual workspaces on request.

To get records from more than one segment into the same table, create a new segment in Audiences whose filters cover the records from both segments, then send that segment to a table with **Add to workbook**.

**To run the same columns and enrichments on several segments, use a workflow instead of a table.** A workflow's segment trigger (**New member in segment** in the trigger picker, shown as **Member added** on the trigger node) can watch more than one segment:

1.  Open a segment in Audiences and click **Send** → **Send to workflow**, then build your enrichment and scoring steps as workflow nodes.
2.  Open the trigger node and click **Add segment** to add each additional segment.
3.  The trigger node shows how many segments it watches, for example **2 segments**. Click it to see the list of segments.

Records that enter any of the connected segments run through the same workflow steps. See [Connecting a workflow to a segment](audiences.md#connecting-a-workflow-to-a-segment) for how to publish the workflow and run it on members already in a segment.

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
