---
title: Auto-run
description: Control when Clay enrichments run automatically — the run decision tree, table-level and column-level toggles, Keep existing results, and common scenarios.
last_synced: 2026-07-01T00:00:00.000Z
---

# Auto-run

Auto-run automatically runs enrichments whenever rows are added or edited, keeping your table current. You can control this feature at multiple levels:

-   **Table-level** (master control)
-   **Column-level** (individual control)
-   **Conditional logic**

## How Clay decides whether a cell runs

Every time a source runs or re-runs, Clay walks through a short decision tree before executing any enrichment cell. Understanding this flow helps you predict exactly which cells will fire — and which will be skipped.

**Note on existing rows:** Whether an existing row re-enters this pipeline at all depends on the **Update existing rows** toggle in your source column settings (covered in the [Update Existing Rows toggle](#update-existing-rows-toggle-for-scheduled-source-imports) section below). When that toggle is off — the default for most source types — source re-runs only introduce new rows; existing rows are not re-evaluated.

**Step 1 — Table-level auto-run**

-   If the table's **Auto-run toggle is off** (shows "Manual"): the cell is marked stale and skipped. It will only run on a manual click.
-   If the table's **Auto-run toggle is on** (shows "Auto-run"): Clay checks the **"Keep existing results"** setting.
    -   **"Keep existing results" on (default for new tables)**: only cells that are new, empty, or errored are eligible to run. Cells with an existing successful result are preserved and skipped.
    -   **"Keep existing results" off**: all cells are eligible; Clay proceeds to step 2.

**Step 2 — Column-level auto-run**

-   If the **column's Auto-run toggle is off**: the cell is marked stale and skipped (only runs on a manual click).
-   If the **column's Auto-run toggle is on** (default): **the cell runs**.

**Note: Adding a People, Companies, or Jobs list-builder source to an existing table auto-runs enrichments on the first 10 rows only.** When you use a People, Companies, or Jobs search source to add rows to an existing table — including tables created by duplicating a workbook and then adding a source afterward — Clay automatically queues enrichments for only the **first 10 imported rows**. The remaining rows are added to the table but do not trigger auto-run. This is intentional behavior to prevent unexpected credit burns. This 10-row cap applies only to the initial source setup; subsequent scheduled runs of the same source run enrichments on all newly imported rows. To process the remaining rows, manually run them: select all rows in the table, right-click, and choose **Run [N] rows** — or right-click the first column in your workflow and select **Run column**.

## Table-level auto-run (master control)

Table-level auto-run acts as the master switch that controls automatic enrichment for the entire table.

-   When **enabled**: Enrichments run automatically whenever rows are added or edited.
    -   New tables use **"Keep existing results" on** by default — only errored, empty, or new cells run automatically. Cells that already have existing data **will not** run automatically unless you turn off Keep existing results.
-   When **disabled**: You must manually click cells to trigger enrichments.
-   **Default setting**: Enabled by default — Clay is designed to automatically enrich data as soon as it arrives.

**Note:** There is no workspace-wide setting to disable auto-run across all tables at once. Auto-run must be configured individually for each table.

**To enable or disable table-level auto-run:**

**Note:** The Auto-run toggle cannot be changed while the table is actively running. Stop the run first by clicking the **Stop** button in the run summary panel at the bottom-right. If the toggle remains greyed out after stopping, try a hard refresh (`Cmd+Shift+R` on Mac, `Ctrl+Shift+R` on Windows/Linux) to clear stale browser state.

1.  Click the `⛭` icon in the top toolbar, or click the table name and navigate to **Run Settings**.
2.  Toggle the `Auto-run` mode.
3.  If enabling, choose:
    -   `Continue without running` — Don't run existing cells right now.
    -   `Update cells` — Immediately run all cells that are out-of-date.

**Note:** Rows added while auto-run was disabled are **not** automatically queued when you re-enable auto-run. Choosing `Continue without running` leaves those rows unrun — they will not trigger on the next source sync. To process them, either choose `Update cells` when re-enabling, or manually trigger the column (right-click the column header → **Run column** → **Run N empty or out-of-date rows**).

### Keep existing results

"Keep existing results" is only available when Auto-run is turned on. **This setting is on by default** for new tables — Clay skips cells that already have a successful result rather than re-running them on every source sync.

-   With this **on (default)**: only empty, errored, or new cells run automatically — cells with existing successful results are skipped.
-   With this **off**: all cells are eligible to run, including ones that already have results.

**To change "Keep existing results":**

1.  Click the `⛭` icon in the top toolbar (or click the table name → **Run Settings**).
2.  Make sure the `Auto-run` toggle is **on**.
3.  Check or uncheck the **"Keep existing results"** checkbox as needed.

**Tip:** Keep "Keep existing results" on (the default) to protect credits from being spent re-running enrichments on rows that are already complete. Turn it off when you explicitly want enrichments to re-run on all rows — for example, after updating an enrichment prompt or adding a new provider to a waterfall.

**Note:** Changing "Keep existing results" does **not** automatically re-run cells already showing the out-of-date indicator — the new setting only applies to future auto-run triggers. To refresh currently stale cells:

-   **Turn off "Keep existing results"**: a prompt appears asking whether you'd like to update out-of-date cells — click **Update cells** to immediately queue all stale cells.
-   **Run from the column header**: right-click the enrichment column header → **Run column** → **Run [N] empty or out-of-date rows**.
-   **Re-trigger auto-run**: toggle Auto-run off, then back on, and choose **Update cells** to queue all currently stale cells.

### Understanding the out-of-date indicator

The out-of-date clock indicator on a cell means the cell is stale — it has an existing result but auto-run is not re-running it. The most common cause is "Keep existing results" being enabled: Clay skips cells that already have a result rather than overwriting them and spending credits. The cell's current value is still usable downstream; other columns can reference it normally.

A cell also shows as out of date when its inputs have changed since it last ran — for example, if an upstream column with auto-run enabled re-ran and updated its values, or if the column's own configuration was modified (such as editing a prompt). In these cases the indicator is informational: the existing value is still valid and usable downstream. In many cases re-running would produce the same result, so only trigger a re-run if you specifically need fresh output.

**Manual tables and sequential column runs:** If your table is in Manual mode and you run enrichment columns one at a time from left to right, you may see the out-of-date indicator appear across most columns — including ones you've already run. This is expected behavior, not a bug. Every time you run an upstream column, Clay immediately marks all downstream columns that depend on it as out of date, because their inputs may have changed. In a table where columns feed sequentially into each other (for example, a scoring table), running them in order creates a wave of stale indicators that propagates forward as you work. **Your data is not broken**: cell values marked out of date because auto-run is off are still valid and can be referenced by other columns without blocking downstream runs.

Since the table is in Manual mode, these indicators won't auto-clear. A few options:

-   **Ignore the icons** if the values look correct — the clock icon in this context is a workflow indicator, not a data quality signal.
-   **Run all columns in order** — right-click each column header from left to right and select **Run column → Run [N] empty or out-of-date rows** to clear all stale indicators in one pass.
-   **Switch to auto-run with "Keep existing results"** — turn on Auto-run and check **Keep existing results**. The table will then automatically queue only empty, errored, or new cells when dependencies change, without re-running (and spending credits on) cells that already have results.

**"Keep existing results" with unexpected out-of-date indicators:** If you're using "Keep existing results" and notice cells marked as out of date — even though you haven't made any changes to the table — this is expected behavior, not a bug. When an upstream column re-runs and updates its output (for example, because a scheduled source refresh ran, or an upstream enrichment recomputed), Clay marks dependent downstream cells as out of date because their inputs have changed. With "Keep existing results" enabled, Clay preserves those existing cell values instead of automatically re-running them. **Your data is not lost**: the existing values are still intact and usable downstream. If the current values look correct, you can ignore the clock icons. To get updated results, force-run the flagged columns manually — right-click the column header → **Run column** → **Run [N] empty or out-of-date rows** — since "Keep existing results" mode will not refresh them automatically.

If a cell **keeps** showing as out of date even after you re-run it, check whether an upstream column has auto-run enabled. Each time that upstream column runs and updates its output, Clay marks any column referencing it as out of date again — even one you just re-ran. To resolve this:

-   **Disable auto-run on the downstream column** — the column will only run when you trigger it manually. This is the most targeted fix and leaves the upstream column untouched.
-   **Disable auto-run on the upstream column** — stops the cascade at its source, but means the upstream column also switches to manual-only mode.
-   **Enable "Keep existing results"** at the table level — cells with existing results are no longer automatically re-run, so the stale indicator appears but no credits are consumed re-running the column on every upstream change.

### Understanding the manually-overwritten indicator

When you type a value directly into a cell that has a formula — or paste values in bulk into a formula column — Clay treats each entered value as an intentional override and suspends the column's formula for those cells. Affected cells display a pencil icon; hovering over it shows the tooltip "This cell's value has been manually overwritten."

While a cell is in this state:

-   **The formula is suspended for that cell.** Auto-run skips overwritten cells — they are not queued to run, do not consume credits, and do not trigger downstream columns.
-   **The manually entered value is treated as the row's authoritative value.** Other columns can still reference it, but the formula that drives this column will not re-evaluate for that row.

**To restore a cell to its formula-driven state:** hover over the cell and click the ↺ **Reset to original value** button. This clears the overwrite state and allows the formula to re-run on the next auto-run trigger.

**Why this commonly appears:** When you paste data in bulk into a formula column — for example, pasting email addresses into a waterfall lookup column — Clay marks each pasted cell as overwritten to preserve your input. If enrichments stop running for pasted rows, look for the pencil icon and use the ↺ **Reset to original value** button to resume formula-driven behavior for those cells.

## Column-level auto-run (individual control)

Column-level auto-run controls whether a specific enrichment runs automatically. This setting only works when table-level auto-run is enabled.

**To enable or disable column-level auto-run:**

1.  Click the name of the column → `Edit column`.
2.  Toggle auto-run on/off under `Run settings`. Click `Save` to apply your changes.

**Important:** Table-level auto-run acts as the parent setting:

-   If table-run is **OFF**: No columns will run automatically, regardless of column settings.
-   If table-level is **ON** + column-level is **OFF**: That specific column won't run automatically.
-   If table-level is **ON** + column-level is **ON**: Column runs automatically. ✅

## Conditional runs ("Only run if")

Add conditional logic to control when an enrichment executes. The enrichment only runs when the formula evaluates to true.

**Common use cases:**

-   Only run if profile URL exists: `Profile URL is not empty`
-   Only run if company size > 50: `Company Size > 50`
-   Only run if email is missing: `Email is empty`
-   Only run for specific industries: `Industry = "Technology"`

**To set up conditional runs:**

1.  In column settings (`Edit column`), enable `Only run if` under `Run settings`.
2.  Click `Use AI` to write the formula in plain language, or write the formula manually using column references.
3.  Click `Save` — the enrichment now only runs when the condition is met.

**Why this matters:** Conditional runs help control costs by preventing enrichments from running when data already exists or conditions aren't met.

For full documentation on conditional run syntax, operators, and advanced patterns, see [Conditional runs](conditional-runs.md).

## Update Existing Rows toggle (for scheduled source imports)

The **Update existing rows** toggle in your source column settings controls whether source re-runs update records that already exist in the table (matched by their unique identifier). This is a source-level setting, separate from the enrichment cell decision tree above — it determines whether existing rows even re-enter the auto-run pipeline.

-   **Update existing rows: ON** — When the source re-runs, existing rows are updated with the latest source data and re-enter the auto-run pipeline. Use for ongoing data hygiene and backfills.
    -   **Note**: To allow enrichments to re-run on updated existing rows, also turn **"Keep existing results" off** — otherwise, cells that already have a result will be skipped even though the source data was refreshed.
-   **Update existing rows: OFF** (default for most source types) — Source re-runs only add new records. Existing rows with matching identifiers are not touched. More credit-efficient for workflows where you only need to enrich newly added records.

**To configure:**

1.  Click the source column header → `Edit column`.
2.  Toggle **Update existing rows** on or off based on your needs.

## Common scenarios

**Full automation:**

-   Table-level: ✅ ON
-   All columns: ✅ ON
-   Conditional runs: Not set
-   **Result**: New rows → All enrichments run automatically

**Selective automation:**

-   Table-level: ✅ ON
-   Email column: ✅ ON
-   Other columns: ❌ OFF
-   **Result**: New rows → Only email enrichment runs automatically

**Manual control (testing mode):**

-   Table-level: ❌ OFF
-   Column-level: ✅ ON (doesn't matter)
-   **Result**: New rows → Must manually click cells to run enrichments

**Conditional execution:**

-   Table-level: ✅ ON
-   Column-level: ✅ ON
-   Conditional run: "Only if profile URL exists"
-   **Result**: Rows with a profile URL → Enrichment runs; Rows without → Skipped

## Best practices

**When building/testing tables:**

1.  Turn table-level auto-run OFF to prevent accidental credit usage.
2.  Add sample data (5-10 rows).
3.  Manually test enrichments by clicking cells.
4.  Refine your setup.
5.  Turn auto-run ON when ready for production.

**When running production workflows:**

1.  Turn table-level auto-run ON.
2.  Configure column-level toggles strategically.
3.  Use conditional logic (`Only run if`) for cost control.
4.  Monitor credit usage.

**For credit control:**

-   Use `Only run if` conditions extensively.
    -   Example: `Email is empty` — only find email when missing.
    -   Example: `Company Size > 50` — only enrich companies in your ICP.
-   For table auto-run, we recommend keeping "Keep existing results" on (the default) to avoid accidentally overwriting data and wasting credits.
