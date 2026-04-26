---
title: HitHorizons integration overview
source_url: https://university.clay.com/docs/hithorizons-integration-overview
description: Europe-focused company data provider.
last_synced: 2026-04-26T01:40:08.037Z
upstream_hash: 49cdf66f92b821a6b1b8d5ace8db7fc219721b42eda0b0d8d85428387746b0cf
---

# HitHorizons integration overview

Europe-focused company data provider.

### What is HitHorizons?

The HitHorizons integration in Clay gives you access to firmographic data on over 80 million European companies, including sales, employee count, industry, and location.

### Setting up HitHorizons and Clay

You can connect HitHorizons in Clay two ways.

### Option 1: Use the Clay-managed HitHorizons account

By default, HitHorizons enrichments in Clay use the Clay-managed HitHorizons account, which charges one credit for each enrichment.

To utilize this, simply open any HitHorizons enrichment within Clay.

![](https://cdn.prod.website-files.com/687e604972375496b891fe58/691e659fa43832e5c673d810_674e81591ca3b15ecc5c9a13_6731a0a0bf257dde56ebbd08_67319216d9c1ba17f3b3e983_CleanShot%252525202024-11-01%25252520at%2525252005.02.42%252525402x%25252520\(1\).png)

### Option 2: Use your own HitHorizons API key

If you are currently on a paid plan, you can use your own HitHorizons account within Clay through an API key.

To access your HitHorizons API key, head over to **My Account > My Services > API Dashboard.**

![](https://cdn.prod.website-files.com/687e604972375496b891fe58/691e659fa43832e5c673d807_674e81591ca3b15ecc5c99f2_6731a0a0bf257dde56ebbcfa_6731921eefa10fbd48c43386_CleanShot%252525202024-11-01%25252520at%2525252005.04.54%25252520\(1\).png)

You can then access your API key by selecting **API Management > Resend Key.**

![](https://cdn.prod.website-files.com/687e604972375496b891fe58/691e659fa43832e5c673d7ff_674e81591ca3b15ecc5c99ef_6731a0a0bf257dde56ebbcee_6731922fa22914011e5504c3_CleanShot%252525202024-11-01%25252520at%2525252005.07.17%25252520\(1\).png)

You can add your HitHorizons API key to Clay within the enrichment panel. The image below shows where to add your API key in the enrichment panel.

![](https://cdn.prod.website-files.com/687e604972375496b891fe58/691e659fa43832e5c673d825_674e81591ca3b15ecc5c9a0d_6731a0a0bf257dde56ebbd05_67319247ea942fb4bed038a8_CleanShot%252525202024-11-01%25252520at%2525252005.09.42%252525402x%25252520\(1\).png)

### `Action` Find EMEA Company Firmographics

The **Find EMEA Company Firmographics** helps find company sales, employee count, industry code, and location based on Government data. This integration works best when both Company Name and Country are inputted.

**Step 1: Select Find EMEA Company Firmographics**

Access this action through the integration panel.

**Step 2: Select HitHorizons Account**

Proceed with either a Clay-managed or a personal account.

![](https://cdn.prod.website-files.com/687e604972375496b891fe58/691e659fa43832e5c673d80a_674e81591ca3b15ecc5c9a32_6731a0a0bf257dde56ebbd0b_6731926c91f7134a65262fd8_CleanShot%252525202024-11-01%25252520at%2525252005.09.42%252525402x%25252520\(2\).png)

**Step 3: Input Company data**

This integration works best when both company name and country are inputted. More information will lead to better results searches.

**Step 4: Configure run settings**

Auto-update: HitHorizons will automatically enrich any new rows that get added to the table. Learn more about auto-update in this [this brief guide](https://docs.clay.com/en/articles/9642165-auto-update-and-auto-dedupe-table).

Conditional runs: To run enrichment only under specific conditions, use formulas that trigger the column when the formula is true. See [this Clay University lesson.](<https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101#:~:text=Conditional runs \(which make use,personal emails for all rows\).>)

**Step 5: Choose data to add as columns to table**

Select which data from the enrichment you’d like to add as columns to your table. Even if you choose not to add columns at this point, the enriched data will still be available and accessible for later use.
