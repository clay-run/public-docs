---
title: Formulas
description: Generate formulas with AI to transform your data. Includes how to
  use today's date in a formula, pull error messages with getCellErrorMessagePreview(),
  check cell status with getCellStatus(), and keep date comparisons current automatically.
last_synced: 2026-04-26T01:40:01.780Z
---

# Formulas

Generate formulas with AI to transform your data.

## Generate formula with AI

The formula generator opens as a **sidebar** alongside your table, so you can see your data while building formulas.

To generate a formula with AI:

1.  Add a formula column (or open an existing formula column) to open the **Formula generator** sidebar.
2.  Describe what you want to calculate or transform. Type `/` to insert a column reference.
3.  Click **Generate** to create your formula.

A preview column appears inline in the table showing the formula output. The formula column and any referenced columns are highlighted; other columns are grayed out. To jump to a referenced column in the table, click its name under **Referenced columns** in the sidebar.

## Improve formula accuracy

If the formula produces incorrect output for some rows, you can provide examples to help the AI regenerate a better formula:

1.  Click a preview cell that shows a wrong result.
2.  Enter the correct value in the **Edit expected output** popover.
3.  Click **Regenerate** to get an updated formula based on your examples.

Once the results look right, click **Save column**.

## AI formula generator examples

Here are examples of formulas you can create with the formula generator:

1.  Extract the domain from {{Email}}
2.  Use {{LinkedIn URL}} if available; otherwise use {{LinkedIn Profile}}.url
3.  Extract the text after @ in {{Twitter Handle}}
4.  Split {{city}} by comma, keep everything before the first comma, remove "Area" if present, then add quotes
5.  Extract the first word from {{Column\_1}}, combine with {{Column\_2}}, then remove all non-letter characters
6.  Calculate the number of days between {{Created Date}} and {{Closed Date}}

## How Clay formulas work

Clay formulas are powered by **Clayscript**, a JavaScript-based language that evaluates expressions to transform your data. When you generate a formula with AI or write one manually, you're creating JavaScript expressions that Clay runs row-by-row.

**What's available in formulas:**

