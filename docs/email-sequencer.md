---
title: Email sequencer
description: Run outbound campaigns directly from your table.
last_synced: 2026-05-04T00:00:00.000Z
upstream_hash: 3d3db81ae3036812b3d4dc0b56f1ae7fff367acb652370008e4fdffc6f91fa96
---

# Email sequencer

Run outbound campaigns directly from your table.

Clay's email sequencer lets you run outbound email campaigns directly from your tables. This guide covers setup, campaign configuration, sending behavior, analytics, and troubleshooting tips.

## Connecting Google Workspace via OAuth

**Note:** This setup requires Google Workspace admin access and only needs to be done once per domain. Changes can take up to 24 hours to apply.

1.  In Clay, go to `Campaigns` → `Email Accounts` → `Add email accounts` → `Google OAuth`.
2.  Copy the Clay Sequencer Client ID from the `Search for Clay Sequencer` step in the modal.
3.  Go to your [Google Workspace Admin Panel](https://admin.google.com/) and navigate to `Security` → `API Controls` → `App Access Control`.
4.  Click `Configure new app`.
5.  Paste the Client ID into the search bar and click `Search`.
6.  Select `Clay Sequencer (Web)` from the results.
7.  Choose which org units should have access — either `All in [your org] (all users)` or specific org units — then click `Continue`.
8.  Select `Trusted` under Access to Google Data and click `Continue`.
    -   **Important:** You must choose `Trusted`, not `Specific Google Data`. Selecting `Specific Google Data` will not grant all the permissions Clay needs, and the access error will persist. Despite the name, `Trusted` only allows Clay to request Gmail-specific permissions (full email access, basic email settings, OpenID, and your profile) — it does **not** grant Clay access to Google Drive, Calendar, Docs, or any other Google service.
9.  Review the summary and click `Finish`.
10.  Back in Clay, click `Continue` in the modal, then click `Connect your Google account` and complete the OAuth sign-in.

## Create a new email campaign

1.  Start in a table that contains the lead emails you want to contact.
    -   If you haven't done this yet, click `Tools` → `Import` to add emails from a third party or CSV.
2.  Click `Tools` → `Exports` → `Create Clay email campaign`
    -   The `Sync lead data to campaign` column automatically pushes 10 rows from your parent table into the campaign to draft with
    -   Tip: You can customize the `Sync lead data to campaign` column to only send leads with an email address using `Only run if`.
3.  In the `Setup` tab, you can set:
    -   `Lead email address`: We automatically detect email address columns, but confirm this before proceeding.
    -   `Enable HTML`: Campaigns default to plaintext for better deliverability. Enable HTML if you want to use formatting features like fonts, bold text, and hyperlinks. This also unlocks advanced settings such as open tracking, click tracking, and unsubscribe links. **Note:** The `Enable HTML` toggle is currently in beta and is not available in every workspace — if the toggle appears disabled, contact support to request access.
4.  Under `Message sequence`, draft and customize your emails (up to 4 per campaign). Sequences automatically stop when all emails are sent or when a lead replies (excluding out-of-office replies, which we detect and work around).
    -   Toggle `Preview` mode to see real data from your source table in the message template. When HTML is enabled (beta — see note above), Preview also renders how your formatting will appear in the recipient's inbox — the message editor shows the content structure you've built, not the final rendered output, so use Preview to verify formatting before sending.
    -   Within each message, use `/` to access features such as:
        -   `Clean variable`: Reference synced lead data with safe fallbacks and optional formatting. When configuring a Clean variable, the **Fallback** field ("Simple text to display if variable is empty") is required — the variable will not save if left blank.
        -   `Sender variable`: Reference identifying information from the sending account
        -   `AI snippet`: Generate personalized copy for each lead automatically. After inserting an AI snippet via `/`, a snippet chip appears in your message. Click the chip to open the inline prompt editor — describe what the snippet should generate and reference lead data columns in your instructions (for example: *"Write a one-sentence opening based on [Company Domain] and [Job Title]"*). Toggle **Preview** to see the AI-generated output for your current preview lead in real time and refine the prompt as needed. The AI model is configured at the campaign level, not per snippet; if you need to control which AI model generates the copy, build the personalized content in a **Use AI** column in your source table and reference it as a `Clean variable` in the email template instead.
        -   `Spintax variable`: Choose a random value from a list
        -   `Rows from [Table]`: Directly reference synced data (Clean variables are recommended to handle empty values safely).
        -   (HTML only): If enabled, use hyperlinks, inline images, fonts, and rich text formatting.
5.  Go to `Settings` to add your email account:
    -   `Google OAuth` (recommended): Connect your Google Workspace account via OAuth.
        -   ⚠️ Note: You or your Workspace admin must authorize the Clay sequencer app for your domain, or you'll see an access error.
    -   `Microsoft Outlook OAuth` (recommended): Connect your Outlook account via OAuth.
        -   ℹ️ Note: Unlike Google OAuth, no Clay-side admin setup is required upfront. If your Microsoft 365 / Entra tenant requires admin approval for third-party apps, your admin may need to grant consent for "Clay Sequencer – Smartlead" in the [Microsoft Entra Admin Center](https://entra.microsoft.com).
    -   `SMTP`: Connect a single account via SMTP credentials directly.
    -   `Bulk CSV upload`: Add multiple accounts at once by uploading a CSV. Download the example template from the modal and fill in the following eight columns for each account: `from_email`, `from_name`, `user_name`, `password`, `smtp_host`, `smtp_port`, `imap_host`, `imap_port`. For Google Workspace accounts, generate an app password for each account (Google Account → Security → 2-Step Verification → App passwords) and use it as the `password` value.
    -   You can also [buy email accounts directly in Clay](https://university.clay.com/docs/buying-email-accounts) if you want to increase your sending capacity.
    -   After setup, you can:
        -   `Enable warmup`: Sends and receives automated emails from the linked account to build reputation. Each account uses a unique two-word keyphrase (e.g., `clever-rocket`) to identify warmup emails. Follow the in-app instructions to set up a label and filter to easily ignore warmup messages.
        -   `Restrict access`: Limit the account to your use only (e.g., for a personal business address). Otherwise, accounts are available to anyone with edit access in your workspace.
        -   `Update send limit`: Change the daily number of emails the account can send per day
        -   `Update sender variables`: Change the sender variable values for the account
    -   **Searching and bulk actions:** Use the **search bar** and **Filter** control in `Sender accounts` to quickly find accounts by email address or name. Filter by account type (Google OAuth, Outlook, or SMTP) or status (Ready, Warming up, Not warming, or Auth error). Select multiple accounts to bulk-enable warmup or remove them from the campaign at once.
6.  Adjust your `Schedule settings`:
    -   `Timezone`: Select the timezone to send from (we recommend matching your prospects').
    -   `Days of the week`: Choose which days emails are sent.
    -   `Start/End times`: Set sending windows within the chosen timezone.
    -   `Min time between emails (min)`: Minimum gap between consecutive sends from a single account (3–30 minutes, Custom schedule only). Shorter gaps increase daily throughput; longer gaps improve deliverability.
    -   `Maximum new leads per day`: Caps the number of new leads contacted daily (in addition to account send limits).
    -   `Campaign start date` (optional): Set a future launch date, or start immediately based on your settings.
7.  Explore `Advanced settings` if needed:
    -   `Webhooks`: Route campaign events to a specific Webhook destination instead of the default Campaign Events Clay table. Example: Send Smartlead metrics to tools like OutboundSync or Enrichley for downstream routing.
    -   `Email tracking`: Configure tracking for email opens and link clicks (if HTML is enabled)
    -   `Pause leads at the same company on reply`: When a lead replies, automatically pause other leads with the same email domain. Off by default.
8.  Go to `Leads` to preview the messages for all people in your campaign
    -   `Send test email` to verify your template looks right
    -   Click the `Pencil` icon to spot-edit a message for a specific lead

## Launching your campaign

Once all your settings are saved, you can launch your campaign. Launching a campaign does the following:

-   Emails begin sending according to your schedule, following deliverability best practices.
-   The `Analytics` tab displays detailed stats for your campaign. You can refresh data manually using the button in the top right.
-   The `Replies` tab shows you any incoming replies and lets you respond to them directly in Clay
-   Actions are consumed for each email sent (1 Action per lead, plus standard Action and Data Credit rates for any AI snippets used).
-   Your campaign becomes live, which means:
    -   Any new leads routed into the campaign will automatically be sequenced, enabling "always-on" campaigns for inbound routing.
    -   All campaign settings become locked.
-   If you haven't set up custom webhooks in the `Advanced` section, a campaign events table will be created to capture all activity as it occurs.

At any point, you can pause or complete a campaign:

-   `Pause`: Stops emails from sending and allows edits to message copy and campaign settings (but not change the number of messages in the sequence). You can relaunch later without being charged additional credits for previously sequenced leads.
-   `Complete`: Permanently ends the campaign and freezes analytics. Use this option only when you're certain you won't need to sequence leads in the campaign again.

### Campaign events table

When a campaign launches, a dedicated campaign events table is created. It records key actions such as sends, bounces, and replies. Because this is a Clay table, you can build automations around these events. Reply events may appear with a 15–30 minute delay.

The events table can also be created before launching the campaign if you'd like to set up any automations in Clay.

Special sequencer enrichments available in the table include:

-   `Reply to lead`: Automate responses to any email reply event using a pre-built HTML template, AI-generated snippet, or booking link.
-   `Pause lead in campaign`: This can be called from any Clay table to pause a lead on an incoming event (e.g. event signup, or if the recipient filled in a form).
-   `Add email to blocklist`: Automatically prevent unsubscribed or removed leads from being added to future campaigns.

## Managing campaigns

You can view and manage all campaigns from the `Campaigns` tab on your home screen. This view summarizes every campaign in your workspace and shows you the workbook it belongs to.

In the Campaigns homepage, you can access the `Global inbox` which centralizes replies across all campaigns, giving you one place to review and manage every response. `Global analytics` shows you how all of your campaigns are performing.

Check out the `Email accounts` tab to manage your fleet of sender accounts and `Global blocklist` to add or remove entries.

To duplicate a campaign — for example, to reuse your message sequence and settings for a new persona or messaging variant — open the campaign you want to copy and click its name in the breadcrumb at the top. Select **Duplicate campaign** from the dropdown. Clay creates a new draft campaign named "<original name> (copy)" with the same message sequence, settings, and AI context, then opens it immediately for editing.

## Best practices

The golden rule of outreach: send emails the way you'd want to receive them. Your ultimate goal is to land in the prospect's main inbox—if your message goes to Spam or Promotions, it's unlikely to be read. Deliverability (your ability to reach that primary inbox) depends on both the quality of your messaging and the way you send it.

📖 For a deeper dive, check out [Za-zu's Cold Email Handbook](https://za-zu.com/docs/handbook/intro).

Key practices to follow:

-   Don't spam. Spam is high-volume, low-quality, and generic. Instead, use Clay to research leads at scale and send hyper-targeted, personalized offers.
-   Don't deceive. Tricks may get you a click once, but they damage trust. Instead, be upfront about your value and what you're offering.
-   Send plaintext for cold outreach. Bold text, fonts, inline images, and hyperlinks rely on HTML, which ESPs often block to fight phishing. Unless you already have an email history with the recipient, stick to plaintext.
-   Warm up your inbox. ESPs flag sudden spikes in email volume as suspicious. Gradual inbox warmup builds trust and reputation before you scale.
-   Vary your copy. Avoid sending the same message repeatedly. Use AI, Spintax, and lead-specific variables to keep your outreach fresh and personal.
-   Mimic human sending patterns. Pace emails as if each were written individually—spread them throughout the day (e.g., one every 10 minutes) with some randomness, rather than blasting them all at once.

## FAQs

### What if I already have a Smartlead account? Can I use my API key?

Our sequencer is powered by Smartlead, but everything runs on Clay credits. You don't need a Smartlead account, and you can't use an existing Smartlead API key with the sequencer. If you have a key, you can still use it with our in-table enrichments.

### Why does my campaign only show 10 leads after launching?

When a campaign is created, the `Sync lead data to campaign` column pushes 10 rows so you can preview and configure your messages. After launching, the rest of your source table is not pushed automatically. To add all remaining rows, open your source table (the table where you created the campaign — not the campaign events table) and run the `Sync lead data to campaign` column manually — click the run button in the column header.

### Why did my campaign stop sending before reaching all my leads?

The daily send limit is set at the **email account level**, not per campaign. If you have multiple active campaigns using the same email account, they all share that account's daily sending budget.

**Example:** If your email account has a limit of 20 emails per day and you're running two campaigns from the same account, those 20 sends are distributed across both campaigns — not 20 per campaign. Once the account's daily limit is reached, sending pauses for that account until the next sending window.

To increase your total daily sending capacity:
-   **Add more email accounts** — each additional account has its own independent daily budget. With two accounts you can send up to twice as many emails per day.
-   **Increase the send limit** on an existing account — open the campaign's `Sender accounts` section, click the three-dot (⋯) menu next to the account, and select `Update send limit`.

Keep in mind that sending high volumes of cold email from a single inbox puts your domain at risk. Starting near the default (20 emails/day) and scaling by adding accounts rather than increasing individual limits is safer for deliverability.

### Why are my emails queued up but not sending yet?

Several factors work together to pace delivery over multiple days rather than sending all at once:

-   **Daily send caps**: Each sender account has a configurable daily sending limit. Once an account reaches that limit, it pauses and resumes only when the next sending window opens (typically the next day). If most of your sender accounts are already at their daily limit when new leads are added, those emails won't go out until the following day.
-   **Sending window**: Your campaign's schedule settings restrict when emails can go out (timezone, start/end times, and days of the week). A narrow window — like 9 AM to 5 PM in one timezone — caps how many emails can be sent per day across all accounts.
-   **Multiple campaigns sharing sender accounts**: If the same sender accounts are used across multiple active campaigns, all those campaigns share the same daily sending budget. Adding leads to a new campaign doesn't create additional capacity — it competes for the same pool.

**To speed up delivery, you can:**

-   **Increase the send limit on existing accounts** — open the campaign's `Sender accounts` section, click the three-dot (⋯) menu next to the account, and select `Update send limit`. Keep in mind that raising individual limits aggressively can hurt deliverability; adding more accounts is generally safer for long-term inbox health.
-   **Add more sender accounts** — each additional account has its own independent daily budget.
-   **Widen your sending window** — a broader time range gives more hours per day for sends to go out.

If all your sender accounts have hit their daily limit, the campaign resumes automatically when the next sending window opens.

### How many emails can I send per day, and is the sequencer right for large-volume campaigns?

The daily send limit is set at the **email account level** and varies by account type:

-   **Self-connected accounts** (Google Workspace OAuth, Microsoft Outlook OAuth, or SMTP) default to 20 emails per day and can be adjusted from 10 to 500. Go to your campaign's `Sender accounts` section, click the three-dot (⋯) menu next to an account, and select `Update send limit`.
-   **SmartSenders accounts** purchased through Clay (currently in beta; available on Growth and Enterprise plans) have a maximum of 30 emails per day. Newly provisioned accounts start at a lower send limit and can be increased up to 30 via `Update send limit`. See [Buying email accounts](buying-email-accounts.md).

Total daily throughput scales with the number of connected accounts — each account has its own independent daily budget.

Clay's sequencer is built for **targeted, personalized sales outbound** — high-quality sequences to well-researched lists. For very large-scale sends (e.g., 1M+ contacts), a dedicated bulk or marketing email platform is generally a better fit for delivery volume. Clay works well as the enrichment and list-building layer in that setup.

### Why is the expected campaign completion time so long?

The **Expected time to complete campaign** shown at the top of Schedule settings estimates how many days it will take to reach all leads based on your sending window, per-account limits, and schedule.

The biggest lever is the **Min time between emails (min)** setting (Custom schedule only). It controls the minimum gap between consecutive sends from a single sender account, which caps that account's maximum daily output:

**Max sends per sender per day ≈ sending window (minutes) ÷ min time between emails (minutes)**

For example: an 08:00 AM–07:00 PM window is 660 minutes. With the minimum set to 20 minutes, each sender account can send at most 33 emails per day. At that rate, reaching 1,000 leads with one sender account takes roughly 30+ weekdays.

To shorten the estimated time:
-   **Lower the min time between emails** — a smaller gap increases daily sends per account. Shorter intervals can raise spam risk; the [Best practices](#best-practices) section recommends pacing sends throughout the day.
-   **Add more sender accounts** — each account adds its own independent daily capacity.
-   **Increase the account send limit** — in `Sender accounts`, click the three-dot (⋯) menu next to an account and select `Update send limit`.

### My "Sync lead data to campaign" column is showing a warning. What does it mean?

This usually means the Clay table that the column points to was deleted. Hover over the warning icon to confirm — the error reads *"Destination table was deleted. Please either restore that table from the trash, or create a new Send table data column."*

To fix it, open `Trash` from the bottom-left of your workspace sidebar, find the deleted table, and click `Restore`. The column will reconnect once the table is back.

If the table was permanently deleted from Trash and can't be recovered, create a new campaign: click `Tools` → `Exports` → `Create Clay email campaign` in your source table.

Deleting a campaign through the column header's settings (the **Delete campaign** option) is permanent — it removes the campaign from the sending platform and all associated columns with no recovery option.

### I updated my campaign, but the changes didn't save.

Be sure to press `Save settings` after making edits. Note: deleting a campaign step saves immediately without requiring a manual save click—all other edits require pressing `Save settings`.

If you added or edited a **Clean variable** and it is not appearing in your message, check that the **Fallback** field ("Simple text to display if variable is empty") is filled in — this field is required, and the variable will not save if left blank.

### Why can't I see or edit the Message sequence section?

If your campaign is active, all settings — including the Message sequence — are locked. To make edits, open the campaign's `Setup` tab and click `Pause`. Once paused, you can edit message copy and campaign settings. Note that you cannot change the total number of messages while paused — to add or remove messages, complete the campaign and create a new one.

### Why is the three-dot menu on my campaign messages greyed out after pausing?

If you've paused a campaign but the options to add or remove messages are still greyed out, it's because structural changes — adding or removing steps — are disabled once a campaign moves past draft status. Pausing only re-enables edits to message copy and campaign settings; it does not restore the ability to add or remove messages from the sequence.

**To add follow-up messages:** Create a new campaign and set up your full sequence — including all follow-up messages — from the start. You can include up to 4 messages per campaign.

### How much does the sequencer cost?

The Clay email sequencer is available on all plans. Each lead sequenced consumes 1 Action (platform orchestration work). If you use AI snippets in your messages, those consume 1 Action per run and Data Credits for AI generation in addition to the Action for sending the email.

### Can I send multiple sequences to the same email address?

Each lead can only be sequenced once per campaign. To send multiple sequences to the same email address (like [bob@example.com](mailto:bob@example.com)), create a separate campaign for each sequence. Best practice: wait at least a couple of months between sequences to the same person unless you have a completely different offer.

### What happens if my source table has two leads with the same email address?

If two leads in the same campaign share a recipient email address, Clay automatically enrolls only one of them to prevent duplicate outreach. The other lead is permanently skipped and will not be retried in future enrollment runs. In the `Leads` view, skipped contacts show the status: "Another lead with this email address is already enrolled in this campaign, so we skipped this one." Leads without an email address are not affected — they pass through to standard enrollment validation.

To avoid losing leads this way, deduplicate your source table before launching. Click any email column header → **Dedupe** to remove rows with identical email values before starting the campaign.

### My sender account got disconnected. What happened?

Email providers like Google and Microsoft occasionally revoke access due to inactivity, security checks, or suspicious activity detection. To fix this, delete the disconnected account from your sequencer settings and re-authenticate it.

### What is email account warmup?

Warmup is the process of automatically sending and receiving emails from other inboxes in Smartlead's warmup pool so your actual campaign traffic looks similar to the emails you're already sending. We recommend you keep warmup on at all times for email accounts in the sequencer to maximize deliverability.

When you add accounts via OAuth, we will automatically set up labels and filters to make it clear what emails are warmups and reduce clutter in your inbox. Your workspace has a unique two-word filter key (e.g., `clever-rocket`) that marks all warmup emails so you can apply these labels and filters.

Warmup is enabled during the account connection flow: after connecting your email account, Clay shows a prompt with all newly added accounts pre-selected for warmup. Clicking **Enable warming** activates it — warmup emails will then appear in your inbox (filed under your warmup label/filter) even if you haven't launched a campaign yet. If you enabled warmup by accident or want to stop it, go to `Campaigns` → `Email Accounts`, find the account, click the ⋯ options menu, and select **Disable warming**.

### Why did warmup turn itself off?

Warmup automatically disables when your emails are being throttled by your email provider. This protects your sender reputation. You can manually turn warmup back on from the `Sender Accounts` tab once the throttling issue is resolved.

### I'm getting an error that my email account is already in use. What does this mean?

Clay's email sequencer runs on shared Smartlead infrastructure, and Smartlead only allows each email address to be connected once across the entire system. This error most commonly appears when the email was already connected to the sequencer in **another Clay workspace** — you don't need a separate Smartlead account for this to occur. To fix it, check your other Clay workspaces: go to `Campaigns` → `Email Accounts`, locate the address, and delete it there. Once removed from the other workspace, you can add it to the current one. If you can't identify which workspace has it, contact Clay support with the email address and we'll remove it from our end.

### How do I add multiple email accounts at once?

Use the `Bulk CSV upload` option on the `Add email accounts` screen (it's a top-level choice, not nested under SMTP). Download the example template from the modal and fill in one row per account with eight columns: `from_email`, `from_name`, `user_name`, `password`, `smtp_host`, `smtp_port`, `imap_host`, `imap_port`.

For Google Workspace accounts on adjacent or alternate domains, you'll need to:
1. Enable SMTP access for each domain in your Google Workspace Admin panel (Apps → Google Workspace → Gmail → End User Access → Enable IMAP and SMTP).
2. Generate an app password for each email alias (Google Account → Security → 2-Step Verification → App passwords) and use it as the `password` column value.

### Are personal email accounts supported (e.g., Gmail, Hotmail)?

No, only business accounts (Google Workspace, Microsoft Outlook) are supported for OAuth. Personal Gmail accounts can be connected through a legacy SMTP method (see [these docs](https://helpcenter.smartlead.ai/en/articles/4-connect-gmail-with-smtp)), but this workaround may stop working if Google discontinues it.

### I saw an error toast pop up. What should I do?

Often errors in the app are transient. We're calling Smartlead APIs under the hood, and sometimes the request has an issue—usually you can retry the operation and it will succeed (especially if it says a 502 error code). If you keep running into an error, contact support.

### How do I write campaign event data back to my CRM (HubSpot or Salesforce)?

Because the campaign events table is a standard Clay table, you can add CRM enrichment columns directly to it to log activity back to HubSpot, Salesforce, or any other connected CRM. There is no separate native sync — you configure it column by column using Clay's standard CRM actions. Here are best practices for a clean, reliable write-back:

1.  **Filter by event type before writing.** Not every event needs to hit your CRM. Add an `Only run if` condition to your CRM action column to trigger write-backs only on meaningful events (e.g., replies or bounces) — this keeps your CRM clean and avoids noise from every send.

2.  **Look up the contact first.** Before creating or updating a record, use a `Lookup record` action (by email) to find the existing CRM contact. This prevents duplicates and ensures the activity is logged to the right record. For Salesforce contact or lead records, `Upsert object` can find and update in a single step (requires an external ID field on the Salesforce object).

3.  **Map your key fields.** Recommended mappings from the events table to your CRM:
    -   `Event Type` → Activity Type / Task Subject
    -   `Event Timestamp` → Activity Date
    -   `Campaign Name` → Campaign / Custom Field
    -   `Reply Body` → Notes / Description

4.  **Use Create record (not Update) when logging activity events.** Each event should become its own activity entry in your CRM — this preserves the full engagement history. Updating a single record would overwrite prior events.

5.  **Account for reply delays.** Reply events can appear in the campaign events table with a [15–30 minute delay](#campaign-events-table), so avoid automations that depend on real-time reply data.

6.  **Enable Auto-run for ongoing campaigns.** Turn on `Auto-run` on your CRM action column so new events continuously trigger write-backs as the campaign runs — otherwise, the column only processes rows that are manually triggered.

7.  **Test before scaling.** Turn off `Auto-run` and manually run 5–10 rows first to validate your field mappings before enabling full automation.

### How do unsubscribes work in the sequencer?

When HTML is enabled, you can turn on an unsubscribe link in `Advanced` settings. This adds a hyperlinked phrase at the bottom of every email (default text: "Not interested? Click here to unsubscribe."). You can customize this text in the `Advanced` section.

**What happens when a recipient clicks unsubscribe:**

-   Their email address is automatically added to your workspace's global blocklist.
-   They are removed from all active campaigns.
-   Future emails to that address from any campaign in your workspace are blocked.

To view and manually manage your blocklist—including adding individual email addresses or domains—go to the **Campaigns** tab on your home screen and click the `Blocklist` tab. You can also block leads programmatically using the `Add email to blocklist` enrichment in the campaign events table.

**What about leads who reply asking not to be contacted?**

If a lead *replies* to your email — rather than clicking an HTML unsubscribe link — their response is categorized by Smartlead (e.g., as `Do Not Contact` or `Not Interested`), but they are **not** automatically added to the blocklist. The `Add email to blocklist` column in the campaign events table is a button by default: you can click it manually for a specific row, or automate it by setting an `Only run if` condition on the column. To trigger the blocklist action for reply-based opt-outs, set the condition to run when `Event type` equals `LEAD_CATEGORY_UPDATED` — this event fires whenever Smartlead categorizes a lead's reply. See [How are replies categorized in the Campaign Events table?](#how-are-replies-categorized-in-the-campaign-events-table) for the full list of reply categories.

### What is a cold lead? What is a warm lead?

A cold lead is someone who doesn't already know about your business and you. A warm lead is someone who has already responded to your email or expressed interest in some other way. The kinds of emails you send to each type are completely different—you can send a lot more emails from your main domain to warm leads than you can to cold leads.

### What exact Gmail permissions does sequencer require?

These are disclosed when you add your account via OAuth. Clay requests the following scopes:

-   `openid` — OpenID Connect identity token
-   `https://www.googleapis.com/auth/userinfo.email` — read the user's email address
-   `https://www.googleapis.com/auth/userinfo.profile` — read the user's basic profile (name, avatar)
-   `https://mail.google.com/` — full Gmail access (read, send, delete, manage)
-   `https://www.googleapis.com/auth/gmail.settings.basic` — read/manage Gmail settings (filters, send-as aliases, etc.)

Additionally, you will need to have a Google Workspace admin authorize our app to request these permissions for the domain(s) you want to add to the sequencer.

### I'm seeing "Access blocked: clay.com has not completed the Google verification process" when I try to connect my Google account. What does this mean?

This error is expected — Clay's sequencer uses automated warmup sends, which prevents it from passing Google's standard app verification process. It does not mean Clay is broken or untrustworthy. The fix is for your **Google Workspace admin** to authorize Clay Sequencer as a Trusted app in your Google Admin panel. Until they do, all users in your domain will see this error when attempting to connect via OAuth.

To resolve it, have your admin follow the steps in [Connecting Google Workspace via OAuth](#connecting-google-workspace-via-oauth). Changes can take up to 24 hours to apply.

If your admin has already completed those steps and you still see the error, see [I followed the admin setup steps but still see "Access blocked"](#i-followed-the-admin-setup-steps-but-still-see-access-blocked-claycoms-has-not-completed-the-google-verification-process-what-should-i-do).

### How do I authorize Clay's app in the Google Admin panel?

Follow the instructions in the modal and have your Google Workspace admin set our Clay sequencer app to `Trusted` — not `Specific Google Data`. When searching in Google Admin, the app is listed as **Clay Sequencer (Web)** — the `(Web)` suffix indicates the web client type and refers to the same Clay Sequencer app. Selecting `Specific Google Data` will not grant all the permissions Clay needs, and the access error will persist. Despite its name, `Trusted` only allows Clay to request Gmail-specific permissions (full email access, basic email settings, OpenID, and your profile) — it does not grant access to Google Drive, Calendar, Docs, or any other Google service. It can take up to 24 hours for Google to recognize the update; once it's taken hold, all accounts in your domain (e.g., [example.com](http://example.com)) can now add themselves to the Clay sequencer.

### I followed the admin setup steps but still see "Access blocked: clay.com has not completed the Google verification process." What should I do?

This error is expected — Clay's sequencer uses automated warmup sends, which prevents the app from passing Google's standard verification process. Admin approval in your Google Workspace Admin panel is the intended workaround; Clay's app will not become Google-verified.

If the error persists more than 24 hours after your admin marked the app as `Trusted`, confirm that they approved the app for the exact domain of the email account you're connecting (e.g., for `ryan@company.com`, the admin must approve for `company.com` specifically — not a different domain they manage). If you're connecting accounts from multiple domains, each domain requires its own separate Trusted configuration — having one domain approved does not automatically cover the others. Your admin can verify which org units are currently configured by going to Google Admin → Security → API Controls → App Access Control and checking the Clay Sequencer app's org unit count. If it's still blocked after verifying the domain, contact support.

### What exact Microsoft permissions does sequencer require?

These are disclosed when you add your account via OAuth. We request: offline\_access, openid, email, profile, Mail.Send, Mail.Send.Shared, Mail.ReadWrite, Mail.ReadWrite.Shared, [User.Read](http://User.Read), MailboxSettings.ReadWrite.

### How are replies categorized in the Campaign Events table?

Smartlead assigns leads into one of the following categories:

1.  Interested
2.  Meeting Request
3.  Not Interested
4.  Do Not Contact
5.  Information Request
6.  Out Of Office
7.  Wrong Person
8.  Uncategorizable by Ai
9.  Sender Originated Bounce

### How do I handle replies from leads?

Replies are available in the `Replies` tab of your campaign and in the campaign events table. You can reply directly from Clay using the `Reply to lead` enrichment in the campaign events table.

### Why does the reply body show HTML instead of plain text?

This is expected. When a lead replies using an HTML-capable email client like Microsoft Outlook, the reply arrives in HTML format. The `Reply Message` field in your campaign events table includes two sub-fields:

-   `Html`: the raw HTML body as sent by the lead's email client
-   `Text`: a plain text version of the same content

To work with the reply as clean text — for example, when mapping it to a CRM note or passing it to an AI action — use the `Text` sub-field instead. If you prefer to use `Html` and strip the tags, add a formula column to do so.

### Useful links

-   [Smartlead documentation](https://helpcenter.smartlead.ai/)
-   [Buying email accounts in Clay](buying-email-accounts.md)
-   [Clay email sequencer pricing](https://www.clay.com/pricing)
-   [Clay community forum](https://community.clay.com/)
