---
title: Sandbox mode
description: Learn about sandbox mode, a playground to safely iterate +
  experiment with your data! Also covers how to safely test a new version of a
  Clay workflow that your table calls, without affecting the published version.
last_synced: 2026-10-07T01:17:19.137Z
---

# Sandbox mode

Learn about sandbox mode, a playground to safely iterate + experiment with your data!

Sandbox mode is a special table mode that lets you safely build, test, and publish table configurations using a small subset of rows—without affecting your running workflow. **With sandbox mode you can:**

-   Test enrichments and integrations on a smaller dataset so you conserve credits and prevent accidental credit usage.
-   Hand-pick specific rows from your table to experiment with in your sandbox.
-   Keep your production table safe from changes while sandbox mode is active.
-   Review all changes before applying them to your full table.

## **Enabling sandbox mode**

1.  Click the `Sandbox Mode` button in the toolbar.
2.  After a few seconds, a new sandbox will be set up with sample rows, ready for you to make changes.
    -   **To discard changes and start a fresh copy of the sandbox:** Click `⚙️` → `Reset sandbox`.
    -   **To turn off sandbox mode:** Click `Exit Sandbox` in the toolbar. This will return you to your normal table and discard all unpublished changes in your sandbox.
    -   **If you close your browser tab or navigate away:** Your sandbox is saved automatically — no changes are discarded. When you return to the table, Clay redirects you back to your sandbox where you left off.

**Note on tables created from a source:** Sandbox mode requires a table that already has data in it — the **Sandbox Mode** button is disabled on empty tables. If you are creating a new table from a credit-consuming source (for example, a "Companies by product usage with HG Insights" table), the initial source run happens before sandbox mode is available. Use the **Maximum credit cost per run** setting in the source setup to cap spending during that first run. Once the table is created and rows are imported, enable sandbox mode before running any enrichment columns.

**Note:** During sandbox mode:

-   Your regular table becomes read-only and cannot be updated directly — the **All data** tab shows a **View-only** indicator while sandbox is active.
-   You can switch between your sandbox and the read-only production table using the tabs menu.
-   Lookup columns in other tables (`Lookup single row in other table` and `Lookup multiple rows in other table`) that point at this table keep reading your regular (live) table, not the sandbox copy. Sandbox copies don't appear in the lookup's `Table to search` picker. Edits you make in the sandbox aren't visible to those lookups until you publish them — see [Lookup Rows](lookup-rows.md#lookup-keeps-returning-old-values-after-you-edited-the-other-table-sandbox-mode).
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
-   Cell values in your sandbox rows — including values you typed or edited manually — **are copied to the matching rows in your regular table when you publish**, replacing any updates made to those rows since the sandbox was created. Rows you added manually in the sandbox are also added to your regular table if they contain data; empty rows are skipped, and rows that are still running when you publish are not copied.
-   Cell edits can't be published on their own. Publishing requires at least one column change, so if you've only edited cell values in the sandbox, `Review changes` stays greyed out. To change cell values in your regular table without a column change, click **Exit Sandbox** (this discards your sandbox changes) and make the edits directly in your regular table.
-   Changes to a column that affect downstream columns are shown in a nested format to clearly indicate which other columns may be impacted.

### Publishing changes

When you are ready to publish the changes in your sandbox to your regular table, you have two options:

-   `Publish and don't run` will sync all your column configuration changes to all data but will _not start_ a run for any of these columns. You would need to manually run them later.
-   `Publish and run` will sync all column configuration changes to all data **and** run all affected columns on all rows in the full table.

## Testing a new version of a workflow that your table calls

Sandbox mode is for tables only. Clay Workflows has its own draft-and-publish versioning instead. This section answers a common question: *"My table triggers a workflow I've published as V1. If I edit the workflow for V2, will V1 keep working, and how do I test V2 from a table?"* Workflows is currently in beta — if you don't see Workflows in your workspace, contact your Clay account team or support to enable it.

### Where is the Publish button for my workflow?

A new Clay workflow starts as a draft: the status pill next to the workflow name shows **Draft** until you publish it, then **Live**. You need edit access to the workflow to publish it. Where the **Publish** button appears in the workflow editor depends on how the workflow was built:

-   **Workflows built directly on the canvas:** click **Publish** in the top-right of the workflow editor's top bar.
-   **Workflows built with a setup guide** (for example, an audience enrichment, Find People, or Find Companies workflow): the top bar shows **Open guide** instead of a **Publish** button. Publish the workflow from the guide.

To publish a workflow that was built with a setup guide:

1.  Click **Open guide** in the top-right of the workflow editor.
2.  Go to the guide's **Review & run** step.
3.  Click the **Run** dropdown and select **Publish and run**.
4.  In the publish dialog, name the version and choose whether to run the workflow on existing records. Click **Publish and run** to confirm — the button reads **Publish** if you turn off running after publishing.

You can also ask the AI chat in the workflow editor to publish the workflow for you.

Publishing a workflow makes its triggers live, so a workflow with a segment, schedule, or webhook trigger can start running automatically once it's published. To stop a published workflow from running, pause its triggers — Clay Workflows doesn't have an unpublish button.

### Does editing a published workflow change the version my table runs?

No. Editing a published workflow doesn't change the version your table runs. After you publish a workflow, any edits you make go to a draft. Your table's **Invoke workflow** column (the "Run workflow" step that sends rows to a workflow) keeps running the published version until you click **Publish** again. The same is true for webhook, schedule, and segment triggers. Each workflow run is also pinned to the version it started on, so publishing a new version doesn't change runs already in progress.

If your table sends a field that the published workflow version doesn't use, the published version ignores that field — it doesn't cause an error.

### Can a table's Invoke workflow column run the draft version of a workflow?

No. A table's **Invoke workflow** column always runs the currently published version of the workflow. There's no setting to point a table column — or any other trigger outside the workflow editor, such as a webhook, schedule, or segment — at a draft.

The only way to run a draft workflow without publishing it is from inside the workflow editor: start a manual run from the editor, or hover a node and click its run button to test that one step.

### How do I test a new workflow version with new inputs from a test table?

To test a new version of a workflow from a table — for example, a version that needs inputs your published workflow doesn't have — create a separate copy of the workflow and test the copy, so your published workflow keeps running unchanged:

1.  Open your published workflow, open workflow settings, and click **History** to open the **Workflow history** panel.
2.  On the version you want to start from, open the **⋮** menu and select **Create new workflow**. Clay creates a new workflow from that version.
3.  In the new workflow, add the new inputs and logic, then click **Publish**.
4.  In a copy of your table (not your live table), add or edit an **Invoke workflow** column, select the new workflow in the **Workflow** field, and map its inputs. Run the column on a few rows to test.
5.  When the new workflow is ready, open the **Invoke workflow** column in your live table, select the new workflow in the **Workflow** field, and map its inputs again. Changing the selected workflow clears the existing input mapping, so you'll need to re-map every input.

Test from a copy of your table rather than your live table. Changes to your table — its columns, or the inputs your **Invoke workflow** column sends — aren't part of the workflow's version history, so changing them in your live table immediately changes what the published workflow receives.

### How do I roll a workflow back to an earlier version?

To roll a workflow back to an earlier version:

1.  Open workflow settings and click **History** to open the **Workflow history** panel.
2.  On the version you want, open the **⋮** menu and select **Restore this version**, then confirm with **Restore draft**. This replaces your current draft with that version — your live workflow doesn't change yet.
3.  Click **Publish** to make the restored version live.

The **Versions** dropdown in the workflow editor's top bar switches which version you're viewing in the editor. It doesn't roll the workflow back.
