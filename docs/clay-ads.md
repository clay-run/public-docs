---
title: Clay Ads
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
    -   **Important:** Email is the primary field ad platforms use to match contacts. If no email column is mapped, the platform will process the sync but return an audience size of 0 — even for tens of thousands of contacts. This appears as a "too small for use in campaigns" status. Because field mapping cannot be changed after an Ad Sync is created, verify at least one email column is mapped before sending your audience.
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
5.  Set the app type to `Business`.
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

## Google Ads OAuth authentication

Google Ads audience syncing is currently in **closed beta** — contact [Clay support](https://www.clay.com/contact) to request access.

When you connect your Google Ads account, Clay requests the following OAuth permission:

-   **`https://www.googleapis.com/auth/adwords`** — the standard Google Ads API scope

**For security teams:** This scope grants read/write access to the connected Google Ads account. It is the only scope Google's Ads API offers — Google does not provide narrower alternatives for the Ads API, even though Clay only uses the access to manage audience lists. Clay sends contact identity data (personal email or SHA-256 hashed email, phone number, first name, last name, country code, and postal code) to create, update, or remove Customer Match audience lists. The integration does not access campaign performance data, modify bids or budgets, or create or change any ads.

Access control is enforced at the Google Ads account level — the person connecting must have appropriate permissions on the ad account they link.

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

### **Can I add a second ad platform to an existing Ad Sync?**

Yes. After your initial sync is active, an **Expand your reach** section appears below your current platform destinations. Click **Add** next to any available platform to configure field mappings for that provider — it will sync on the same schedule as your existing provider.

**Notes:**

-   You cannot add a platform while a sync is currently in progress — wait for the active sync to complete first.
-   Google Ads is only available for audiences sourced from first-party data (your own CRM or data warehouse). If your audience includes contacts from Clay's company/people search data, Google Ads will appear disabled. See [Why are some contacts excluded when I set up an ad sync?](#why-are-some-contacts-excluded-when-i-set-up-an-ad-sync) for details.

### **How long does it take for audiences to be created?**

After sending your audience to LinkedIn or Meta, it will be created within **48 hours** (typically 1-2 days). Plan accordingly when launching time-sensitive campaigns.

### **Why should I use personal emails instead of work emails?**

Personal emails are essential for better match rates because most users sign up for LinkedIn and Meta with personal email addresses rather than work emails. Match rates depend on your audience data quality. To maximize results, use the `Hashed Email for Ads` waterfall to find contact email addresses.

### **How does the `Hashed Email for Ads` waterfall work?**

The `Hashed Email for Ads` waterfall uses professional profile URL as the primary input (some providers also accept work email or other identifiers) to find and return a SHA-256 hashed personal email for each contact. The input is not what gets hashed — it is used only to identify the person and look up their personal email, which is then hashed.

If the waterfall prompts for work email as input, that is normal. One or more providers in the waterfall will use the work email to look up the contact and retrieve their personal email for hashing. Providing work email as input does not cause the work email itself to be hashed, and your match rates are not affected.

The waterfall queries multiple providers and returns a **single hashed email** per contact from the first provider that finds a result.

### **Do audiences automatically update?**

Yes! Once synced, your audiences automatically update as data changes in your Clay table. New rows that match your criteria are added, and rows that no longer match are removed. This keeps your ad targeting aligned with your latest data without manual updates.

### **Can I see which contacts matched?**

No, LinkedIn and Meta don't provide contact-level match visibility for privacy reasons. However, Clay shows aggregate match rates and total audience size after each sync.

### **Why does my ad audience show "too small for use in campaigns"?**

Ad platforms report an audience as "too small" when fewer than 300 contacts matched. The most common cause is that no email column was mapped in the field mapping — ad platforms match contacts by email, so without it the platform processes all sent records but matches 0.

A second factor: if Enhanced Matching is enabled, it uses a professional profile URL or Work Email column you designate to look up personal emails before syncing. If those input columns are not configured, Enhanced Matching cannot improve your match rate.

**To fix this:** Because field mapping cannot be changed after an Ad Sync is created, you'll need to deactivate the current sync and create a new one. Map at least one email column, and configure Enhanced Matching inputs if using that feature. See [Why should I use personal emails instead of work emails?](#why-should-i-use-personal-emails-instead-of-work-emails) for guidance on which email type gives the best results.

### **How do I connect my LinkedIn, Meta, or Google Ads account?**

When you create your first ad audience, you'll be prompted to authenticate with LinkedIn Campaign Manager, Meta Business Manager, or your Google Ads account via OAuth. Make sure you have admin access to the ad account you want to use. Note that Google Ads syncing is currently in closed beta — contact [Clay support](https://www.clay.com/contact) to request access.

### **Why did I receive an email saying my Meta account will disconnect soon?**

This is expected behavior. Meta enforces a 60-day expiry on OAuth tokens — when you connect your Meta account to Clay using "Sign in with Facebook," the connection stays active for 60 days before it needs to be renewed. Clay sends a warning email 7 days before expiry and again 1 day before expiry so you can take action before any Ad Syncs are interrupted.

**To resolve this, you have two options:**

-   **Reconnect your Meta account** — go to your Meta connections in Clay and click to reconnect using "Sign in with Facebook." This resets the 60-day timer.
-   **Switch to a System User Token** — system user tokens can be configured to never expire, avoiding the need to reconnect every 60 days. This is the recommended approach for production Ad Sync workflows. See [Meta system user token authentication](#meta-system-user-token-authentication) for setup instructions.

### **Can I sync to multiple ad accounts?**

Yes, you can connect multiple LinkedIn or Meta ad accounts and choose which account to sync each audience to.

### **How much does it cost to sync audiences?**

Each record exported or synced to an ad platform consumes 1 action (for the export/sync work). Data credits are consumed for any enrichments you run in the table to build your audience (e.g., finding emails, enriching profiles). The export itself does not consume additional data credits.
