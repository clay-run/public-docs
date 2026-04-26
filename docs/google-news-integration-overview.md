---
title: Google News integration
source_url: https://university.clay.com/docs/google-news-integration-overview
description: News aggregator delivering current events and information.
last_synced: 2026-04-26T01:40:03.783Z
upstream_hash: 4d8dd6842dbf854fe7fc1993e5bfe832427abc6d934b7cf7e66c7f2c373235f8
---

# Google News integration

News aggregator delivering current events and information.

## Google News Overview

Google News in Clay allows users to find news results for a given query.

## **Available Actions with the Google News Integration**

### `Action` Find News Results

Given a query find results from Google News.

**Step 1:** Enter search query.

Provide the query you want to search for. You can input plain text directly or reference data from other columns to dynamically generate the query.

**Step 2 (Optional):** Specify the language for the search.

If no language is provided, the search will default to English.

**Step 3 (Optional):** Filter news results by date, selecting a range from the past hour to the past year.

**Step 4:** Configure run settings.

By default, new rows within your Clay table will automatically run the Google News action. Learn more about auto-update in [this brief guide](https://docs.clay.com/en/articles/9642165-auto-update-and-auto-dedupe-table).

To run enrichment only under specific conditions, use formulas that trigger the column when the formula is true. Learn more about AI formulas in [this Clay University lesson](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101).

**Step 5:** Run your enrichment to find results from Google News.
