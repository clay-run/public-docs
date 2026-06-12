---
title: Lookup Rows
source_url: https://university.clay.com/docs/lookup-rows
description: Bring in data into your table from other tables.
last_synced: 2026-04-26T01:40:17.543Z
---

# Lookup Rows

Bring in data into your table from other tables.

The Lookup Rows feature allows you to search and retrieve data from other tables in your workspace, enabling connections between tables and filtering data based on specific criteria.

Whether you need a single row or multiple matching records, these lookup actions provide flexible options to enhance your data management and create more dynamic, interconnected workflows.

**Cost:** Lookup Rows does not consume Actions or Data Credits — these lookups read data that already exists in your Clay workspace with no external data fetching involved.

### When to use Lookup Rows vs. Send Table Data

Both Lookup Rows and Send Table Data move information between tables, but they work in opposite directions and serve different purposes.

**Use Lookup Rows when...**

Lookup Rows **pulls** data from another table into your current table based on matching criteria. It's non-destructive and doesn't modify the source table.

-   You need to **enrich your current table** with data that already exists in another table
-   You want to **check if a record exists** in another table without modifying anything
-   You need to **count or aggregate** rows that share a trait (e.g., how many people work at each company)
-   You want to **reference** data from a central table (like a pricing list, messaging library, or Do Not Contact list)
-   You're working with **static reference data** that multiple tables need to access

