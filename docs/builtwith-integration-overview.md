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

-   **Only Return Exact Technology Names?** — When enabled, only technologies whose name exactly matches your keyword are returned. Useful when you want to confirm a company uses a specific product (e.g., "Salesforce") without returning related products (e.g., "Salesforce IQ").
-   **Use Description in Keyword or Category Match?** — When enabled, keyword matching also checks the technology's description, not just its name. Enabled by default.
-   **Show additional fields** — Returns first and last detected dates, tags, and whether the technology requires a premium BuiltWith account to view. Enabled by default.

**Step 4: Configure run settings**

Auto-update: BuiltWith will automatically enrich any new rows that get added to the table. Learn more about auto-update in this [this brief guide](https://docs.clay.com/en/articles/9642165-auto-update-and-auto-dedupe-table).

Conditional runs: To run enrichment only under specific conditions, use formulas that trigger the column when the formula is true. See [this Clay University lesson](<https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101#:~:text=Conditional runs \(which make use,personal emails for all rows\).\)>).

If needed, you can later break out entries from the list format using [Send Table Data](https://university.clay.com/docs/send-table-data) (choose **Send row for each item in a list**).

## Finding all companies that use a specific technology

Clay's **Find Technology Stack** action checks whether a given domain uses a technology. If you want to go the other direction — start with a technology and get a list of all companies that use it — you can use BuiltWith's website directly and then import the results into Clay.

**Step 1: Check whether BuiltWith tracks the technology**

Before building a list, confirm BuiltWith has coverage for the technology you want. Go to [trends.builtwith.com](https://trends.builtwith.com/) and search for the technology name. If it appears as a dedicated "Technology" result (not just a company overview), BuiltWith has it indexed.

**Step 2: Download the company list**

Open the technology's page on BuiltWith (for example, `trends.builtwith.com/websitelist/[technology-name]`) and download the list of websites currently or historically using that technology. BuiltWith exports as a CSV.

**Step 3: Import the list into Clay**

Bring the downloaded CSV into Clay as a new table (click **+ Add** → **Import CSV**). From there you can enrich company records, add contacts, and run your standard workflow.

**If the technology isn't in BuiltWith**, use a [Claygent](https://university.clay.com/docs/claygent-builder) column to scan the web for evidence. Map the company domain as an input and prompt it to search for signs of the technology — for example: *"Does {{company_domain}} use [technology name]? Search the company's website, case studies, and press mentions. Return yes or no with the evidence you found."* Claygent returns structured output, so you can add a boolean field for the yes/no result and a text field for the supporting evidence.

## Identifying which ATS platform a company uses

To find out which applicant tracking system (ATS) a company uses to post jobs on their careers page — for example, Greenhouse, Lever, Ashby, or Workday — combine Claygent with Clay Navigator and BuiltWith technographics.

**Claygent with Clay Navigator (visit the careers page directly)**

Clay Navigator is Clay's browser-based model that can visit live URLs and extract information directly from web pages. To use it for ATS detection:

1.  Add a **Claygent** column to your table and set the model to **Clay Navigator**.
2.  Map the company domain as an input variable.
3.  Write a prompt such as: *"Visit the careers page at {{company_domain}} and identify which ATS platform hosts their job listings — for example, Greenhouse, Lever, Ashby, Workday, or Rippling. Return the platform name and the URL where you found the job listings."*
4.  Define a JSON output schema with a `string` field for the ATS name and a `string` field for the source URL.

Clay Navigator costs 6 credits per row. See [Claygent builder](claygent-builder.md) for full setup details.

**BuiltWith technographics (detect embedded ATS code)**

Run the **Find Technology Stack** action on each company domain. Use the **Keyword or Category** filter to check for specific ATS tools — for example, enter "Greenhouse", "Lever", or "Ashby" as the keyword to detect whether that platform's tracking code is embedded on the page. This costs 2 credits per row and works well for ATS platforms that inject scripts or embed job widgets.

**Normalizing results with an AI formula**

For highest accuracy, run both approaches and add a **Use AI** column to normalize the two results into a single clean value:

*"Given these two ATS signals — Claygent result: {{claygent_ats}}, BuiltWith result: {{builtwith_ats}} — return the most likely ATS platform name as a single clean category, or 'Unknown' if neither signal is conclusive."*

This gives you a structured column per company showing exactly which platform they use to host jobs.
