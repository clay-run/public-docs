---
title: Monitor for new hire
description: Track new hires signals and act on timely data, and see each new hire's name, job title, and LinkedIn URL.
last_synced: 2026-04-26T01:40:24.407Z
---

# Monitor for new hire

Track new hires signals and act on timely data.

New hire Signals track recently hired employees at target companies within the last three months. You can set specific filters to monitor the most relevant new hires at these accounts.

Monitoring new hires is beneficial because they:

-   Often make key purchasing decisions in their first 90 days, creating prime opportunities for conversion.
-   Can also indicate department growth and increased budgets.

**_Cost:_** _Each check consumes 1 action plus 0.2 data credits._

## Monitoring for new hires

To set up new hires Signals in your table:

1.  Click `Tools`, then select `Monitor for new hires`.
2.  Select your company table and identify the correct company identifiers (website, LinkedIn URL).
3.  Configure your filters to specify which new hires you want to track (job titles, experience, etc.)
4.  Set how often the Signal should run.
5.  Optionally, add enrichments to gather additional data about new hires.
6.  Optionally, `Add sample results`.
    -   This lets you preview how the data will appear after any changes actually happen.
7.  Click `Save and run X rows` to finish.

**Need regular data updates instead of specific change monitoring through Signals?** Check out [scheduled columns](https://www.clay.com/university/guide/scheduled-columns) and [scheduled sources](https://www.clay.com/university/guide/scheduled-sources).

## Where to see who was hired: name, job title, and LinkedIn URL

After a New hire signal runs, you can see which person was hired, their job title, and their LinkedIn URL. Where to find them depends on whether you set the New hire signal up on a table or on an Audience.

### New hire signal on a table

A table-based New hire signal adds each detected new hire as its own row in the signal's results table. By default, the results table has these columns:

-   `Event: New hire`: the signal column (📡 icon). It holds the full event details for the hire.
-   `Company Record`: links the hire back to the company row in the company table you monitor.
-   `Company Name`: the company the person was hired at.
-   `Person LinkedIn Profile`: the new hire's LinkedIn URL.

The new hire's name and job title don't get their own columns by default. To see them:

1.  Click a cell in the `Event: New hire` column to expand the event details.
2.  Expand the `fullProfile` object. It contains the hire's `name`, job title (`latest_experience_title`), start date (`latest_experience_start_date`), and location (`location_name`).
3.  To turn a value into a column, hover over it (for example, `name` or `latest_experience_title`) and click `Add to column`, or double-click the value. The value then shows up as its own column for every new hire row.

### New Hire signal on a Companies audience

When you add the New Hire signal to a Companies audience (**Enrich** → **Signals** → **New Hire**), it writes to a signal column on each company record. The column is labeled with your lookback window, for example `New hire (90d)`, and shows how many new hires were detected. Its sub-columns show the most recent hire at that company:

-   `New hire title`
-   `New hire LinkedIn URL`
-   `Location`

The company record doesn't show the new hire's name. To see the results for every company in one place:

1.  Open the Companies audience.
2.  Click the `Signals` button in the top-right header.
3.  On the New Hire signal card, click `View results`. The results list each company's `Name` (the company name), `Domain`, `Occurrences` (the hire count, for example `Occurrences (90d)`), `New hire title`, `New hire LinkedIn URL`, and `Location`.

To see every new hire as an individual person, including their name, use either of these:

-   **The New hires segment:** Clay automatically creates a draft People segment named **New hires**, pinned at the top of the Audiences left sidebar. Each record in it is one new hire.
-   **A workflow with the "On a signal" trigger:** the workflow runs once per new hire. The trigger output includes `New Hire LinkedIn URL` and a `Full Profile` object with the hire's name, job title, location, and start date. See [Signals](signals.md) for setup steps.

## People Filters

The **People Filters** section controls which new hires get added to your table. Clay only adds a new row when a hire matches all of your active filters.

### Job title match mode

The **Job title** filter lets you specify job title keywords and how they're matched against a hire's title. Use the dropdown next to the field to select a match mode:

-   **Is similar to** _(default)_ — uses AI-powered expansion to find synonyms and equivalent role names. For example, "CEO" also matches "Chief Executive Officer." Best for broad coverage with minimal setup.
-   **Contains** — returns hires whose title contains your keyword phrase as a whole-word match. "Engineer" matches "Software Engineer" and "Senior Engineer" but not "Engineering Manager" or "Engineering Tech." More precise than "is similar to."
-   **Is exactly** — returns only hires whose title exactly matches one of your keywords. Use this only when you need very precise title filtering.

> **Tip:** The job title field accepts any text you type — it is not limited to the suggestions shown while you type. Type any keyword (for example, "AI Specialist" or "VP Sales") and press Enter, or select the **Create "[your text]"** option that appears, to add it as a filter. You can add multiple custom keywords this way.

> **Getting zero results despite a valid search?** If your Signal returns no results but a LinkedIn Sales Navigator search for the same companies and titles returns results, check your Job title match mode. Setting it to **Is exactly** means only hires whose title is an exact, character-for-character match will be included. Switch to **Contains** or the default **Is similar to** for broader matching similar to how Sales Navigator works.

### Job titles to exclude

The **Job titles to exclude** field removes hires whose title contains any of your listed keywords as a whole word. For example, adding "Analyst" will exclude "Data Analyst", "Financial Analyst", and "Business Analyst" — any title where "Analyst" appears as a complete word.

Note that the match is word-level, not character-level: adding "Engineer" will exclude "Software Engineer" and "Senior Engineer", but will **not** exclude "Engineering Manager" or "Engineering Tech" (because "engineering" is a different word from "engineer"). To exclude titles containing "engineering", add "engineering" as a separate keyword.
