---
title: BuiltWith overview
description: Web technology intelligence for sales, marketing, and market analysis.
last_synced: 2026-04-27T18:09:27.255Z
---

# BuiltWith overview

Web technology intelligence for sales, marketing, and market analysis.

## What is BuiltWith?

BuiltWith allows you to view a website's tech stack and find technologies that companies are built with.This action costs 2 credits per cell to run.

## Setting up BuiltWith and Clay

You can connect BuiltWith in Clay two ways.

### Option 1: Use the Clay-managed BuiltWith account

By default, BuiltWith enrichments in Clay use the Clay-managed BuiltWith account, which charges 2 credits for each enrichment.

To utilize this, simply open any BuiltWith enrichment within Clay.

### Option 2: Use your own BuiltWith API key

If you are currently on a paid plan, you can use your own BuiltWith account within Clay through an API key.

To access your BuiltWith API key, you can head over to [pro.builtwith.com](https://pro.builtwith.com/) to retrieve your API key.

You can add your BuiltWith API key to Clay within the enrichment panel. The image below shows where to add your API key in the enrichment panel.

### `Action` Find Technology Stack

The **Find Technology Stack** integration with BuiltWith allows users to identify the technologies used on a website.

Users can gain insights into its tech stack, with options to filter by keyword, category, and detection date for more tailored results.

**Step 1: Select Find Technology Stack**

Access this action through the integration panel.

**Step 2: Select BuiltWith Account**

Proceed with either a Clay-managed or a personal account.

**Step 3: Configure tech stack search**

Enter the **Company Domain** search for the tech stack.

Optionally, apply filters for **Keyword or Category** and **Last Detected Date** to narrow results, and use toggles to refine the search criteria as needed:

-   **Last Detected Date Filter** — Only returns technologies that BuiltWith last detected on or after the date you enter. Accepts a specific date (e.g., "2025-01-01") or a relative date (e.g., "5 days ago").
-   **Only Return Exact Technology Names?** — When enabled, only technologies whose name exactly matches your keyword are returned. Useful when you want to confirm a company uses a specific product (e.g., "Salesforce") without returning related products (e.g., "Salesforce IQ").
-   **Use Description in Keyword or Category Match?** — When enabled, keyword matching also checks the technology's description, not just its name. Enabled by default.
-   **Show additional fields** — Returns first and last detected dates, tags, and whether the technology requires a premium BuiltWith account to view. Enabled by default.

**Step 4: Configure run settings**

Auto-update: BuiltWith will automatically enrich any new rows that get added to the table. Learn more about auto-update in this [this brief guide](https://docs.clay.com/en/articles/9642165-auto-update-and-auto-dedupe-table).

Conditional runs: To run enrichment only under specific conditions, use formulas that trigger the column when the formula is true. See [this Clay University lesson](<https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101#:~:text=Conditional runs \(which make use,personal emails for all rows\).\)>).

If needed, you can later break out entries from the list format using [Send Table Data](https://university.clay.com/docs/send-table-data) (choose **Send row for each item in a list**).

## How often are BuiltWith "first detected" and "last detected" dates updated?

The **First Detected** and **Last Detected** dates in BuiltWith **Find Technology Stack** results come directly from BuiltWith's own dataset. They are BuiltWith's crawl dates — the date BuiltWith first saw a technology on the website and the date it most recently saw it. They are **not** the date your Clay column ran, and Clay does not change or recalculate them.

What this means in practice:

-   **Running or re-running the Find Technology Stack column does not reset the dates to today.** Each run requests fresh results from BuiltWith and returns whatever detection dates BuiltWith currently has on record.
-   **The Last Detected date only moves forward when BuiltWith's crawler sees the technology on the site again.** If BuiltWith hasn't re-crawled the site since your last run, re-running the column returns the same dates.
-   **Results can include technologies a company no longer uses.** BuiltWith returns its detection history for the domain, with no separate "currently live" flag. To focus on technologies seen recently, set the **Last Detected Date Filter** (for example, "90 days ago") so older detections are excluded.
-   **The dates only appear when Show additional fields is enabled.** This toggle is on by default; if your results don't show First Detected or Last Detected, open the column settings and turn **Show additional fields** back on.

## Finding all companies that use a specific technology

Clay's **Find Technology Stack** action checks whether a given domain uses a technology. If you want to go the other direction — start with a technology and get a list of all companies that use it — you can use BuiltWith's website directly and then import the results into Clay.

**Step 1: Check whether BuiltWith tracks the technology**

Before building a list, confirm BuiltWith has coverage for the technology you want. Go to [trends.builtwith.com](https://trends.builtwith.com/) and search for the technology name. If it appears as a dedicated "Technology" result (not just a company overview), BuiltWith has it indexed.

**Step 2: Download the company list**

Open the technology's page on BuiltWith (for example, `trends.builtwith.com/websitelist/[technology-name]`) and download the list of websites currently or historically using that technology. BuiltWith exports as a CSV.

**Step 3: Import the list into Clay**

Bring the downloaded CSV into Clay as a new table (click **+ Add** → **Import CSV**). From there you can enrich company records, add contacts, and run your standard workflow.

**If the technology isn't in BuiltWith**, use a [Claygent](https://university.clay.com/docs/claygent-builder) column to scan the web for evidence. Map the company domain as an input and prompt it to search for signs of the technology — for example: *"Does {{company_domain}} use [technology name]? Search the company's website, case studies, and press mentions. Return yes or no with the evidence you found."* Claygent returns structured output, so you can add a boolean field for the yes/no result and a text field for the supporting evidence.
