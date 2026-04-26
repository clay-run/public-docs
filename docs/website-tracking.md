---
title: Web intent
source_url: https://university.clay.com/docs/website-tracking
description: Collect visitor information including pages visited, time spent,
  and traffic sources.
last_synced: 2026-04-26T01:40:54.567Z
upstream_hash: 28b397dda0a2866f285eb94622303ee73697a5c5e2f26f124d56ff97604c2967
---

# Web intent

Collect visitor information including pages visited, time spent, and traffic sources.

Clay’s website tracking enables teams to collect visitor information in order to understand web intent — including pages visited, time spent, and traffic sources.

This tracking provides insights into how visitors engage with your content and helps you identify high-intent accounts at the optimal moment.

## Using website tracking in Clay

### **Creating the connection**

1.  Click on your account name → `Settings` → `Website tracking`.
2.  Click `Add connection` and give the connection a unique name – you'll need this later.
3.  Copy the code under `Install tracking snippet` and install with one of the two methods.
    -   **Directly installing a tracking snippet (Recommended):**
        -   We recommend installing the tracking snippet before the closing `</body>` tag on **all pages** of your website to collect comprehensive data. This snippet loads tracking scripts asynchronously, ensuring it won't affect your page loading time.
    -   **Installing via** [**Google Tag Manager**](https://support.google.com/tagmanager/answer/6107167#CustomHTML)**:**

        -   _Note: While this method works, we recommend installing directly as ad blockers often disable Tag Manager._

        1.  Navigate to the `Tags` section in your GTM account.
        2.  Click `New` in the top-left to create a new tag..
        3.  Add a name like `Clay Visitor Tracking`.
        4.  Edit your `Tag Configuration`, and select `Custom HTML` as the tag type.
        5.  Paste the JavaScript snippet from Clay into the text box.
        6.  Below, add a new trigger, and select `All Pages`.
        7.  Finally, click `Save` for this new tag, and publish your changes.
    -   **Installing via** [**Twilio Segment**](https://segment.com/docs/connections/destinations/catalog/actions-clay/)**:**
        1.  Visit [this link](https://app.segment.com/goto-my-workspace/destinations/catalog/actions-clay) to add the Clay integration as a new destination in Segment.
        2.  Select the website data source in Segment you want to connect to Clay.
        3.  From your Clay website connection page, copy both your `Connection key` and `Secret key` to the Segment settings page.
        4.  Enable your Clay destination to begin sending events.
4.  Configure which de-anonymization providers you'd like to use. Clay provides a recommended selection or you can manually choose your own provider settings.
    -   **Note:** Pricing is based on unique IP addresses that successfully retrieve data. You'll be charged at most once per 30-day period for each visitor with the same IP address who visits your website.
5.  Add filters for specific countries or pages.
    -   You can include a `*` to match any page paths (e.g., `/blog*`).
6.  Make sure `Connection enabled` is toggled and click `Save`.
7.  In a workbook, under `Create`, click `Website visitor tracking`.
8.  Select your website connection from the dropdown and adjust your filters.
    -   Configure your table filters using page paths, session time, referrer, or UTM tags to show only relevant visitor data.
    -   For advanced filtering, create filter groups and adjust visit frequency parameters to refine results.

Website visitor data appears in your table grouped by company domain. Since we only display completed visitor sessions, data may be delayed up to 30 minutes after user activity.

# Best practices

### Snippet placement

Install the tracking snippet before the closing `</body>` tag, not in the `<head>`. We recommend placing it in a global site template so it appears on all pages of your website.

### URL path formatting

Use relative URL paths starting from the root domain:

-   ✅ `/pricing` or `/blog/*`
-   ❌ `https://www.example.com/pricing`

For wildcards, use `*` to match all child pages (e.g., `/resources/*`). Note that URL paths are exact-match, so `/blog` and `/blog/` are treated as different paths.

### Reducing credit usage

To minimize credit usage while maintaining quality results, adjust your **advanced filters** to focus on higher-intent traffic.

**Recommended settings:**

-   **Minimum session duration:** 20–30 seconds
-   **Minimum unique pages visited:** 2

These filters help narrow your results to visitors who spend more time on site and engage with multiple pages, indicating genuine interest.

**Use Waterfall instead of Best Match:** `Waterfall` stops after the first provider match, while `Best Match` tests all providers and can cost 5-10 times more. Remember that IPs are cached for 30 days to avoid repeat costs.

# Troubleshooting

### Verification says "Tracking script not found"

This usually means:

-   The snippet isn't installed on all pages.
-   It's placed in the `<head>` instead of before `</body>`.
-   A Content Security Policy is blocking it.

Check your browser console for errors. Note that verification only checks if the script exists — a failed verification can still coexist with working data flow. Your Clay table is the ultimate proof of success.

### Tracking filters not working as expected

URL paths are exact-match, so `/blog` and `/blog/` are different. Also, filter changes only apply to new data — existing rows aren't affected. Make sure you haven't accidentally excluded important pages.

### Content Security Policy blocking the script

Update your site's Content Security Policy to allow Clay domains:

`Content-Security-Policy:   default-src 'self';   script-src 'self' <https://static.claydar.com> <https://cdn.claydar.com>;   connect-src 'self' <https://api.claydar.com>;`

### Not seeing new rows in my table

Common causes:

-   The connection is disabled or was just enabled (allow 30 minutes for data to appear).
-   The snippet isn't installed on the relevant pages.
-   Connection-level or table-level filters are too restrictive.
-   Your site hasn't had enough live traffic yet.

### Web intent connection stopped or shows as disabled

This happens when:

-   The signal hit its credit spend limit.
-   Your workspace ran out of credits.
-   The table reached the 50,000 row limit (enable passthrough tables to avoid this).

You'll need to manually re-enable the connection after addressing the issue — it won't resume automatically.

### Unexpected companies showing up in results

Traffic from bots, VPNs, cloud infrastructure, or ISP-owned IPs can appear as companies. Filter results by company size, industry, or minimum visit count to screen out unwanted records.

### Wrong domain showing for a company

IP de-anonymization can sometimes return a secondary or infrastructure domain instead of the primary marketing domain. If needed, use Clay enrichments by company name instead of domain to improve data quality.

### Credit spend higher than expected

The most common cause is using `Best Match` instead of `Waterfall` for de-anonymization. `Waterfall` stops after the first match, while `Best Match` tests all providers and can cost 5-10 times more. Remember that IPs are cached for 30 days to avoid repeat costs.

Other common causes: adding new pages to tracking, removing exclusions, loosening filters, or surges in site traffic.

### Can the tracking snippet cause my site to crash?

No. The script runs in the visitor's browser and loads asynchronously, so it won't affect page performance. Website issues after installation are usually due to other simultaneous changes.

# FAQ

### Is visitor tracking data shown in real-time?

No, visitor event data can be delayed up to 30 minutes. This allows the full visitor session to be completed first.

### When will I start getting charged?

Charges begin after you install the tracking snippet and Clay starts receiving events. To stop tracking, disable the website connection under your workspace settings. Clay will stop processing new visitor sessions and stop charging Clay credits.

### How does pricing work?

**Cost:** Each successful IP enrichment consumes 1 action plus the applicable data credits (based on the de-anonymization provider). Results are cached for 30 days to avoid repeat costs.

You can view your credit spend for signals underneath the `Signals` tab of the [credit usage dashboard](https://www.clay.com/university/guide/credit-usage). To access, click on your account name → `Settings` → `Credit usage`.

### Can I track person-level information?

Clay's visitor tracking identifies unique accounts visiting your website, not individuals. Once an account is identified, you can use enrichments to find specific profiles of relevant people you may want to target at those companies.

### How many site visitors can Clay support?

Clay can support hundreds of thousands of daily visitors for even the largest enterprise customers.

### Is the visitor data consistent across different providers?

Yes, de-anonymized website data is in a consistent format across various providers.