-   **Standard JavaScript**: All standard JavaScript objects and methods including `Math`, `String`, `Array`, `Date`, `RegExp`, `Number`, `Object`, and more.
-   **Lodash**: Access the full [Lodash](https://lodash.com) library using `_` for advanced data manipulation.
-   **Moment.js**: Use [Moment.js](https://momentjs.com) with `moment` for powerful date and time operations.
-   **Excel and Google Sheets functions**: Clay supports hundreds of familiar spreadsheet functions like `VLOOKUP`, `IF`, `SUM`, `CONCATENATE`, and many more through the [FormulaJS](https://formulajs.info) library.
-   **Column references**: When you reference a column like {{Email}}, Clay automatically passes the value from that column into your expression.
-   **Clay utilities**: A set of Clay-specific helper functions under the `Clay.*` namespace for reading cell metadata — for example, `Clay.getCellErrorMessagePreview()` and `Clay.getCellStatus()`.

### FAQs

### **Can I create or change my formula without running it?**

Yes! When editing a formula, you'll see the option to `Save and don't run enrichments`.

Clicking this prevents your formula from running on any enrichment columns that would cost credits. These columns will appear greyed out to indicate they're out of date.

### **How do I use today's date in a formula?**

Use `moment()` with no arguments to get the current date and time at the moment the formula evaluates. For example, to return `"Yes"` if an event date is more than 6 months in the future from today:

```javascript
moment({{Event Date}}).isAfter(moment().add(6, 'months')) ? "Yes" : ""
```

**Keeping the comparison current automatically**

Formula columns only re-evaluate when they are re-run (and the table's **Auto-run** is on). `moment()` will return the correct date each time the formula runs, but if your table sits idle the formula won't refresh on its own.

To keep a date comparison up to date without manually re-running the table each day, use an HTTP API column as a daily "clock":

1.  Add an **HTTP API** column (GET, no authentication needed) pointed at a free time API — for example `https://timeapi.io/api/time/current/zone?timeZone=UTC`. This column returns the current datetime whenever it runs.
2.  Reference the HTTP API column's output in your formula. Because Clay formula columns automatically re-evaluate whenever a referenced enrichment column changes (when Auto-run is on), the formula will re-run each time the HTTP API column updates. For example:

    ```javascript
    moment({{Event Date}}).isAfter(moment({{Today API.dateTime}}).add(6, 'months')) ? "Yes" : ""
    ```

3.  Schedule the HTTP API column to run daily: click the **⛭** icon in the top toolbar → **Run Settings** → **Re-run columns on a schedule** → **Only selected columns** → select your HTTP API column → **Day** → **Save changes**. Note: only enrichment/action columns are selectable here — formula columns cannot be directly scheduled, but the formula will update automatically as a downstream effect of the HTTP API column running. See [Scheduled columns](scheduled-columns.md) for full details.

Once the HTTP API column fetches a fresh date each day, any formula that references it automatically re-evaluates against the new value.

### **How do I pull an error message from an action column into another column?**

Use `Clay.getCellErrorMessagePreview()` in a formula column to capture the error text from any action (enrichment) cell that failed:

```javascript
Clay.getCellErrorMessagePreview({{Column Name}})
```

This returns up to **300 characters** of the error message — the same text shown when you hover over a failed cell. Messages longer than 300 characters are truncated at 297 characters and end with `"..."`.

A few important notes:

-   **The formula preview sidebar will show nothing** — this is expected. `Clay.*` functions are evaluated on the backend and cannot run in the preview. Save the column and the values will populate.
-   **Only works for action (enrichment) columns that have errored.** Returns empty for formula columns, non-errored cells, and cells that have never run.
-   **Only captures errors from cells run on or after April 28, 2026.** Errors from before that date return empty.
-   **Error message text is not guaranteed to be stable** across Clay releases. If you need to branch on error *type* (not message text), use `Clay.getCellStatus()` instead for more reliable conditional logic.

There is no `getCellErrorMessage()` function — the full un-truncated error message is not available in formulas. The 300-character preview is the only error message content accessible via formula.

### **What does `Clay.getCellStatus()` return?**

Use `Clay.getCellStatus()` in a formula column to read the current processing status of any enrichment (action) column:

```javascript
Clay.getCellStatus({{Column Name}})
```

This returns a string representing the cell's current state. Possible values include:

-   **Success**: `"SUCCESS"` (data returned), `"SUCCESS_NO_DATA"` (ran successfully but returned no data), `"SUCCESS_BLOCKED_DATA"`
-   **In progress**: `"RETRY"` (actively retrying — shown as "Retrying…" in the UI), `"QUEUED"`, `"RUNNING"`, `"RATE_LIMITED"`, `"AWAITING_CALLBACK"`
-   **Error**: `"ERROR"` and error-specific variants such as `"ERROR_TIMEOUT"`, `"ERROR_NUMBER_OF_RETRIES_EXCEEDED"`
-   `"UNKNOWN"` when no status has been recorded for that cell yet

A few important notes:

-   **The formula preview sidebar will show nothing** — this is expected. `Clay.*` functions are evaluated on the backend and cannot run in the preview. Save the column and the values will populate.
-   **Only works for enrichment (action) columns.** The function reads the cell's stored status; it returns `"UNKNOWN"` for formula columns or cells that have never run.
-   The function reflects the cell's **current** status — including in-progress states. A cell actively retrying returns `"RETRY"`, a cell waiting to execute returns `"QUEUED"`.

### **Why does my regex formula work in the preview but fail when the table runs?**

Clay's backend formula engine uses [RE2](https://github.com/google/re2/wiki/Syntax) for regex evaluation. RE2 is designed for fast, predictable matching but **does not support lookaheads or lookbehinds** — patterns like `(?=...)`, `(?!...)`, `(?<=...)`, and `(?<!...)`. The formula preview runs in the browser using native JavaScript regex, which *does* support these constructs.

This means a formula containing a lookahead can appear correct in the preview but produce no output (or fail silently) when the table actually runs.

**Workaround:** Rewrite the regex to avoid lookahead and lookbehind assertions. For example, to strip a subaddress tag before the `@` in an email:

-   ❌ Uses lookahead (fails at runtime): `{{Email}}?.replace(/(+.*)(?=@)/, "")`
-   ✅ Equivalent without lookahead (works): `{{Email}}?.replace(/\+.*@/, "@")`

Always verify regex formulas by saving the column and checking actual table results — not just the preview.

### **Why does my formula return 0 when combining values from other formula columns?**

If a formula that sums or combines values from other columns shows 0 in the preview even though those columns contain data, the formula may not be resolving the column references you intended.

The most reliable fix is to use the `/` column picker when writing your prompt:

1.  In the Formula Generator prompt, type `/` to open a dropdown listing all columns in your table.
2.  Select the column you want to reference. This inserts an exact column token rather than a typed name.
3.  Click **Regenerate** to update the formula with the explicit references.

Using the `/` picker guarantees the formula targets the exact column, which is especially helpful when column names are similar (for example, "Activity Score" vs. "Activity Type Score") or when combining the output of several formula columns into a final score.
