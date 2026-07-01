---
title: Web intent
description: Collect visitor information including pages visited, time spent,
  and traffic sources. Includes workflow for sending emails to identified visitors.
last_synced: 2026-04-26T01:40:54.567Z
---

# Web intent

Collect visitor information including pages visited, time spent, and traffic sources.

Clay's website tracking enables teams to collect visitor information in order to understand web intent — including pages visited, time spent, and traffic sources.

This tracking provides insights into how visitors engage with your content and helps you identify high-intent accounts at the optimal moment.

**Plan availability:** Web intent is available on Trial, Pro, Growth, and Enterprise plans.

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

## Sending emails to identified website visitors

Once your visitor table is populated, you can enrich those companies to find contact emails and send outbound emails directly from Clay.

**Workflow:**

1.  **Find the right contacts** — in your visitor table, add a **Find People** enrichment to pull relevant people at each visiting company.
2.  **Get their email addresses** — add an email enrichment (such as the Work Email Waterfall) to retrieve verified work emails for those contacts.
3.  **Create an email campaign** — from your enriched table, create a Clay email campaign (see the [Email sequencer](https://university.clay.com/docs/email-sequencer) doc for setup steps). Map the email column and draft your message sequence.
4.  **Launch and let it run** — new visitors matching your tracking filters will flow into the table automatically, keeping your outreach loop always-on.

## Using a third-party website visitor identification tool

If you already use a separate website visitor identification tool to track and identify your visitors, you can route that data into Clay for enrichment and outreach without setting up Clay's native tracking.

**Bring visitor data into Clay via a webhook table:**

1.  In a Clay workbook, click `+ Add`, search for `Webhooks`, and select **Monitor webhook** to create a table with a webhook source.
2.  Copy the webhook URL Clay generates.
3.  In your visitor identification tool, configure it to POST visitor data to that URL whenever a new visitor is identified.
4.  Once records arrive in your Clay table, add enrichment columns — for example, **Find People** to find contacts at visiting companies — and set up a [Clay email campaign](https://university.clay.com/docs/email-sequencer) for personalized outreach.

See [Webhooks in Clay](webhook-integration-guide.md) for plan availability, payload format requirements, and throughput limits.

**If your visitor tool doesn't support webhooks natively**, use an automation platform such as Zapier to bridge the connection: configure a trigger on new identified visitors in your tool, add a **Webhooks by Zapier** POST action pointing to your Clay webhook URL, and map the visitor data fields in JSON. See [Send Clay data to Zapier](clay-to-zapier.md) for step-by-step instructions on routing data into Clay via a Zapier webhook.

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

### Writing website visits to Salesforce

If you want to persist website session data in Salesforce, the recommended approach is to create a **custom child object** in Salesforce rather than storing a JSON blob directly on the Account record.

**Why a child object instead of a field on Account:**

Storing the full session JSON in a single field on the Account can get hard to manage quickly — especially if the same account visits multiple times. Depending on how the write-back is configured, you risk overwriting the previous value and losing historical session data. A separate record per visit keeps the full history intact and makes Salesforce reporting much easier.

**Recommended Salesforce setup:**

1.  Create a custom object in Salesforce (e.g., `Web_Session__c`).
2.  Add a **Lookup** field on the custom object pointing to the Account.
3.  Add a **Long Text Area** field (e.g., `Raw_JSON__c`) for the full session JSON.
4.  Add dedicated fields for the values your team wants to report on — such as session date, pages visited, referrer, and duration.

**Writing from Clay:**

In your website visitor tracking table, add a Salesforce **Create Record** action targeting your custom object. Map each session's fields to the corresponding Salesforce fields. Each row in your Clay table becomes a new record in Salesforce linked to the matching Account.

This use case — creating a new per-session record in a custom Salesforce object — requires a Clay table with the Salesforce **Create Record** action. Audiences' Salesforce Export Sync is designed for syncing enriched fields and segment membership on to existing Contact and Account records, not for creating new records in custom objects.

# Troubleshooting

### Verification says "Tracking script not found"

This usually means:

-   The snippet isn't installed on all pages.
-   It's placed in the `<head>` instead of before `</body>`.
-   A Content Security Policy is blocking it.

Check your browser console for errors. Note that verification only checks if the script exists — a failed verification can still coexist with working data flow. Your Clay table is the ultimate proof of success.

To verify the script is loading at the browser level:

-   **Network tab** — search for `claydar`. Look for `init.v1.js` and `radar.min.js` with a 200 status. If they're missing, the script isn't loading.
-   **Console tab** — type `window.Claydar`. It should return an object, not `undefined`. If it returns `undefined`, the script failed to load or was blocked.
-   **Application tab** — under `Local storage` and `Cookies`, look for entries starting with `claydar_`. If present, the script is running and storing session data correctly.

### Tracking filters not working as expected

URL paths are exact-match, so `/blog` and `/blog/` are different. Also, filter changes only apply to new data — existing rows aren't affected. Make sure you haven't accidentally excluded important pages.

### Content Security Policy blocking the script

If you see a CORS error in your browser's Network tab for a request to `static.claydar.com` (for example, `init.v1.js` failing with a CORS error), your site's Content Security Policy (CSP) is blocking the Web Intent script.

Update your site's CSP to allowlist the following Clay domains:

```
Content-Security-Policy:
  default-src 'self';
  script-src 'self' https://static.claydar.com https://cdn.claydar.com;
  connect-src 'self' https://api.claydar.com;
```

### Not seeing new rows in my table

Common causes:

-   The connection is disabled or was just enabled (allow 30 minutes for data to appear).
-   The snippet isn't installed on the relevant pages.\
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

### Enrich Company returns "Company Not Found" for some web intent companies

Web intent identifies visitors at the company level by de-anonymizing IP addresses, which produces a company domain. When you run **Enrich Company** using that domain as the identifier, some companies — particularly niche, small, or regional businesses — may not have data coverage in the provider's dataset. This is expected behavior, not an error.

**To improve match rates:**

-   **Switch to a LinkedIn URL as the identifier.** Enrich Company accepts a company LinkedIn URL, domain, Sales Navigator URL, or Sales Navigator Company ID — a LinkedIn URL gives higher accuracy than a domain alone. If your web intent table doesn't include a LinkedIn URL column, add an enrichment step to look one up first, then re-run Enrich Company with that URL.
-   **Use a waterfall of company enrichment providers.** Instead of running a single Enrich Company action, create a custom waterfall column (**Add column → Waterfall**) and add multiple company enrichment providers in sequence. The waterfall stops after the first provider returns a result, so you only pay for the steps that run before a match is found. See [Waterfalls](building-a-data-waterfall.md) for setup details.

Note: Some very niche or newly formed businesses may have no coverage across any provider — in that case, "Company Not Found" is the final outcome regardless of which approach you use.

### Credit spend higher than expected

The most common cause is using `Best Match` instead of `Waterfall` for de-anonymization. `Waterfall` stops after the first match, while `Best Match` tests all providers and can cost 5-10 times more. Remember that IPs are cached for 30 days to avoid repeat costs.

Other common causes: adding new pages to tracking, removing exclusions, loosening filters, or surges in site traffic.

### Can the tracking snippet cause my site to crash?

No. The script runs in the visitor's browser and loads asynchronously, so it won't affect page performance. Website issues after installation are usually due to other simultaneous changes.

# FAQ

### Is visitor tracking data shown in real-time?

No. Clay waits for a visitor's session to finish before processing and delivering the data. Sessions are finalized after a period of inactivity, so data can be delayed up to 30 minutes after a visitor's last page view.

This means **same-session personalization is not supported** — if a visitor hits your website and you immediately query your Clay table, that session's data won't be there yet. The information only becomes available after the session ends and the pipeline has processed it.

**What Web Intent is well-suited for:**

-   **Post-session outreach:** Once a completed visit appears in your table, trigger enrichment and sequencer steps to reach relevant contacts at the identified company.
-   **Return visitor workflows:** If a company has visited before, their data is already in your table. You can use the [Clay API](https://docs.clay.com) to query that table for accounts identified in past sessions and act on it.
-   **Account-level personalization for known accounts:** Use a prior session's data (already stored in your table) to personalize future visits for returning companies.

### When will I start getting charged?

Charges begin after you install the tracking snippet and Clay starts receiving events. To stop tracking, disable the website connection under your workspace settings. Clay will stop processing new visitor sessions and stop charging Clay credits.

### How does pricing work?

**Cost:** Each successful IP enrichment consumes 1 action plus the applicable data credits (based on the de-anonymization provider). Results are cached for 30 days to avoid repeat costs.

You can view your credit spend for signals underneath the `Signals` tab of the [credit usage dashboard](https://www.clay.com/university/guide/credit-usage). To access, click on your account name → `Settings` → `Usage`.

### Can I track person-level information?

Clay's visitor tracking identifies unique accounts visiting your website, not individuals. Once an account is identified, you can use enrichments (like **Find People** and the Work Email Waterfall) to find specific people at those companies and get their email addresses. To send emails to those contacts, see [Sending emails to identified website visitors](#sending-emails-to-identified-website-visitors) above.

### How do I send emails to my website visitors?

Because Clay's visitor tracking identifies companies, not specific individuals, reaching out requires a few additional steps:

1.  In your Web Intent table, use the **Find People** enrichment to search for relevant contacts — such as decision-makers or the roles you're targeting — at each identified company.
2.  Add a **work email waterfall** column to find verified email addresses for those contacts.
3.  Add a sequencer column (Smartlead, Instantly, Outreach, or a similar tool) and set its run condition to fire when the email column is populated. This automatically enrolls new contacts into your email sequence.

This lets you reach real people at high-intent companies, even though Clay's tracking cannot identify the specific individual who visited your site.

### How many site visitors can Clay support?

Clay can support hundreds of thousands of daily visitors for even the largest enterprise customers.

### Is the visitor data consistent across different providers?

Yes, de-anonymized website data is in a consistent format across various providers.

### What do "Total Time On Page" and "Engaged Time On Page" mean, and what are the units?

Both fields are measured in **seconds**.

-   **Total Time On Page** — the total time the user had the page open in their browser, regardless of whether they were actively viewing it.
-   **Engaged Time On Page** — the total time the user was actively engaged with the page. This timer pauses when the user switches to a different tab, so it reflects genuine attention rather than just the page sitting open in the background.

A third field, **Engagement Time**, surfaces the same value as Engaged Time On Page but at a different nesting level in the session data structure.

### How do I analyze a field like UTM Term across all sessions in the table?

Session attributes such as `UTM Term` are nested under each individual session object in the web intent data. AI columns (Claygent) run at the **row level**, so they can only access values available in that specific row — they won't automatically look across every session or every nested UTM Term field in the full table.

Two approaches work well for cross-session analysis:

-   **Use Sculptor.** Open Sculptor from the bottom-right chat in your table and describe what you want to analyze. As long as the UTM Term values are visible in the table, Sculptor can read and analyze them across all rows and help you create a new column or structure the data.
-   **Flatten nested fields into columns.** Add explicit columns pulling out each session's value (for example, Session 1 UTM Term, Session 2 UTM Term). Once those values are in dedicated top-level columns, both Sculptor and AI columns can reference them directly.

### How should I set up web intent for multiple domains?

For completely separate root domains, you can create a dedicated signal per domain. Note that using the same signal across different root domains does **not** merge a visitor's journey across those sites. Because the tracking relies on first-party cookies scoped to each domain, visitors on `company-a.com` and `company-b.com` will have separate session and visitor IDs even if they are the same person.

For subdomain tracking questions (for example, `shop.company.com` and `blog.company.com`), contact Clay support to confirm how your configuration handles cross-subdomain sessions.

### What do I need to know about GDPR and cookie consent for web intent?

The tracking script captures IP address data, which may be considered personally identifiable information in some jurisdictions. Work with your legal and web teams to confirm that your consent and privacy setup supports your intended use. In particular, make sure your Content Security Policy and any cookie consent tooling allow the Clay tracking scripts to run — if they block the script, tracking will stop working.

### What cookies and local storage items does the tracking script use?

All storage keys are prefixed with `claydar_`. The script uses `localStorage` by default and falls back to cookies if `localStorage` is unavailable.

| Key | Storage | Expires | Purpose |
|-----|---------|---------|---------| 
| `claydar_device_id` | localStorage / Cookie | 365 days | Unique device identifier across sessions |
| `claydar_session` | localStorage | 60 min of inactivity | Current session data (id, start time, engagement) |
