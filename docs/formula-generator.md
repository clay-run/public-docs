---
title: Formulas
source_url: https://university.clay.com/docs/formula-generator
description: Generate formulas with AI to transform your data.
last_synced: 2026-04-26T01:40:01.109Z
upstream_hash: 30a9dfa01dd9c6fff8f8a3a0ff6805b1416bad474e318943a2d533010c6b832f
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
