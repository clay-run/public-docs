---
title: Functions
description: Functions let you convert any enrichment sequence into a reusable
  workflow. Once created, you can use it across any table — and any updates you
  make to the…
last_synced: 2026-04-26T01:40:01.780Z
---

# Functions

Functions let you convert any enrichment sequence into a reusable workflow. Once created, you can use it across any table — and any updates you make to the function automatically apply everywhere it's used.

**Functions** let you turn any enrichment sequence you've built in a table into a reusable, centrally managed workflow that you can use anywhere — so you can standardize your best logic, stop rebuilding the same columns across tables, and propagate updates everywhere the moment you make them.

## What functions are for

Functions are built for workflows you'd otherwise rebuild from scratch in every table. Common use cases include:

-   Company enrichment: Given a domain or LinkedIn URL, return firmographic data (revenue, employee count, website traffic) — collapsing 15+ columns into one.
-   ICP scoring: Enrich sourced accounts against a pre-defined scoring methodology and update your CRM with the result — governed centrally so logic never drifts between tables.
-   Inbound qualification & routing: Run enrichments to identify and score inbound leads, apply routing logic, and update your CRM — all from a single function column.

## Creating a function

**Create from existing workflow:**

1.  Open any Clay table with the enrichment sequence you want to make reusable.
2.  Select the columns to include in the function:
    -   **Individual selection:** Hold `Cmd` on Mac or `Ctrl` on Windows and click each column header you want to include.
    -   **Range selection (recommended for waterfall sequences):** Click the first column header, then hold `Shift` and click the last column header to select the full contiguous range. For waterfall enrichments, selecting the full range ensures only the entry-point inputs appear in the function dialog — not every internal provider or validation step.
3.  **With your columns highlighted**, right click on a column and select `Save as function`.
4.  In the dialog that appears:
    -   **Confirm function name/description** — We've auto-filled these fields using AI given the selected workflow. Please audit this to make sure there is a descriptive name/description that you can use to find this function later.
    -   **Define your inputs** — the values that will change from table to table (e.g., `Domain`). Everything else is fixed logic that stays the same.
    -   **Define your outputs** — the value that you will return from the function.
    -   Note: You can change all the above settings after you create the function as well.
5.  (Optional) Check `Replace columns with function` to swap out the original columns in your table with the new function
    1.  Clay will copy over all the existing data so nothing is lost. **This can take a few minutes for larger tables**.
6.  Click `Create` → `Create`. Your function now appears in the left-hand column of your table.
    1.  You can also click `Create + Open in Function Editor` to view/edit the new functions immediately (See "Editing a function" for more details).
7.  The function is now ready to be used in your workflow and will also appear under the `Functions` tab on your Clay homepage.

**Create function from scratch:**

1.  From the homepage, click on `Functions` in the sidebar.
2.  Click on `+ New Function` on the top right.
3.  This will create a blank function that you can directly edit, add inputs/outputs, etc.

## Calling a function from a table

1.  Open any table where you want to run the enrichment.
2.  Click `Tools` and select an option under `Functions`.
3.  In the configuration panel:
    -   **Search/Choose which function to run.**
    -   **Map your inputs** — connect the function's input fields to the corresponding columns in this table (e.g., map `Domain` in the function to the domain column in your table).
        -   You can also add a static value for an input (if a value is not changing for a function) by toggling the inputs mode button at the right of each input.
4.  Run the column. Clay spins up a background mini-table, runs every enrichment step, and returns the outputs to your table as a single column.

**Note:** All enrichment logic runs in a background mini-table invisible to you. Your main table stays clean — what used to be 20–50 enrichment columns becomes a single `Run Function` column.

## Editing a function

1.  On your Clay homepage, go to `Functions` and select the function you want to edit.
2.  Select `Edit function` in the top of the function's settings panel.
3.  While your function is in edit mode, you can safely modify and test your function.
    -   You can click `Add test inputs` to:
        1.  Manually enter test data.
        2.  Select recent inputs to replay inputs received by your live function.
    -   Additionally you can select up to 50 archived rows from your live function and `Debug` in edit mode to help safely investigate in a running mode.
    -   Note that no changes made here will apply to the live function until published.
4.  Once your changes are ready, click `Review Changes` to view your pending changes and click `Publish Changes` to apply your changes to your live function.

## Managing MCP access and credit budgets