[**Learn more about Lookup Rows →**](https://university.clay.com/docs/lookup-rows)

**Use Send Table Data when...**

Send Table Data **pushes** data from your current table into another table. It creates or updates rows in the destination table.

-   You need to **route or segment** your data into different tables based on logic or filters
-   You want to **flatten lists** into individual rows (e.g., turn a list of 5 people into 5 separate rows)
-   You need to **merge data** from several tables into one consolidated table
-   You want to **separate concerns** across multiple tables (e.g., companies in one table, people in another)
-   You're building **multi-stage workflows** where each table handles a specific step in your process

[**Learn more about Send Table Data →**](https://university.clay.com/docs/send-table-data)

### **Using `Lookup single row in other table`**

1.  Identify a shared value to compare between the two tables (e.g., company URL, email address, or other value two rows might share).
2.  Normalize your key if needed (e.g. extract the domain from an email into a `Domain` column).
3.  Add the `Lookup single row` action in the table you want to enrich.
4.  Configure the lookup:
    -   `Table to search` — the table you're checking against to look for matches
    -   `Target column` — the column to match on in that table
    -   `Filter operator` — how to compare the values (strict `Equals` or flexible `Contains`)
    -   `Row value` — the value you're looking for
5.  Run the lookup.
6.  Review results to see whether matches were found.

**Common use cases**

-   Pull company attributes into a people table (name, revenue, industry, etc.)
-   Pull people attributes into a company table (e.g., key contacts/leaders)
-   Re-use standard messaging stored in a central table
-   Check against a static reference database, like a list of users
-   Check a Do Not Contact list or verify whether a record has already been enriched, then branch actions based on yes/no
-   Validate that a contact's email domain matches their company's domain — use a formula column to extract the domain from an enriched email address, then look it up against a table of company-level domains

**Best practices**

-   For readability, when a result is found you can promote returned fields into their own columns (select a returned value → `Create column for it`)
-   Match on stable, unique identifiers (e.g., a URL is often better than a company name)
-   Clean and normalize both sides of the match key (trim, lowercase, consistent formatting)
-   **Ensure the target column type matches your lookup value**: If the `Target column` in the reference table is **Number** type but your `Row value` contains non-numeric text (such as an ID with letters, a dash, a blank, or "N/A"), the lookup may return unexpected results or show a type mismatch error. To fix this, change the target column to **Text** type in the reference table.
-   Use single row lookup instead of multiple row lookup when you only need one result — it's faster
-   If an expected field isn't visible in the result panel, the matched row in the source table likely has an empty value for that field — the panel only shows fields that have a value for the specific matched row. To add that column anyway, find a row whose matched source record has the field populated, open that lookup cell, and click **Add as column**.
-   **Lookup not auto-running for new rows?** If the **Row Value** is a static string with no column reference (no `/` pick), Clay sees no upstream dependency and won't trigger the column when new rows are added. Fix: in **Run settings → Only run if**, add a condition that references an upstream column — for example, `/[Your source column] is present`. This creates the dependency Clay needs to fire the lookup automatically for each incoming row.

### **Using `Lookup multiple rows in other table`**

1.  Identify a shared value to compare between the two tables (e.g., company URL, email address, or other value two rows might share).
2.  Normalize your key if needed (e.g. extract the domain from an email into a `Domain` column).
3.  Add the `Lookup multiple rows` action in the table you want to enrich.
4.  Configure the lookup:
    -   `Table to search` — the table you're checking against to look for matches
    -   `Target column` — the column to match on in that table
    -   `Filter operator` — how to compare the values (strict `Equals` or flexible `Contains`)
    -   `Row value` — the value you're looking for
    -   `Limit (Optional)` — set max number of rows to return per row. The maximum is **100** (hard limit — values above 100 are ignored). Defaults to 100 if left blank. Use a lower value to reduce response size when you have many columns.
5.  Run the lookup.
6.  Review results:
    -   Each row returns a count of matches
    -   The cell also shows a sample list (up to 10) matched rows you can click into
7.  Optional: Break matches into separate columns using `Add as column` (e.g., pull the first 1–2 matched records/fields into dedicated columns)

**Common use cases**

-   Count related records (e.g., how many people map to each company)
-   Detect interest/volume (e.g., multiple inbound form submissions tied to one company)
-   Trigger follow-ups based on count (e.g., 0 → run a "find people" search; 3+ → prioritize outreach)

**Best practices**

-   **Match on domain, not company name**: Company names vary across tables (e.g., "Zoom" vs "Zoom Video Communications"), so using company name as the match key often returns unexpectedly low counts — sometimes just 1 match per company even when many records exist. Use a company domain (e.g., `zoom.us`) as your match key on both sides for accurate, reliable counts.
-   **Ensure the target column type matches your lookup value**: A **Number**-type target column cannot match non-numeric text — matching a Number-type column against text values (IDs with letters, dashes, blanks, or "N/A") may return unexpected results or show a type mismatch error. Change the target column to **Text** type when your lookup values are text identifiers.
-   Remember the UI shows up to 10 matches, but the count reflects all matches found
-   Only use `Add as column` for the few results you actually need to avoid clutter and keep tables readable
-   **100-record cap**: Lookup multiple rows returns at most 100 records per row — this is a hard limit that cannot be changed. If your source table has more than 100 matching records, only the first 100 are returned. To work around this, split the source table into smaller segments (e.g., by category, region, or product line), create a separate lookup column per segment, and merge the results in a formula or AI prompt. Each segment lookup stays under 100 records while the AI prompt still gets the full set.
-   Use the lookup result as a gate to control downstream actions (enrich/send/route only when criteria are met) — for a step-by-step example using a run condition, see [Conditional runs](conditional-runs.md).
-   **Lookup not auto-running for new rows?** If the **Row Value** is a static string with no column reference (no `/` pick), Clay sees no upstream dependency and won't trigger the column when new rows are added. Fix: in **Run settings → Only run if**, add a condition that references an upstream column — for example, `/[Your source column] is present`. This creates the dependency Clay needs to fire the lookup automatically for each incoming row.

### **Using lookups in the same table**

You can also use `Lookup multiple rows` within the same table to find duplicates, count related records, or group rows by shared traits.

1.  Decide what you're trying to group/dedupe by.
2.  Create a shared match key column in the table.
3.  Add the `Lookup multiple rows` action on the table.
4.  Set `Table to search` to the same table you're enriching.
5.  Set `Target column to search` to your match key (e.g. email domain) and match it to the current row's match key.
6.  Run the action to return a count + list of matching rows for each record.
7.  Click into the result cell to view the matched rows and their details.

**Common use cases**

-   Detect duplicates or repeat submissions (e.g., multiple form fills from the same company)
-   Count related records inside one table (e.g., "how many people share this domain?")
-   Prevent duplicate enrichment (e.g., only enrich a company the first time it appears; skip repeats)
-   Consolidate paired or related rows (e.g., pull a duplicate account's ID or attributes into the master record row) — run a self-lookup on the shared group key (such as a duplicate set number or shared parent ID) to find all rows in the group, then use `Add as column` or a formula column to extract the specific fields you need from the matched rows

**Best practices**

-   Use a clean, consistent match key (domain is usually more reliable than company name)
-   Remember a self-lookup will usually match the row to itself—account for that when interpreting counts (e.g., "other matches" vs "total matches")
-   Use the lookup result as a gate to control downstream actions (enrich/send/route only when criteria are met)

### **Timing considerations in multi-step workflows**

A lookup reads the target table at the exact moment it runs — it doesn't wait for other enrichments to finish and has no awareness of in-progress steps elsewhere. If your workflow populates a table in one step and then immediately looks up that same table in a dependent step, the lookup can execute before the first step has finished adding rows. When that happens, the lookup returns no results even though matching records will exist shortly.

**Symptoms to watch for:**

-   The lookup returns no results (or fewer results than expected) for some rows, but manually re-running the same cells later finds records.
-   Adding a delay between steps reduces failures but doesn't eliminate them entirely — results are inconsistent row to row.

**Why re-runs work:** By the time you manually re-run the cell, the other step has finished populating the table, so the lookup finds the records it missed the first time.

**Why delays help but aren't fully reliable:** A delay gives the other step more time to finish, but enrichment timing varies per row — some records complete in seconds, others take longer. A fixed delay that works for most rows can still fail for the slowest ones.

**Ways to make it more reliable (most to least effective):**

-   **Remove the cross-table dependency:** Run the enrichment (e.g., a "Find People at Company" action) directly in the same table where you need the results, rather than populating a separate people table and then looking it up. This eliminates the timing dependency entirely and is the most reliable fix.
-   **Restructure to a sequential flow:** Make sure the source table fully finishes running before the dependent table reads from it. For scheduled tables, offset the second table's schedule by enough time for the first to complete — see [Custom signals](custom-signals.md) for an example of staggering table schedules.
-   **Use a scheduled lookup:** A table run on a schedule reads other tables that have already completed their prior runs, so it is less susceptible to this issue than a lookup triggered in real time alongside an in-progress enrichment.
-   **Add a delay:** Insert a delay column before the lookup (up to 600 seconds). This reduces failures but does not guarantee they disappear, since enrichment time varies per row.
