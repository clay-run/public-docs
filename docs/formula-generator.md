---
title: Formulas
source_url: https://university.clay.com/docs/formula-generator
description: Generate formulas with AI to transform your data. Includes how to
  use today's date in a formula and keep date comparisons current automatically.
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

### **Why does my formula column show stale or greyed-out output even though upstream columns have data?**

When an upstream enrichment column reruns and updates its output, Clay marks any formula referencing it as out of date — even if you just ran the formula. This is expected behavior: the stale indicator means the formula hasn't re-evaluated against the latest data yet.

To refresh the formula output:

-   **With Auto-run on**: The formula re-evaluates automatically as soon as the upstream column finishes. If it hasn't updated, verify that the formula column's own Auto-run toggle is also enabled.
-   **With Auto-run off**: Right-click the formula column header → **Run column** → **Run N empty or out-of-date rows** to manually trigger a recalculation.

If the formula keeps showing as stale in a loop, an upstream column may have Auto-run enabled and be continuously refreshing its output, which re-marks the formula as out of date each time. See [Table management settings](table-management-settings.md) for strategies to break the cascade (such as disabling Auto-run on the upstream column or enabling "Keep existing results" at the table level).

### **My formula references a column that returns a list — how do I access individual values?**

Enrichment columns often return list-valued data (arrays of results). Standard string operations on a list won't work as expected because the value is an array, not a plain string.

To work with list data in a formula:

-   **Access the first item**: Use zero-based indexing — `{{Column}}?.[0]` returns the first item in the list, `{{Column}}?.[1]` returns the second, and so on.
-   **Convert the full list to a string**: Use `JSON.stringify({{Column}})` to get a JSON-formatted string representation. Avoid using `.toString()` on complex objects — it returns `[object Object]` instead of the actual data.
-   **Extract a property from each item**: Use `.map()` — for example, `{{Column}}?.map(item => item.name).join(', ')` extracts the `name` field from each item and joins them as a comma-separated string.

If you're unsure what structure a column's data has, click any cell in that column to open the **Cell details** panel — this shows the raw output and lets you inspect the exact shape before writing your formula.