When you enable functions for MCP (Model Context Protocol), admins can control who can access Clay from tools like ChatGPT and Claude, and set credit limits. You can set default budgets, override limits for specific users, monitor usage, and sync identities from Salesforce.

For a full walkthrough, see [MCP settings](https://university.clay.com/docs/mcp-settings).

## FAQs

### What plans are functions available on?

Functions is available on all paid plans at no additional cost, including paid legacy plans. Advanced capabilities such as MCP access are gated to higher tiers.

### Does running a function cost extra credits?

No. Functions do not add their own credit or action cost. Credits are consumed by the individual enrichment actions inside the function (e.g., a profile lookup, an email waterfall step) and are attributed to the table where the function is called, not to the function itself. If a function only contains formula columns and no enrichment steps, it will cost zero credits. Estimated cost is visible in the function editor panel and also in the table where the function is referenced.

### Is there a row limit for functions?

No. As of General Availability, functions support unlimited rows via passthrough. Functions also include a 10x speedup and fair sharding for parallel execution, so large workloads are distributed efficiently instead of queuing. Prior to GA, Functions had a 50,000-row limit.

**Note:** The function's live view displays only the most recent **1,000 rows** at a time. This limit is intentional: functions are passthrough tables, and keeping the active row count low ensures there is enough space for new incoming records to be processed. All rows are fully processed and their results returned to the calling table regardless of this limit.

To review rows beyond the 1,000 shown in the live view, click the **Archive** button in the function table's toolbar. The Archive section shows historically processed rows organized by timeline, and you can export the full set as a CSV. If you need to retain more active rows in the live view (for example, for easier auditing of recent runs), open the auto-delete settings for the function table and update the **Number of rows to keep** field — though increasing this limit on high-volume functions can slow processing.

### What's the difference between an input and a column in a function?

Inputs are the values that change from table to table — typically identifiers like a company domain, a person's full name, or a LinkedIn URL. You define them when saving the function, and map them when calling the function from a different table. Columns that aren't marked as inputs are fixed enrichment logic that runs the same way every time.

### Why can't I run/edit a function in "Live" mode directly?

Viewing a function in "Live" mode provides visibility to current/past function runs and mainly serves as an "audit log" of data processing. Once run, rows are effectively archived and cannot be modified from within the function itself.

-   If you want to edit/test your function logic, click `Edit function` to safely change, test, and publish your changes.
-   If you want to re-run past rows in a function, re-run the function column/cells in the origin table that called the function itself. This will generate a new row in your function which will be automatically run on the latest configurations.

### Can functions call other functions?

Yes. Functions can be nested — a function can call another function as part of its enrichment sequence, letting you compose complex workflows from smaller, validated building blocks.

### What happens if I edit a function while it's running in a production table?

While in edit mode, your function continues to process inputs it receives from production tables. When you publish an edit to your function, the changes apply to all inflight and future rows that the function processes. Note that you can pause your function before publishing changes to ensure that inflight rows are applied with the changes.

### How are functions different from column templates?

Column templates are saved configurations for a single column that you apply manually to new tables — they're useful for one-off enrichments but aren't synced across your workspace. Functions are live, centrally managed workflows: edit the function once and every table calling it updates automatically. Functions also run as single columns in your main table, reducing potential column-limit constraints from your workflows.

### Is there version history for functions?

No, functions don't currently have a version history.

### What is the main use case for functions?

Functions eliminate duplicate work when you need the same workflow in multiple tables. Build your logic once as a function, then reference it anywhere — no more copying enrichment sequences table by table. Common examples include qualification and routing workflows, or repeatable enrichment sequences like "get firmographics from domain."

### Does saving columns as a function rerun those columns and consume credits?

No. Saving columns as a function preserves the existing data without rerunning the enrichments. You won't be charged credits twice.

### What happened to my original columns and prompts after I used "Replace columns with function"?

When you check **Replace columns with function** during function creation, Clay doesn't delete your original columns — it moves them inside the function. All column configurations, AI prompts, enrichment settings, and run conditions are preserved intact inside the function's internal table.

**To view and copy your original prompts:**

1.  In your table, click the function column's header (for example, "Enrich with all columns for…").
2.  Select **Edit function** to open the function editor.
3.  Your original columns appear inside the function exactly as they were — click any column header to see its full configuration, prompt text, and settings. From here you can copy any prompt out to reuse elsewhere.

**To restore the original separate columns:**

There's no one-click way to split a function back into standalone columns. If you need the original column layout back, use [table version history](table-versions.md):

1.  In your table, click **History** (bottom-right corner) → **All configuration versions**.
2.  Find a version taken before you created the function.
3.  Click **Restore Configuration** and confirm.

Restoring removes the function column (which was added after the snapshot) and brings back your original columns with their configurations. Note that table versioning restores **structure and configuration only** — cell value data is not affected by a version restore. See [Table versions](table-versions.md) for full details on what changes.

### Can I use a function someone else on my team built?

Yes. All workspace functions are available to use in your tables — no special permissions needed. Use them as-is, duplicate and modify for your needs, or request edit access from the owner to collaborate directly.

### What is the difference between editing a function and pausing a function?

**Editing** enters a sandbox mode where you can make changes while the function continues running live. Your edits only take effect when you publish them.

**Pausing** prevents the function from accepting new rows into its processing queue. Rows already queued or in progress before you paused will still run to completion. Click **Resume** from the function's ellipsis (⋯) menu to re-enable the function. Use Pause when you need to gate new work without disrupting rows already in flight — for example, while updating an API key or fixing a configuration error.

### What is the difference between pausing a function and stopping a function?

**Pause** prevents new rows from entering the function's processing queue. Rows already queued or actively running will continue to completion. Click **Resume** from the function's ellipsis (⋯) menu when you're ready to accept new rows again.

**Stop** attempts to cancel both actively running rows and rows already waiting in the queue. Allow a few minutes for the cancellation to fully take effect.

Use **Pause** when you want to temporarily suspend new work (for example, while fixing a configuration error) without discarding rows already in flight. Use **Stop** when you need to halt all processing — rows that were queued will be cancelled and would need to be re-triggered manually.

### If I edit a function while it's live, will rows that already ran show as stale?

No. Previously processed rows remain unchanged and won't be marked as stale. Only new rows processed after you publish your changes will use the updated logic.

### What columns should I include when building a function?

Include action columns (enrichments, Claygents, waterfalls) — not static input columns like company name or domain. Action columns contain the reusable logic you want to apply across tables.

Remember: every column you include becomes a required input. More columns mean more inputs users must provide when calling the function.

### How do I save a waterfall as a function, and why do I see "Function inputs must be unique"?

**Saving a waterfall as a function:**

The correct method is to right-click the **final waterfall output (merge) column** — the combined result column at the end of the waterfall group — and choose **Save as function** from the column dropdown. Individual waterfall step columns (the per-provider sub-columns) do not expose "Save as function" by design. Only the merge column does.

Selecting just the merge column captures the full waterfall sequence — every provider step, run condition, and validation step — and packages it into the function. You do not need to include the individual step columns separately.

**"Function inputs must be unique" error:**

This error means two or more inputs in the "Save as function" dialog share the same name. Clay auto-generates a unique name for each input when you open the dialog, but if you manually rename an input to match another already in the list, the validation fails.

To fix it: review the input names in the dialog, make sure each one is unique, and then click **Create**.

### How do I configure which columns are returned from my function to the calling table?

Every function includes a built-in **"Send data back"** column — the final step that controls what data is returned to the table calling the function. Opening that column's settings reveals a **Configure** section with a **"Choose output data to send"** checklist. Only columns that are checked will be sent back to the calling table; unchecked columns are not returned, even if they contain data.

**To access and configure this setting:**

1.  Open the function in edit mode (from your Clay homepage → **Functions**, or click the function column in your table and select **Edit function**).
2.  In the function editor, locate the **"Send data back"** column — the last column in the function.
3.  Click its column header to open the settings panel.
4.  Under **Configure → Choose output data to send**, you'll see a checklist labeled **"Selected columns (N of M)"** listing the function's columns.
5.  Check each column whose values you want returned to the calling table.
6.  Click **Publish Changes** to apply.

If a column's data is not appearing in the calling table, check whether that column is selected here — it may exist in the function but be unchecked in this list.

### Why doesn't my function output appear in the formula column's `/` field picker?

When you type `/` in a formula column to reference another column, Clay scans the first **100 rows** of the table to determine which column outputs are available. If your function column has no populated results in those first 100 rows — for example, because the function has only run on rows further down the table — its outputs won't appear in the picker even if they're correctly configured.

**To fix this:**

1.  Confirm the output is selected in your function's **"Choose output data to send"** checklist (see the FAQ above). If the column isn't checked there, no data will return regardless.
2.  Run the function on at least a few rows so that output values are populated.
3.  If those populated rows fall past row 100 in the table, sort the table by any populated column (for example, a domain or name column) to bring rows with function results to the top.
4.  Re-open the formula column and type `/` — the function outputs should now be discoverable.

### Why aren't fields from a row input available in the "Choose output data to send" checklist?

When you configure a function input as a **"Rows from..."** input (passing an entire row), that row is stored as a source field inside the function. Source fields are excluded from the **"Choose output data to send"** checklist — only the function's top-level data columns (enrichment results, formula columns, and other data columns) appear there.

To return a value that comes in through a row input as function output:

-   **Create a formula column inside the function** that extracts the specific value you need from the row input. That formula column will appear in the "Choose output data to send" checklist as a selectable output.
-   **Or, map individual column values as inputs instead of passing the whole row.** In the function's input configuration, map each specific value you need as a separate named input — those values are then directly accessible in the function's columns and can be selected as outputs.

### How do I return a single output field when two enrichment columns each cover the same data but only one runs per row?

If your function uses two enrichment columns that cover the same data (e.g., two person enrichment providers where only one runs per row based on a run condition), the "Send data back" step maps column values by reference — it does not accept inline formulas to merge or transform values within the step itself.

The workaround is to create a **formula column** (Merge columns) inside your function that coalesces the two enrichment columns, then use that formula column as the output:

1.  Add a **Merge columns** column inside your function. Use the `||` operator to pick whichever enrichment is populated:

    `{{Enrichment A}}?.person || {{Enrichment B}}?.person`

2.  Give the column a clear name (e.g., `Merged Person Data`).

3.  In your function's "Send data back" step, select `Merged Person Data` as the output. Your caller table receives one field instead of two.

**Note:** Formula columns store their result as **text**. If you're coalescing JSON objects, the output will be a serialized string. To make this explicit, wrap with `JSON.stringify`:

`JSON.stringify({{Enrichment A}}?.person || {{Enrichment B}}?.person || null)`

To access the object's sub-keys downstream, parse it back with `JSON.parse({{Merged Person Data}})`.

### How do I merge multiple list outputs from different enrichment columns into one combined list?

If your function has several enrichment columns that each return a list of items — for example, multiple Claygent columns that each find contacts in a different industry segment — each column's output lands in the calling table as a separate field. By default, you'd need one **Send row for each item in a list** action per output column.

To reduce this to a single **Send table data** action that covers all columns at once, use formula mode in the list input to concatenate the arrays:

1.  In the calling table, add or open your **Send table data** column.
2.  Choose **Send row for each item in a list**.
3.  In the list input field, click the **gear icon** on the right and select **Formula** (instead of "Text with Tokens").
4.  Enter a formula that concatenates all of the function's list outputs using `.concat()`:

    `({{Run Function}}?.Claygent1?.contacts || []).concat({{Run Function}}?.Claygent2?.contacts || [], {{Run Function}}?.Claygent3?.contacts || [])`

    Replace `Claygent1`, `Claygent2`, etc. with the actual field names your function returns, and replace `contacts` with the sub-field that holds the list items within each output.

5.  Save the column. Clay iterates over the merged list and writes each item as a row in the destination table.

**Why this is needed:** Referencing multiple list-valued outputs side by side without a formula does not merge them — Clay receives separate arrays rather than a single list, and the column will fail at runtime with a list error. The `.concat()` formula produces one unified array from all the sources.

### What does "Awaiting Callback" mean on a function column?

When you call a function from a table, that column shows **Awaiting Callback** while the calling table waits for the function to finish processing and return results. The status resolves once the function's **"Send data back"** column runs successfully and sends results back.

If the **"Send data back"** column has a **run condition** that is not met for a particular row, the function will not return data for that row. The calling table's cell will remain in **"Awaiting Callback"** until a 24-hour timeout expires, at which point it resolves to an error state. Downstream columns in the calling table that depend on the function output will not run until the cell resolves.

**To re-run rows stuck in Awaiting Callback:**

Go back to the origin table and re-run the function column for those rows. Each row's pass through a function is a one-way trip — you cannot re-trigger processing from within the function itself. Re-running the function cell in the origin table dispatches a fresh invocation that runs on the latest function configuration.

There is no per-row force-stop for cells in Awaiting Callback. To halt all processing immediately, you can pause the entire function — but this stops all rows, not just the stuck ones. Paused rows will resume when you unpause.

**To prevent downstream columns from waiting:**

-   Add a **run condition** on downstream columns in the calling table so they only run once the function column has returned a value (e.g., only run if `{{Function Column}}` is not empty).
-   Use `Clay.getCellStatus({{field_name}})` in a formula column to check the function column's status, then use that formula as a run condition on dependent columns.

### My enrichment data appears missing after a function ran against those columns — where did it go?

The data hasn't been deleted. When a function column runs, it receives data from any Claygent or enrichment columns wired as its inputs, processes it, and stores the results in the **function result column** in your main table. The original Claygent or enrichment column cells may appear empty or replaced — the processed data now lives in the function result column.

To find your data:

1.  **Filter the function column by "has results."** Click the filter button in the table toolbar, select the function column as the field, and choose **has results** from the status dropdown. This surfaces every row where the function ran and returned data successfully.
2.  **Click into any row marked success** to open the cell details panel on the right, where you can see the full data the function returned for that row.
3.  **Adjust what data comes back to your table.** Click the function column header to open its settings. Under **Configure → Choose output data to send**, check or uncheck which fields are returned to your main table. After saving, re-run the function on those rows for the changes to take effect.

Other useful column status filters you can apply to any function or enrichment column: **has no results** (ran but returned nothing), **has not run** (not yet processed), **is queued** (waiting to be processed), **is retrying** (a retry is in progress), and **is awaiting callback** (waiting for the function to finish and return results).

### Can I share a function with someone outside my workspace?

Yes. Enable "share as template" on the function to generate a shareable link. Anyone with the link can view the function's columns and create a table in their workspace using it.

### Can a function be enabled for MCP tools like ChatGPT, Claude, or Glean?

Yes, on supported plans. The `Enable for MCP` option in the function editor panel is available on modern Launch, Growth, Enterprise, and Legacy Enterprise plans. On other legacy plans (such as legacy Pro), the toggle does not appear in the function settings — if you do not see it, your workspace plan does not include this capability. Upgrading to a modern plan is required to enable custom Functions for MCP. For setup instructions, see [MCP settings](https://university.clay.com/docs/mcp-settings).

### How can I limit who can edit my functions?

1.  Click on the function.
2.  In the function's settings panel, scroll to the bottom to find `Access permissions`.
3.  Set it to `Admins and invited collaborators only` to restrict editing permissions to workspace admins and specific collaborators you invite.

### How do I debug specific rows while editing a function?

![](https://cdn.prod.website-files.com/687e604972375496b891fe58/69debe23823b4f78eeda763e_Functions%20Notion%20\(1\).webp)

You can test your function changes against real-world inputs by debugging selected rows:

1.  Open your function and click `Edit function`.
2.  Select one or more rows from your function table (including archived rows).
3.  Right-click on the selected rows and choose `Debug selected rows in edit mode`.
4.  The selected rows will run through your function using your current edits, allowing you to see how your changes affect specific inputs.
5.  Review the results to validate your changes before publishing.

This is especially useful when you want to test edge cases or troubleshoot specific inputs that previously failed or produced unexpected results.

### How do I make a function input optional?

When you create a function — including from a table that contains a Claygent step — all inputs default to required. This happens regardless of how the inputs are configured inside the source Claygent; the required/optional setting lives at the function level and must be set independently.

Each function input has a **Required input** setting. When this is enabled and no value is provided for that input on a given row, the row will not run — you'll see a "Missing required inputs" error on that cell.

To make an input optional:

1.  From your Clay homepage, click **Functions** and open the function you want to change.
2.  Click **Edit function** in the settings panel.
3.  In the inputs list, find the input you want to make optional and toggle off its **Required input** setting.
4.  Click **Publish Changes** to apply.

After this change, rows that don't have a value for that input will still run — they'll pass an empty value for that field instead of being skipped.

### Why do I see "please select a valid value" on a function input, and how do I fix it?

This error means a column reference in your function's input mapping has become stale. The most common cause is that a column in the source table was renamed or deleted after the function was set up — Clay loses the connection to that column ID even though the input mapping still appears configured.

To fix it:

1.  Open the affected function column in the table where the function is called.
2.  Click the **X** next to any input field showing the "please select a valid value" error to remove the broken mapping.
3.  Re-select the correct source column from the dropdown.
4.  Save the column.

If you haven't renamed or deleted any columns recently, the reference may have become stale after a table update — the remap will resolve it either way.