---
title: Monitor for new hire
description: Track new hires signals and act on timely data.
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
