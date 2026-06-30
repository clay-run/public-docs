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

**Note:** During sandbox mode, your regular table becomes read-only and cannot be updated directly — the **All data** tab shows a **View-only** indicator while sandbox is active. You can switch between your sandbox and the read-only production table using the tabs menu. All recurring sources ([webhooks](https://www.clay.com/university/guide/webhook-integration-guide), [signals](https://www.clay.com/university/guide/signals), etc.) and [scheduled runs](https://www.clay.com/university/guide/scheduled-columns) will still run while sandbox mode is active.

**Sculptor and sandbox mode:** [Sculptor](https://www.clay.com/university/guide/sculptor) automatically puts your table into sandbox mode whenever it builds new columns. This lets you review and validate Sculptor's changes before they go live.

> **Important:** If Sculptor put your table into sandbox mode, use the **Review changes** button to publish Sculptor's columns to your live table — do _not_ click **Exit Sandbox**, which will discard all of Sculptor's proposed changes without saving them. See the [Sculptor — Sandbox mode](https://www.clay.com/university/guide/sculptor) section for the full step-by-step.

## Using sandbox mode

In sandbox mode, you can test formulas, waterfalls, and enrichments. **Here are some other helpful notes:**

-   You cannot add or edit sources in sandbox mode. To make these changes, first return to your normal table, then re-enable sandbox mode.
-   To prevent accidental updates, all outbound actions (actions that send data such as exporting or [Write to Other Table](https://www.clay.com/university/guide/write-to-table-integration-overview)) are automatically disabled in sandbox mode.
    -   However, you can still manually run individual cells or columns if needed.

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
