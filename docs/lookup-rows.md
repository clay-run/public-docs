---
title: Lookup Rows
description: Bring in data into your table from other tables.
last_synced: 2026-04-26T01:40:17.543Z
---

# Lookup Rows

Bring in data into your table from other tables — similar to VLOOKUP or INDEX-MATCH in a spreadsheet.

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
-   Exclude contacts that already exist in a CRM or other reference table — see the [view filter exclusion pattern](#excluding-contacts-that-exist-in-another-table-view-filter-pattern) below
-   Validate that a contact's email domain matches their company's domain — use a formula column to extract the domain from an enriched email address, then look it up against a table of company-level domains
-   **Prevent duplicate outreach across teammates with separate tables** — When multiple teammates each manage their own lead table in the same workspace, add a Lookup Single Row column pointing to a co-worker's table and match on email address or professional profile URL. If the lookup finds a match, that lead already exists in the other table — add a [conditional run](conditional-runs.md) to skip outreach for those rows. All tables in a workspace are visible to every workspace member, so no special sharing step is needed.

**Best practices**

-   For readability, when a result is found you can promote returned fields into their own columns (select a returned value → `Create column for it`)
-   Match on stable, unique identifiers (e.g., a URL is often better than a company name)
-   **When pulling row-specific data, match on a field that's unique per row**: A company-level field like domain is stable but not unique per person — if multiple rows in the source table share the same domain, the lookup returns whichever row it finds first, and every contact at that company gets the same result. When the data you're pulling should vary per person (e.g., personalized email copy, individual contact records), use a person-level unique identifier such as email address or professional profile URL as the match key instead.
-   Clean and normalize both sides of the match key (trim, lowercase, consistent formatting)
-   **If expected matches aren't found, try switching to `Contains`**: The `Equals` operator requires an exact character-for-character match — minor discrepancies in spacing, casing, or formatting between the Row Value and the target column will cause it to miss valid records. Switching the Filter Operator to `Contains` is a useful diagnostic: if it finds records that `Equals` missed, normalize the upstream data so both sides match exactly, then switch back to `Equals` for precision.
-   **Avoid Number-type columns as lookup keys — convert to text first**: A **Number**-type `Target column` produces unreliable results. Depending on cache state, the lookup may return "No Record Found" even when identical values exist in both tables, or silently return a wrong row when the `Row value` cannot be parsed as a number. **Workaround:** In both tables, add a formula column that converts the number to a text string — for example, `String({{Clay Company Id}})` — then configure your lookup to match on those text columns instead of the number columns directly.
-   **Checking whether a lookup found a match — use `== null` in formulas and run conditions**: When a Lookup Single Row column finds no matching record, the cell stores `null` — the "No Record Found" label you see in the table is a display indicator, not the stored value. Comparing against the string `"No Record Found"` in a formula always fails because the actual stored value is `null`. Use `== null` to test for no match and `!= null` to test for a match. For example, to label rows as "Unique" or "Duplicate" based on whether any of three lookup columns found a match: `({{Table 2}} == null && {{Table 3}} == null && {{Table 4}} == null) ? "Unique" : "Duplicate"`. The same expression works as a **Run settings → Only run if** condition to skip enrichment for rows that already exist in any of those tables.
-   Use single row lookup instead of multiple row lookup when you only need one result — it's faster
-   If an expected field isn't visible in the result panel, the matched row in the source table likely has an empty value for that field — the panel only shows fields that have a value for the specific matched row. To add that column anyway, find a row whose matched source record has the field populated, open that lookup cell, and click **Add as column**.
-   **Lookup not auto-running for new rows?** If the **Row Value** is a static string with no column reference (no `/` pick), Clay sees no upstream dependency and won't trigger the column when new rows are added. Fix: in **Run settings → Only run if**, add a condition that references an upstream column — for example, `/[Your source column] is present`. This creates the dependency Clay needs to fire the lookup automatically for each incoming row.

### **Excluding contacts that exist in another table (view filter pattern)**

When you want to work only with contacts that are **not** already in a reference table — for example, contacts whose company is not among your active CRM deals — use a lookup with a view filter:

1. **Set up a reference table** containing the records you want to exclude. If your data lives in an external system (e.g., a CRM), export it as a CSV and import it into a new Clay table via **Tools → Import → Import from CSV**. Make sure the reference table has a stable identifier column, such as company domain.

2. In your working table, add a **Lookup single row in other table** column and configure it:
   - `Table to search` → your reference table
   - `Target column` → the identifier column in the reference table (e.g., company domain)
   - `Filter operator` → `Equals`
   - `Row value` → the matching column from your current table (e.g., company domain)

   When the lookup finds a match, the cell shows the matched record. When it finds no match, the cell shows **No Record Found**.

3. Add a **view filter**: click the **Filter** button (funnel icon) in the table toolbar, select your lookup column, and set the operator to **has no results**.

   This shows only rows where the lookup returned no match — contacts whose company is **not** in your reference table. Rows that matched are hidden from the view but remain stored in the table; removing the filter brings them back.

**Why company domain works better than company name for matching:** Names like "Acme" and "Acme Corp" won't match with `Equals` even though they refer to the same company. Domain (e.g., `acme.com`) is stable and consistent across data sources, making it a much more reliable match key.

**Using the result beyond the view:** If you need to enrich or route only the non-matching rows rather than just filter the display, you can gate downstream column runs on the lookup result. See the `== null` note in the best practices above, and [Conditional runs](conditional-runs.md) for how to set up a run condition.

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
-   Use lookup results as input for an AI column — pull matching records from another table with Lookup Multiple Rows (e.g., your existing clients matched by a shared attribute like industry), then reference those results in a Use AI column prompt to compare, rank, or identify the best match (e.g., find the most similar existing client to use as social proof in outreach)

**Best practices**

-   **One filter column only**: The lookup matches on a single `Target column` at a time — you cannot apply multiple columns as simultaneous filter criteria. To filter by multiple attributes at once (for example, domain and industry), create a formula column in both tables that combines those values into a single string (for example, `{{Domain}} + "-" + {{Industry}}`), then use that combined column as your match key.
-   **Match on domain, not company name**: Company names vary across tables (e.g., "Zoom" vs "Zoom Video Communications"), so using company name as the match key often returns unexpectedly low counts — sometimes just 1 match per company even when many records exist. Use a company domain (e.g., `zoom.us`) as your match key on both sides for accurate, reliable counts.
-   **Avoid Number-type columns as lookup keys — convert to text first**: A **Number**-type `Target column` produces unreliable results. The lookup may return no matches even when identical values exist in both tables, or silently return incorrect rows when the `Row value` input cannot be parsed as a number. **Workaround:** In both tables, add a formula column that converts the number to a text string — for example, `String({{Clay Company Id}})` — then match on those text columns instead.
-   Remember the UI shows up to 10 matches, but the count reflects all matches found
-   Only use `Add as column` for the few results you actually need to avoid clutter and keep tables readable
-   **100-record cap**: Lookup multiple rows returns at most 100 records per row — this is a hard limit that cannot be changed. If your source table has more than 100 matching records, only the first 100 are returned. To work around this, split the source table into smaller segments (e.g., by category, region, or product line), create a separate lookup column per segment, and merge the results in a formula or AI prompt. Each segment lookup stays under 100 records while the AI prompt still gets the full set.
-   **"Cell data size exceeds limit (200 kB)":** Lookup Multiple Rows results are stored in action columns with a hard 200 kB output limit — separate from the 100-record cap. Even when the lookup returns exactly 100 records, this error can appear if those records have densely populated fields (few blank values): 100 fully populated records produce a larger payload than 100 sparse ones. To fix this, lower the **Limit** setting in the column configuration (default 100, max 100) to a smaller value — fewer records returned means a smaller payload. See [Cell size limits](manage-cell-data.md#cell-size-limits) for the full list of affected column types.
-   Use the lookup result as a gate to control downstream actions (enrich/send/route only when criteria are met) — for a step-by-step example using a run condition, see [Conditional runs](conditional-runs.md).
-   **Lookup not auto-running for new rows?** If the **Row Value** is a static string with no column reference (no `/` pick), Clay sees no upstream dependency and won't trigger the column when new rows are added. Fix: in **Run settings → Only run if**, add a condition that references an upstream column — for example, `/[Your source column] is present`. This creates the dependency Clay needs to fire the lookup automatically for each incoming row.

**Example: Automatically find new contacts when an account is under-covered**

When prospecting existing accounts, contacts can leave a company, change roles, or opt out of email — leaving you without enough active prospects to reach. To automatically trigger a fresh contact search for any account that falls below a coverage threshold:

1. In your account-level table (one row per account), add a **Lookup Multiple Rows in Other Table** column:
   - `Table to search` → your prospects table
   - `Target column` → the company domain column in your prospects table
   - `Filter operator` → `Equals`
   - `Row value` → the company domain column in this table

   This column returns a count of how many prospects you currently have on file for each account.

2. Add a **Find People** enrichment column. Open its **Run settings → Only run if** and set the condition:

   `/Prospects Count < 2`

   Find People now only fires for accounts where you have fewer than 2 prospects on file. (Clay automatically ensures the lookup runs before this condition is evaluated — column order in the table does not matter.)

3. To avoid returning contacts who are already in your prospects table, open the Find People source configuration and add your prospects table to the **Exclude people** filter. Exclusions match by LinkedIn URL or email, so your prospects table must contain a LinkedIn URL or email column for this to work. See [Find People in Clay](find-people-overview.md) for details.

4. Add a **Send Table Data → Send row for each item in a list** column and point it at your prospects table. Each contact returned by Find People becomes a new row in your prospects table, where they flow into your existing enrichment and sequencing workflow.

**Scaling to multiple workbooks**: Save the lookup and coverage-check logic as a [Function](functions.md). Define the company domain as the input and the coverage count as the output, then call that function from any account table without rebuilding the lookup each time.

### **Using lookups in the same table**

You can also use `Lookup multiple rows` within the same table to find duplicates, count related records, or group rows by shared traits.

**Self-lookups don't work inside a Clay function.** When you add steps inside a function, the function runs in a background table that is not a regular workspace table — it won't appear in the "Table to search" picker. This means the Lookup multiple rows action inside a function can't search the function's own rows. If you need cross-row context (such as a duplicate count) inside a function, use the workaround below: run the self-lookup in the calling table and pass the count as a function input.

**Workaround — run the lookup in the calling table and pass the result in as a function input:**

1. In the calling table (the table that invokes the function), add a **Lookup multiple rows in other table** column and set **Table to search** to the calling table itself.
2. Set **Target column** and **Row value** to your match key (e.g., Domain).
3. Run the lookup. Each row returns a count of matching rows. The lookup always includes the current row itself, so a row with a unique value returns a count of 1 — subtract 1 if you want "other matches only."
4. In the function configuration, map that count (or a formula derived from it) as a function input.
5. Reference that input inside your function logic.

**To set up a self-lookup in a regular table:**

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
-   **Prevent duplicate enrichment for shared company data** — Enrichment columns run independently per row with no awareness of sibling rows. When multiple rows share the same company (e.g., several contacts who work at the same account), each row can trigger the same company-level enrichment separately. To run the enrichment only once per company: add a **Lookup single row** (same table, matching on company domain) that checks for any other row where the company-level enrichment result is already populated. Then add a [conditional run](conditional-runs.md) to your enrichment column that fires only when the lookup finds no existing result. The first row to process writes the company data; subsequent rows with the same domain find the existing result via lookup and skip the enrichment.
-   Consolidate paired or related rows (e.g., pull a duplicate account's ID or attributes into the master record row) — run a self-lookup on the shared group key (such as a duplicate set number or shared parent ID) to find all rows in the group, then use `Add as column` or a formula column to extract the specific fields you need from the matched rows
-   **Rank or compare rows within a group** — find the highest-scoring row among rows sharing a value in a group column, or determine each row's position within its group. Add a self-lookup matched on the group column, then add a formula column that iterates over the returned records — for example, using `findIndex` to locate the current row by its Unique ID within the result list. The self-lookup always includes the current row itself, so account for that offset (position 0 = rank 1). To pick the highest scorer instead, sort the lookup by your score column and compare the first returned record's Unique ID against the current row's.

**Example: Enrich only one row per company group (without deleting duplicates)**

When a table has multiple rows sharing the same company — for example, several contacts from the same organization — each row is processed independently. Because Clay's enrichment runs at the cell level, a row has no built-in awareness of whether another row with the same company domain has already been enriched. To run a company-level enrichment (such as firmographic data or a website scrape) on just one representative row per company while leaving all contact rows intact:

1. Add a **Lookup single row in other table** column. Configure it to search the **same table** you're working in:
   - `Table to search` → this table
   - `Target column` → the company domain column
   - `Filter operator` → `Equals`
   - `Row value` → the current row's company domain column

   Because this lookup returns the **first** matching row found in the table, the result will be the same "representative" row for every contact that shares a domain.

2. Once the lookup runs, click **Add as column** on the returned `Clay Row ID` field. This creates a column (e.g., `Representative Row ID`) that contains the row ID of the first match for each domain.

3. Add a **Formula** column (e.g., `Is Representative Row`) with the expression:

   `{{Representative Row ID}} == {{Clay Row ID}}`

   This evaluates to `true` only for the row whose own ID matches the first-match ID — i.e., the representative row for that domain.

4. On the company-level enrichment column, open **Run settings → Only run if** and set the condition:

   `/Is Representative Row is true`

   The enrichment now fires only for one row per company. All other rows are skipped with **"Run condition not met"** — their contact-level data is preserved and no credits are consumed for the skipped rows.

**Best practices**

-   Use a clean, consistent match key (domain is usually more reliable than company name)
-   Remember a self-lookup will usually match the row to itself—account for that when interpreting counts (e.g., "other matches" vs "total matches")
-   Use the lookup result as a gate to control downstream actions (enrich/send/route only when criteria are met)
-   **Counts can be off when rows evaluate concurrently** — when many rows run at the same time, a self-lookup may return an inaccurate count for some rows (for example, showing 2 when the real count is 1). This happens because rows reading and writing the same table simultaneously can see partially updated data. For accurate counts after a full run, select the lookup column and click **Run column** once the table finishes processing.

### **Deduplication: cross-checking new imports against an existing leads table**

When you upload a new batch of leads and want to identify which ones already exist in another table, add multiple **Lookup single row** columns — one per identifier — and a formula column that marks each row as new or existing.

**Setup**

1.  **Enrich your new leads table** to get consistent identifiers: a professional profile URL (e.g., a social profile URL from a professional network) and a work email address. These become the match keys for your lookups.

2.  **Add one Lookup single row column per identifier**, each pointing at your existing leads table but matching on a different column:
    -   *Lookup by Profile URL* — `Table to search` → your existing leads table, `Target column` → the profile URL column, `Row value` → the profile URL from the new row
    -   *Lookup by Email* — `Table to search` → your existing leads table, `Target column` → the email column, `Row value` → the email from the new row
    -   *(Optional) Lookup by Name + Company* — in both tables, add a formula column that concatenates name and company into a single string (e.g., `{{First Name}} + " " + {{Last Name}} + " " + {{Company}}`), then add a third lookup matching on that combined column. Use this as a fallback when a profile URL or email is unavailable.

3.  **Add a Formula column** (e.g., `Is Existing Lead`) that returns `"Existing"` if any lookup found a match, or `"New"` if all lookups returned null (no match):

    `({{Lookup by Profile URL}} == null && {{Lookup by Email}} == null) ? "New" : "Existing"`

    Add additional `&&` conditions for any extra lookup columns.

4.  **Gate downstream enrichment** on this formula column. Open **Run settings → Only run if** on any enrichment column and set: `/Is Existing Lead equals "New"`. This skips enrichment for leads already in your existing table and avoids consuming credits on records you've already processed. See [Conditional runs](conditional-runs.md) for how to set this up.

**Identifier priority**

Match on the strongest identifier first:
-   **Professional profile URL** — most reliable. Unique per person and doesn't change when someone switches jobs or updates their email. Use this as your primary match key.
-   **Work email** — second-best option. Reliable for identifying a contact at their current company, but can change when someone changes employers.
-   **Name + Company** — weakest fallback. Company names are often inconsistent across datasets (e.g., "Zoom" vs. "Zoom Video Communications"). Use only when neither a profile URL nor email is available.

**Rolling log for ongoing ingestion**

If you import new leads continuously over time, use a dedicated **log table** that accumulates every lead you've already processed, instead of checking against a static snapshot:

1.  Create a separate **leads log table** with columns for the identifiers you match on (profile URL, email).
2.  In your new-leads table, point your lookup columns at this log table instead of your original leads table.
3.  Add a **Send Table Data** column that copies the new lead's identifier columns into the log table after enrichment completes. Set a [conditional run](conditional-runs.md) on this column so it only fires for rows where `Is Existing Lead equals "New"`.

Each subsequent import is automatically checked against the cumulative log. Leads processed in any previous import will be caught as `"Existing"` on every future run.

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
