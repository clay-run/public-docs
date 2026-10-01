---
title: Sandbox mode
description: Learn about sandbox mode, a playground to safely iterate +
  experiment with your data!
last_synced: 2026-04-26T01:40:36.624Z
---

# Sandbox mode

Learn about sandbox mode, a playground to safely iterate + experiment with your data!

Sandbox mode is a special table mode that lets you safely build, test, and publish table configurations using a small subset of rows—without affecting your running workflow. **With sandbox mode you can:**

-   Test enrichments and integrations on a smaller dataset so you conserve credits and prevent accidental credit usage.
-   Hand-pick specific rows from your table to experiment with in your sandbox.
-   Keep your production table safe from changes while sandbox mode is active.
-   Review all changes before applying them to your full table.

## **Enabling sandbox mode**

1.  Click the `Sandbox mode` button in the toolbar.
2.  After a few seconds, a new sandbox will be set up with sample rows, ready for you to make changes.
    -   **To discard changes and start a fresh copy of the sandbox:** Click `⚙️` → `Reset sandbox`.
    -   **To turn off sandbox mode:** Click `Exit sandbox` in the toolbar. This will return you to your normal table and discard all unpublished changes in your sandbox.
    -   **If you close your browser tab or navigate away:** Your sandbox is saved automatically — no changes are discarded. When you return to the table, Clay redirects you back to your sandbox where you left off.

**Note on tables created from a source:** Sandbox mode requires a table that already has data in it — the **Sandbox Mode** button is disabled on empty tables. If you are creating a new table from a credit-consuming source (for example, a "Companies by product usage with HG Insights" table), the initial source run happens before sandbox mode is available. Use the **Maximum credit cost per run** setting in the source setup to cap spending during that first run. Once the table is created and rows are imported, enable sandbox mode before running any enrichment columns.

**Note:** During sandbox mode:

-   Your regular table becomes read-only and cannot be updated directly — the **All data** tab shows a **View-only** indicator while sandbox is active.
-   You can switch between your sandbox and the read-only production table using the tabs menu.
-   All recurring sources ([webhooks](https://www.clay.com/university/guide/webhook-integration-guide), [signals](https://www.clay.com/university/guide/signals), etc.) and [scheduled runs](https://www.clay.com/university/guide/scheduled-columns) will still run while sandbox mode is active — under the same rate limits as your production table.

**Sculptor and sandbox mode:** [Sculptor](https://www.clay.com/university/guide/sculptor) automatically puts your table into sandbox mode whenever it builds new columns. This lets you review and validate Sculptor's changes before they go live.

> **Important:** If Sculptor put your table into sandbox mode, use the **Review changes** button to publish Sculptor's columns to your live table — do _not_ click **Exit Sandbox**, which will discard all of Sculptor's proposed changes without saving them. See the [Sculptor — Sandbox mode](https://www.clay.com/university/guide/sculptor) section for the full step-by-step.

## Using sandbox mode

In sandbox mode, you can test formulas, waterfalls, and enrichments. **Here are some other helpful notes:**

-   You cannot add or edit sources in sandbox mode. To make these changes, first return to your normal table, then re-enable sandbox mode.
-   To prevent accidental updates, all outbound actions (actions that send data such as exporting or [Write to Other Table](https://www.clay.com/university/guide/write-to-table-integration-overview)) are automatically disabled in sandbox mode.
    -   However, you can still manually run individual cells or columns if needed.

**Credits:** Sandbox mode is not free — enrichments and integrations consume credits normally. Because sandbox execution is limited to at most 50 rows (10 by default), credit consumption is much lower than a full-table run, but it is not zero. Think of sandbox as a credit-conservative testing environment rather than a zero-cost one.

### Adding data to the sandbox

When you start sandbox mode, the top 10 rows from your existing table will be duplicated as samples. Sandbox tables have a maximum of 50 rows.

**To add additional rows to your sandbox:**

1.  Click `Add test data`.
2.  Enter the number of rows and select your row selection mechanism.
    -   If you select `Top rows`, it will add the next set of rows from the top of the current view in all data.
    -   If you select `Random set`, it will randomly select rows from your `All data` tab.

**To add specific rows:**

1.  Navigate back to the `All data` tab using the top navigation.
2.  Select a set of rows in the table.
3.  Click `Add X rows to test data`.

## Publishing sandbox changes

> **Important:** To publish your sandbox changes, use the **Review changes** button described below — do _not_ click **Exit Sandbox** first. Clicking **Exit Sandbox** will discard all unpublished changes without giving you a publish option.

### Viewing changes

Click `Review changes` — visible in the tab bar above your table, to the right of the "Test data" / "All data" switcher — to view a list of all _structural_ column updates to your sandbox (compared to your regular table). If `Review changes` appears greyed out, it means no structural column changes have been detected yet (for example, you ran enrichments on sandbox rows but haven't added, updated, or deleted any column configurations).

**This includes:**

-   Adding/deleting a new column.
-   Renaming a column name/description.
-   Update configurations to a formula, waterfall, or enrichment.

**Notes on publishing changes:**

-   Visual updates (such as pinned columns, column ordering, and colors) won't appear in the list, **but** **_will_** **be applied when you publish**.
-   Manually added rows and manual overrides to individual cell data **will not be published**.
-   Changes to a column that affect downstream columns are shown in a nested format to clearly indicate which other columns may be impacted.

### Publishing changes

When you are ready to publish the changes in your sandbox to your regular table, you have two options:

-   `Publish and don't Run` will sync all your column configuration changes to all data but will _not start_ a run for any of these columns. You would need to manually run them later.
-   `Publish and run` will sync all column configuration changes to all data **and** run all affected columns on all rows in the full table.

## Testing a workflow before publishing (Workflows don't use sandbox mode)

Sandbox mode is only for tables. The workflow editor doesn't have a **Sandbox mode** button. To try a draft workflow on a small set of records before it runs on everything, use the **Test** button and the **Test data** panel. Workflows is currently in beta — if you don't see Workflows in your workspace, contact your Clay account team or support to enable it.

To test a workflow before you publish it:

1.  Open the draft workflow in the workflow editor (**Graph** view).
2.  Hover over the trigger node and click **Test** above the trigger card. The **Test data** panel opens at the bottom of the editor.
3.  Clay automatically adds up to **10** sample records from your trigger. For example, an audience segment trigger adds 10 members of the segment. Signal triggers add **3** sample records.
4.  Optional: click **Add data** to hand-pick more records. Each trigger can have up to **50** test records.
5.  Click **Run [N] rows** to run the draft workflow on only those test records. With the default sample, the button reads **Run 10 rows**. Results appear in the panel's columns.

Clicking **Publish** doesn't run your test records. Publishing makes the workflow live, so it runs on records that match the trigger (for example, new members that join the segment). For more on running workflows on existing segment members, see [Connecting a workflow to a segment](audiences.md#connecting-a-workflow-to-a-segment).

To get help building or editing a workflow, open [Sculptor](sculptor.md#how-do-i-open-sculptor-in-a-workflow) from the workflow editor's top-right toolbar.
