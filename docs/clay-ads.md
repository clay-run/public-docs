---
title: Clay Ads
source_url: https://university.clay.com/docs/clay-ads
description: Build and sync contact and account lists to LinkedIn, Meta, and Google Ads for
  precise ad targeting.
last_synced: 2026-05-11T17:47:40.000Z
---

# Clay Ads

Build and sync contact and account lists to LinkedIn, Meta, and Google Ads for precise ad targeting.

Build and sync contact and account lists to LinkedIn, Meta, and Google Ads for precise ad targeting. Import your target accounts and contacts into Clay, enrich them with personal emails for better match rates, then sync to ad platforms for campaigns and exclusions.

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
    -   Note: When using Clay's company/people search (CPJ) as a source, data source restrictions apply by platform — only US-origin contacts are eligible for LinkedIn and Meta; CPJ data cannot be used at all for Google Ads. For Google Ads syncs, use your CRM or data warehouse as the source.
2.  **Choose your connected account** on LinkedIn or Meta and prepare your data before mapping:
    -   LinkedIn has character limits for certain fields. If needed, add a formula column to shorten longer job titles for better match rates.
    -   **Note:** Ad Sync tables have a more limited selection of enrichment providers and actions than regular Clay tables. For complex transformations (such as domain normalization), prepare the data upstream in a regular table first, then use that table or a Clay Audience as the source for your Ad Sync.
3.  **Map columns** for the selected platform and click `Continue`. Not every field is required, but these combinations are critical for match rates:
    -   **For contacts:** Hashed email + first name/last name (required for optimal matching)
    -   **For accounts:** Company name + company website (required for optimal matching)
    -   **Note:** When syncing a LinkedIn **Account list**, a **Company URL** field is also available in the mapping step and can improve match rates. This field does not appear for Contact list audiences — LinkedIn does not support company URL matching for contacts.
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

## Meta system user token authentication

For production Clay Ads workflows syncing to Meta, we recommend using a system user token instead of OAuth. System user tokens provide indefinite access and don't require manual renewal every 60 days.

### Creating a system user token

To create a new system user token, you first need to create an app:

1.  Open your [Meta Business account](https://business.facebook.com/) and navigate to `Business Settings` > `Accounts` > `Apps`. Click `Add`.
2.  Choose `Create a new app ID`.
3.  Name your app.
4.  Select the use case as `Other`.
5.  Set the app type to `Business`.</s>
6.  Click `Create app`.
7.  Ensure the app has `Ads Management Standard Access` permissions. You can find this setting in `App Review` > `Permissions and Features`.
8.  Navigate to `Business Settings` > `Users` > `System users` and add a new system user with `Admin` access.
9.  Use the `Add assets` button to assign both the app you created and the ad account that you want to create audiences for to the system user. Be sure to give both the app and the ad account `Full Control`, not `Partial Access`.
10.  Once the system user is created and assets are assigned, select `Generate token`.
     -   Choose the app you created to generate the token.
     -   Select the expiration policy for the token (we recommend `Never expire`).
     -   Ensure the `ads_management` permission is selected.
     -   Click `Generate token`.
11.  Copy the generated token immediately — Meta won't store it, so consider saving it in a secure password vault.
12.  In Clay, when connecting your Meta account for ad syncs, select `Use system user token` as the authentication method and paste your token.

### Why use a system user token?

-   No manual renewal — OAuth tokens expire every 60 days and require re-authentication. System user tokens can be set to never expire.
-   Production reliability — Avoid sync failures from expired tokens in automated workflows.
-   Team access — System users aren't tied to individual employee accounts, so access persists even if team members leave.

For more details on Meta system user setup, see [Meta's system user documentation](https://www.facebook.com/business/help/503306463479099).

## **FAQs**

### **What platforms are supported?**

Clay currently supports syncing ad audiences to **LinkedIn**, **Meta**, and **Google Ads**.

Note that data source restrictions apply depending on the platform — see [Why are some contacts excluded when I set up an ad sync?](#why-are-some-contacts-excluded-when-i-set-up-an-ad-sync) below for details.

### **Why are some contacts excluded when I set up an ad sync?**

When you create an ad sync, you may see an **Ad sync segment filters** panel showing a breakdown of your audience segment size, excluded contacts, and syncable contacts. Some contacts are automatically filtered out based on the platform you're syncing to and where their data originally came from.

**What "US Origin" means:** A contact is classified as US-origin when their country value is the United States. This classification applies specifically to contacts sourced from Clay's company and people search (CPJ data).

**Why contacts get excluded:**

-   **LinkedIn and Meta:** Contacts sourced from Clay's company/people search (CPJ) are restricted to US-origin contacts only. Non-US CPJ contacts are automatically filtered out.
-   **Google Ads:** Contacts sourced from Clay's company/people search (CPJ) or any other third-party data source are excluded entirely, regardless of country. Only contacts sourced from your own CRM (Salesforce, HubSpot) or data warehouse are eligible for Google Ads syncs.

These restrictions exist for compliance reasons, as third-party sourced contact data is subject to usage limitations under each ad platform's terms of service.

**Why the filters are locked:** The filters remain applied to your segment for as long as an ad sync is active. This prevents credits from being spent enriching contacts that would be excluded from the sync anyway.

**Note:** CPJ filtering during ad syncs is currently available for Enterprise workspaces. Contact Clay support if you'd like this enabled for your workspace.

### **Is this feature available on all plans?**

Ad audiences are available on **Growth** and **Enterprise** plans:

-   **Growth**: Includes 1 ads platform sync
-   **Enterprise**: Includes unlimited audiences and additional ads platform syncs

Each record exported or synced consumes 1 action. Data credits apply for any enrichments used in the table to build the audience.

### **What are the limitations?**

The 50,000 row limit applies to ad audiences exported from tables. For larger audiences, create multiple tables and attach multiple audiences to your campaigns in the ad platform.

### **Can I edit the field mapping after setting up an Ad Sync?**

No. Field mapping is configured when you create the Ad Sync and cannot be changed afterward. Deactivating an Ad Sync places it in read-only history — it does not unlock the mapping for editing. To use a different field mapping, deactivate the current sync and create a new Ad Sync with your updated configuration.

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

### **Can I use hashed emails for ad targeting in the EU?**

Under GDPR, hashed personal emails are still considered personal data — hashing is a pseudonymization technique, not anonymization. This means EU data-protection rules apply regardless of whether you send a raw or hashed email to an ad platform.

**First-party contacts** (contacts already in your CRM or database who have an existing relationship with your business) can generally be enriched with the `Hashed Emails for Ads` waterfall and activated for EU ad targeting, provided you have a valid GDPR legal basis — such as legitimate interest or consent — for using their data for advertising.

**Net-new contacts discovered through Clay** are a different matter. Using third-party-sourced hashed personal emails for Custom Audience targeting in the EU carries significant GDPR risk, because you likely have no established legal basis to process those individuals' data for advertising.

**EU-compliant approaches:**
-   **Lookalike targeting (TOFU):** Export your first-party CRM contacts → run the `Hashed Emails for Ads` waterfall → upload to Meta or LinkedIn → build a Lookalike audience in the platform → exclude the seed list.
-   **ABM targeting:** Run account-based campaigns against named accounts using your CRM contacts, keeping all data first-party.

_This is informational guidance only, not legal advice. Always consult your legal team before activating audiences using EU-based contact data._
