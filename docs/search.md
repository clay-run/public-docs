---
title: Search (Beta)
description: Build precise searches across companies, people, and jobs in a single query, and save any search as an always-on Audience.
last_synced: 2026-07-28T16:52:01.482Z
---

# Search (Beta)

Find your ideal customers in one search across companies, people, and jobs — as a one-time list or an always-on Audience.

Clay's Search lets you describe your entire ICP in a single query — across companies, the people inside them, and the jobs they're hiring for — instead of pulling a broad list and enriching every row just to filter it down. This guide covers what Search does and how to run your first one.

**Note:** Search is in open beta ahead of general availability. Opt in by navigating to `Find leads` and clicking the settings gear to toggle on the new experience.

**What you can do with Search:**

-   **Search across companies, people, and jobs in one query** — layer criteria about a company, the people who work there, and the roles it's hiring for into a single search (for example, companies hiring 5+ engineers where there's already a Head of RevOps). Results are deterministic, drawn from Clay's data of 900M people, 70M companies, and 300M jobs.
-   **Build a search three ways** — describe what you want in plain language and let Sculptor set up the filters, build and refine filters yourself in the `Filters` panel, or generate the query with Clay's search language in an AI tool like Claude Code, Cursor, or Codex (using the `Agent skill` download) and paste it in.
-   **Turn any search into an always-on list** — save a search as an Audience and Clay keeps feeding in new records as they match, automatically deduped against what you already have.

## Running your first search

1.  **Start a search.** From the Clay homepage, click the `Find leads` card and choose `People` or `Companies` depending on what you want your list to be. (You can also start from inside a workbook: click `+ Add` and choose `Find people` or `Find companies`. Either way, you pick the list type up front, then layer in criteria about the other entities as filters.)
2.  **Describe what you're looking for.** Under `Start your search`, type your ICP into the `I'm looking for…` box (for example, B2B SaaS companies in EMEA with 50+ engineers and open SDR roles). Sculptor turns it into structured filters and highlights each change so you can see exactly what it set up.
3.  **Refine in the `Filters` panel.** Use the `Editor` toggle to add or adjust criteria with `Add filter`, including cross-entity criteria — on a companies search, filter on the people who work there and the roles they're hiring for; on a people search, filter on company attributes like size, location, and tech stack. Switch to `Query` to see and edit the underlying query in Clay's search language. (To skip the plain-language step and build from scratch instead, click `Build with filters instead` before you describe anything.)
4.  **Narrow and dedupe (optional).** Use `Target companies` to scope a people search to a specific set of accounts, and `Excluded people` / `Excluded companies` to exclude records already in an existing Audience.
5.  **Pull or save your list.** Click `Continue`, then either save to a table (`Save to new workbook and table` if you started from the homepage, or `Save to new table` / `Save to existing table` from inside a workbook) for a one-time pull, or save it as an Audience (`Save to People` / `Save to Companies`) to make it an always-on list that refreshes as new records match. Audience results land in draft first, with new and existing records shown side by side so you can qualify them before they sync anywhere — or turn on auto-save to move matches straight into `All companies` / `All people`.

## FAQs

### Does Search cost extra to run?

Filtering doesn't cost credits, and the core data points that come back with your results are included. You only pay credits for additional data you choose to enrich — so building a precise list in one search means you aren't paying to enrich rows you'll filter out anyway.

### Which plans include Search?

Search is available across all Clay plans. Cross-entity filters — combining company, people, and job criteria in one query — are included on paid plans, both legacy and modern.

### Can I save any search as an Audience?

Yes — both People and Companies searches can be saved as an Audience for always-on sourcing. Search covers people and companies during open beta; if you need job postings themselves as your list, use the classic filter experience instead. You can still filter on a company's job postings inside a Companies search.

### What's still coming during the beta?

Sculptor can't yet start a search from a job description or a professional profile URL — describe your ICP in plain language instead. In a People search you also can't filter on a company's job postings or its other employees yet; run those as a Companies search.
