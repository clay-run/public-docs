---
title: Clay Ads
source_url: https://university.clay.com/docs/clay-ads
last_synced: 2026-04-26T01:39:43.557Z
upstream_hash: 06885b8c873ff50c640ce0ef5253ce195e7b3acdf5145c13e3e79cb3dc010016
---

# Clay Ads

Build and sync contact and account lists to LinkedIn and Meta for precise ad targeting.

Build and sync contact and account lists to LinkedIn and Meta for precise ad targeting. Import your target accounts and contacts into Clay, enrich them with personal emails for better match rates, then sync to ad platforms for campaigns and exclusions.

**Key use cases:**

-   Target high-intent prospect lists synced from your CRM
-   Re-target leads based on website activity or engagement signals
-   Create exclusion lists to prevent advertising to existing customers, employees, or open opportunities
-   Advertise to executives who recently changed jobs or got promoted
-   Target leads that aren't in your CRM to expand total addressable market

## **Creating and syncing ad audiences**

_Note: Personal email addresses significantly improve match rates when syncing to ad platforms. Use the `Hashed Email for Ads` waterfall to find contact email addresses._

1.  **To start, go to `Ads`** from the Clay homepage. Then click `New Ad Sync` and select a source type:
    -   **Best practice:** Sync lists from your CRM (Salesforce, HubSpot) or data warehouse for compliance
    -   Also available: CSV upload
    -   Note: Contact search through Clay (CPJ) is currently restricted to US-only contacts for compliance reasons
2.  **Choose your connected account** on LinkedIn or Meta and prepare your data before mapping:
    -   LinkedIn has character limits for certain fields. If needed, add a formula column to shorten longer job titles for better match rates.
3.  **Map columns** for the selected platform and click `Continue`. Not every field is required, but these combinations are critical for match rates:
    -   **For contacts:** Hashed email + first name/last name (required for optimal matching)
    -   **For accounts:** Company name + company website (required for optimal matching)
4.  **Review your audience insights and quality summary**.
    -   Check your estimated match rate and audience size before syncing.
    -   Make adjustments to your table if needed (for example, narrowing down to specific job titles or industries) and re-run your export.
5.  **Send your audience** to the selected platform.
    -   Your audience will be created within **24 hours for Meta** and **48 hours for LinkedIn**. You can then attach your audience to campaigns in LinkedIn Campaign Manager or Meta Ads Manager.

Once synced, your audience updates automatically as data changes in your Clay table. Contacts and accounts are added or removed based on your criteria, keeping your ad targeting aligned with your latest data.

## **Managing ad audiences**

You can view and manage all synced audiences from the `Exports` panel in your table. This view shows:

-   Sync status and history
-   Match rates for each sync
-   Total audience size
-   Last sync timestamp

To update an audience, simply modify the data in your Clay table. The audience will automatically resync based on your configured schedule.

## **Glossary**

-   **Match rate** — The percent of contacts or accounts your ad platform can match to real users. Personal emails usually improve match rates (often ~40–60%+ on Meta and up to ~95% on LinkedIn).
-   **Ad audience** — A list of contacts or accounts synced from Clay to an ad platform for use in campaigns. Audiences can be used for targeting (showing ads to people on the list) or exclusion (preventing ads from reaching people on the list).
-   **Exclusion list** — An ad audience configured to prevent a group of people from seeing your ads. Common exclusion lists include existing customers, current employees, or open pipeline opportunities — helping eliminate wasted ad spend.
-   **Hashed email** — A privacy-safe version of an email address encrypted using a one-way algorithm (SHA-256) before being sent to an ad platform. Ad platforms use hashed emails to match contacts without ever seeing the raw address. Clay's `Hashed Email for Ads` waterfall finds and hashes personal emails automatically to maximize match rates.
-   **Audience sync** — The process of sending a Clay table's contacts or accounts to an ad platform and keeping them continuously updated. When rows are added or removed from your Clay table, the synced audience updates accordingly — no manual re-exports needed.

## **FAQs**

### **What platforms are supported?**

Clay currently supports syncing ad audiences to LinkedIn and Meta. Support for Google Ads is coming soon.

### **Is this feature available on all plans?**

Ad audiences are available on **Growth** and **Enterprise** plans:

-   **Growth**: Includes 1 ads platform sync
-   **Enterprise**: Includes unlimited audiences and additional ads platform syncs

Each record exported or synced consumes 1 action. Data credits apply for any enrichments used in the table to build the audience.

### **What are the limitations?**

The 50,000 row limit applies to ad audiences exported from tables. For larger audiences, create multiple tables and attach multiple audiences to your campaigns in the ad platform.

### **How long does it take for audiences to be created?**

After sending your audience to LinkedIn or Meta, it will be created within **48 hours** (typically 1-2 days). Plan accordingly when launching time-sensitive campaigns.

### **Why should I use personal emails instead of work emails?**

Personal emails are essential for better match rates because most users sign up for LinkedIn and Meta with personal email addresses rather than work emails. Match rates depend on your audience data quality. To maximize results, use the `Hashed Email for Ads` waterfall to find contact email addresses.

### **Do audiences automatically update?**

Yes! Once synced, your audiences automatically update as data changes in your Clay table. New rows that match your criteria are added, and rows that no longer match are removed. This keeps your ad targeting aligned with your latest data without manual updates.

### **Can I see which contacts matched?**

No, LinkedIn and Meta don't provide contact-level match visibility for privacy reasons. However, Clay shows aggregate match rates and total audience size after each sync.

### **How do I connect my LinkedIn or Meta ad account?**

When you create your first ad audience, you'll be prompted to authenticate with LinkedIn Campaign Manager or Meta Business Manager. Make sure you have admin access to the ad account you want to use.

### **Can I sync to multiple ad accounts?**

Yes, you can connect multiple LinkedIn or Meta ad accounts and choose which account to sync each audience to.

### **How much does it cost to sync audiences?**

Each record exported or synced to an ad platform consumes 1 action (for the export/sync work). Data credits are consumed for any enrichments you run in the table to build your audience (e.g., finding emails, enriching profiles). The export itself does not consume additional data credits.
