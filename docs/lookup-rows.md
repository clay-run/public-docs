---
title: Lookup Rows
source_url: https://university.clay.com/docs/lookup-rows
description: Bring in data into your table from other tables.
last_synced: 2026-04-26T01:40:17.543Z
upstream_hash: ff318cbcf26791335e4b07e1243d68d75de2fa86bb0381920a1076d893b42243
---

# Lookup Rows

Bring in data into your table from other tables.

The Lookup Rows feature allows you to search and retrieve data from other tables in your workspace, enabling connections between tables and filtering data based on specific criteria.

Whether you need a single row or multiple matching records, these lookup actions provide flexible options to enhance your data management and create more dynamic, interconnected workflows.

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

**Best practices**

-   For readability, when a result is found you can promote returned fields into their own columns (select a returned value → `Create column for it`)
-   Match on stable, unique identifiers (e.g., a URL is often better than a company name)
-   Clean and normalize both sides of the match key (trim, lowercase, consistent formatting)
-   Use single row lookup instead of multiple row lookup when you only need one result — it's faster

### **Using `Lookup multiple rows in other table`**

1.  Identify a shared value to compare between the two tables (e.g., company URL, email address, or other value two rows might share).
2.  Normalize your key if needed (e.g. extract the domain from an email into a `Domain` column).
3.  Add the `Lookup multiple rows` action in the table you want to enrich.
4.  Configure the lookup:
    -   `Table to search` — the table you're checking against to look for matches
    -   `Target column` — the column to match on in that table
    -   `Filter operator` — how to compare the values (strict `Equals` or flexible `Contains`)
    -   `Row value` — the value you're looking for
    -   `Limit (Optional)` — set max number of rows to return (useful to cut down on response size if you have large numbers of columns)
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

-   Match on clean, normalized identifiers (domain/email domain beats company name)
-   Remember the UI shows up to 10 matches, but the count reflects all matches found
-   Only use `Add as column` for the few results you actually need to avoid clutter and keep tables readable

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

**Best practices**

-   Use a clean, consistent match key (domain is usually more reliable than company name)
-   Remember a self-lookup will usually match the row to itself—account for that when interpreting counts (e.g., "other matches" vs "total matches")
-   Use the lookup result as a gate to control downstream actions (enrich/send/route only when criteria are met)
