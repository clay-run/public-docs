---
title: Email sequencer
description: Run outbound campaigns directly from your table.
last_synced: 2026-09-01T01:27:12.565Z
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
    -   `Enable HTML`: Campaigns default to plaintext for better deliverability. Enable HTML if you want to use formatting features like fonts, bold text, and hyperlinks. This also unlocks advanced settings such as open tracking, click tracking, and unsubscribe links.
4.  Under `Message sequence`, draft and customize your emails (up to 4 per campaign). Sequences automatically stop when all emails are sent or when a lead replies (excluding out-of-office replies, which we detect and work around).
    -   Toggle `Preview` mode to see real data from your source table in the message template. When HTML is enabled, Preview also renders how your formatting will appear in the recipient's inbox — the message editor shows the content structure you've built, not the final rendered output, so use Preview to verify formatting before sending.
    -   Within each message, use `/` to access features such as:
        -   `Clean variable`: Reference synced lead data with safe fallbacks and optional formatting. When configuring a Clean variable, the **Fallback** field ("Simple text to display if variable is empty") is required — the variable will not save if left blank.
        -   `Sender variable`: Reference identifying information from the sending account
        -   `AI snippet`: Generate personalized copy for each lead automatically. After inserting an AI snippet via `/`, a snippet chip appears in your message. Click the chip to open the inline prompt editor — describe what the snippet should generate and reference lead data columns in your instructions (for example: *"Write a one-sentence opening based on [Company Domain] and [Job Title]"*). Toggle **Preview** to see the AI-generated output for your current preview lead in real time and refine the prompt as needed. The AI model is configured at the campaign level, not per snippet; if you need to control which AI model generates the copy, build the personalized content in a **Use AI** column in your source table and reference it as a `Clean variable` in the email template instead.
        -   `Spintax variable`: Choose a random value from a list
        -   `Rows from [Table]`: Directly reference synced data (Clean variables are recommended to handle empty values safely).
        -   (HTML only): If enabled, use hyperlinks, inline images, fonts, and rich text formatting.
5.  Go to `Settings` to add your email account:
    -   `Google OAuth` (recommended): Connect your Google Workspace account via OAuth.
        -   ⚠️ Note: You or your Google Workspace admin must authorize Clay Sequencer as a Trusted app for your domain before connecting. If you or a teammate sees **"Access blocked: clay.com has not completed the Google verification process" (Error 403: access_denied)** when connecting, follow [Connecting Google Workspace via OAuth](#connecting-google-workspace-via-oauth) for the required admin setup steps. Until this is done, all users in your domain will see this error.
    -   `Microsoft Outlook OAuth` (recommended): Connect your Outlook account via OAuth.
        -   ℹ️ Note: Unlike Google OAuth, no Clay-side admin setup is required upfront. If your Microsoft 365 / Entra tenant requires admin approval for third-party apps, your admin may need to grant consent for "Clay Sequencer – Smartlead" in the [Microsoft Entra Admin Center](https://entra.microsoft.com).
    -   `SMTP`: Connect a single account via SMTP credentials directly. The form requires both SMTP settings (host, port, username, password) and IMAP settings (host, port) — Clay does not provide a built-in inbox, so your IMAP credentials must come from an existing IMAP-capable mailbox under your domain (such as Google Workspace, Microsoft 365, Zoho, or Fastmail). If your sending service is send-only (for example, SendGrid or another transactional email relay), you must pair it with a separate IMAP-enabled mailbox.
    -   `Bulk CSV upload`: Add multiple accounts at once by uploading a CSV. Download the example template from the modal and fill in the following eight columns for each account: `from_email`, `from_name`, `user_name`, `password`, `smtp_host`, `smtp_port`, `imap_host`, `imap_port`. For Google Workspace accounts, generate an app password for each account (Google Account → Security → 2-Step Verification → App passwords) and use it as the `password` value.
    -   You can also [buy email accounts directly in Clay](https://university.clay.com/docs/buying-email-accounts) if you want to increase your sending capacity.
    -   After setup, you can:
        -   `Enable warmup`: Sends and receives automated emails from the linked account to build reputation. Each account uses a unique two-word keyphrase (e.g., `clever-rocket`) to identify warmup emails. Follow the in-app instructions to set up a label and filter to easily ignore warmup messages.
        -   `Restrict access`: Limit the account to your use only (e.g., for a personal business address). Otherwise, accounts are available to anyone with edit access in your workspace.
        -   `Update send limit`: Change the daily number of emails the account can send per day
        -   `Update sender variables`: Change the sender variable values for the account
    -   **Searching and bulk actions:** Use the **search bar** and **Filter** control in `Sender accounts` to quickly find accounts by email address or name. Filter by account type (Google OAuth, Outlook, or SMTP) or status (Ready, Warming up, Not warming, or Auth error). Select multiple accounts to bulk-enable warmup or remove them from the campaign at once.
    -   **Assign sender account field to lead (optional):** At the bottom of the `Sender accounts` section, you can optionally map a column to assign a specific sending account to each lead. When this field is set, Clay uses the email address in that column as the sender for each lead — that address must match one of the sender accounts already configured in the campaign. If the mapped column contains an email that is not a configured sender account, that lead's row in the `Sync lead data to campaign` column will fail with a validation error when it runs. Leads where the column is blank (no value) are distributed evenly across all configured sender accounts. If you are not deliberately routing leads to specific senders, leave this field empty.
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
-   `Add email to blocklist`: Stop an email address from receiving emails across all campaigns in your workspace — including any campaigns that address is currently active in.
-   `Forward lead email in campaign`: Route an email thread from the global inbox to any email address — including addresses outside Clay (recipients do not need a Clay seat). Map Campaign ID and Lead ID from the event row, set Recipient email addresses to the target inbox, and add a run condition so it only fires on `EMAIL_REPLY` events.

## Managing leads in campaigns

The `Leads` tab in your campaign lists every lead synced into it, along with a `Lead status` column showing where each lead sits in the sequence. What you can do to an individual lead depends on whether the campaign has launched yet.

### Removing a lead before launch

While a campaign is still a draft, you can take leads out of it completely:

1.  Go to the `Leads` tab in your campaign.
2.  Hover over the lead's row and click the three-dot (⋮) menu on the right.
3.  Select `Remove from campaign`.

To remove several leads at once, select them and click `Remove [n] leads from campaign`.

**Note:** Removal is immediate — there is no confirmation step, and it can't be undone. Leads are only removed from the campaign; their rows stay in the source table they were synced from.

### Pausing a lead in a launched campaign

After a campaign launches, `Remove from campaign` is no longer offered. Pause the lead instead:

1.  Go to the `Leads` tab in your campaign.
2.  Hover over the lead's row and click the three-dot (⋮) menu on the right.
3.  Select `Pause lead`.

Pausing stops further emails to that lead while the rest of the campaign keeps running, and the same menu shows `Resume lead` once a lead is paused. To act on several leads at once, select them and click `Pause [n] leads` or `Resume [n] leads` — that button is disabled when your selection mixes active, paused, and completed leads.

The same menu also offers `Show in leads table`, which opens the lead's row in the table it was synced from, and `Send test email`.

### Lead statuses

The `Lead status` column is populated by the sequencing provider behind the campaign, so leads don't carry a status until the campaign launches and they're handed off — there's no separate "pending launch" state to look for. Once sequencing begins, the values you'll see are `STARTED`, `INPROGRESS`, `PAUSED`, `COMPLETED`, `STOPPED`, and `BLOCKED`.

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

To estimate how many inboxes you need, divide your target daily send count by 20–30 — the recommended per-inbox range for cold outreach. For example, to send 200–300 emails per day, connect roughly 8–15 inboxes, each sending 20–30 emails per day. While self-connected accounts can technically be raised up to 500 emails per day, distributing volume across multiple inboxes at 20–30 each is safer for long-term deliverability than maxing out a single inbox. If you are adding new inboxes to increase capacity, [warm them up first](#what-is-email-account-warmup) — warmup typically takes 2–3 weeks before a new account reaches full sending capacity.

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

### Why doesn't my Claygent or AI column appear as a variable in the email template?

Claygent (web research AI) columns store their output as a structured object with multiple sub-fields — Response, Reasoning, Confidence, Steps Taken, and others. Even if the column appears in the email template's variable picker, its value renders as raw JSON rather than the clean text you want. To get just the response text as a usable personalization variable, extract it to a standalone plain-text column first.

To use the AI output as a personalization variable in your message sequence:

1. In your source table, click a populated cell in the Claygent column to open the cell details panel.
2. Hover over the **Response** value — an **Add to column** button appears.
3. Click **Add to column** and give the new column a name (for example, "First Name").
4. Re-run the `Sync lead data to campaign` column in your source table so the new column's data is pushed to the campaign.
5. Open the campaign's **Message sequence**, type `/` where you want the personalization, select **Clean variable**, and pick the new column from the list.

**Editing a live campaign:** If your campaign is already running, you must pause it before changing the message template — open the campaign's `Setup` tab and click **Pause**. Make your edits to the message sequence, then relaunch the campaign.

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

### How do I switch my campaign's sending email to a new provider or address?

If you've moved to a new email provider (for example, switching from a third-party address to Google Workspace), update your Clay campaigns in these steps:

1.  **Connect the new email account.** Go to `Campaigns` → `Email Accounts` → `Add email accounts` and choose the connection method for your new provider:
    -   Google Workspace: select `Gmail (OAuth)`. If you see an "Access blocked" error, your Google Workspace admin must first authorize Clay Sequencer for your domain — follow the steps in [Connecting Google Workspace via OAuth](#connecting-google-workspace-via-oauth).
    -   Microsoft Outlook: select `Microsoft Outlook OAuth`.
    -   Other providers (including third-party email hosting): select `SMTP` and enter your SMTP and IMAP credentials.
2.  **Enable warmup on the new account.** The new account starts warmup from scratch — the initial phase typically takes 2–3 weeks before the account shows as **Ready**. Enable warmup right after connecting to start building sender reputation.
3.  **Update your campaigns.** Open each active campaign that used the old sending account. In the `Sender accounts` tab, add the new account, then use the ⋯ menu next to the old account to remove it.

### What is email account warmup?

Warmup is the process of automatically sending and receiving emails from other inboxes in Smartlead's warmup pool so your actual campaign traffic looks similar to the emails you're already sending. We recommend you keep warmup on at all times for email accounts in the sequencer to maximize deliverability.

The initial warmup phase typically takes **2–3 weeks**, during which the account's status shows as **Warming up** in Campaigns → Email Accounts. Once the initial phase completes, the status switches to **Ready**. Warmup emails continue to run in the background even after the status shows **Ready** — the Ready label means the account has been warming for at least 2 weeks and is ready for campaigns, not that warmup has stopped.

When you add accounts via OAuth, we will automatically set up labels and filters to make it clear what emails are warmups and reduce clutter in your inbox. Your workspace has a unique two-word filter key (e.g., `clever-rocket`) that marks all warmup emails so you can apply these labels and filters.

During warmup, your inbox will receive emails from other accounts in Smartlead's warmup pool. These emails often look random or spam-like in content — this is intentional, as the warmup engine simulates natural human email activity. They are automatically filed under your warmup label (named **Clay sequencer warmup email**), so they won't clutter your main inbox. Receiving them is not a sign of unauthorized account access or phishing activity.

Warmup is enabled during the account connection flow: after connecting your email account, Clay shows a prompt with all newly added accounts pre-selected for warmup. Clicking **Enable warming** activates it — warmup emails will then appear in your inbox (filed under your warmup label/filter) even if you haven't launched a campaign yet. If you enabled warmup by accident or want to stop it, go to `Campaigns` → `Email Accounts`, find the account, click the ⋯ options menu, and select **Disable warming**.

### What does the Reputation percentage mean?

The **Reputation** percentage shown next to each email account in `Campaigns → Email Accounts` is the percentage of warm-up emails from that mailbox that landed in the inbox — not in spam or promotions. It reflects how successfully that specific warmed mailbox is delivering warm-up emails through Smartlead's warmup pool.

A high Reputation score (for example, 100%) means the vast majority of warm-up sends for that mailbox are reaching the inbox. This is a useful directional health signal for the warmup process itself. It is **not** an authoritative, provider-level domain-reputation score from Google Postmaster Tools, Microsoft SNDS, or similar services — those reflect your actual campaign traffic, not the simulated warmup activity.

### Why did warmup turn itself off?

Warmup automatically disables when your emails are being throttled by your email provider. This protects your sender reputation. You can manually turn warmup back on from the `Sender Accounts` tab once the throttling issue is resolved.

### Can I send campaign emails from an inbox that shows "Warming up"?

Yes — a **Warming up** inbox is not blocked from campaign sending. However, it is not recommended. The 3-week warmup period builds your sender reputation with email providers; sending before warmup completes risks lower deliverability and emails landing in spam. If you do send before warmup finishes, keep daily volume low to minimize the impact on your domain reputation.

The only status that triggers a warning in the campaign UI is **Auth error** — that indicates a connection problem that needs to be resolved before that inbox can send reliably. **Warming up** and **Not warming** inboxes carry no campaign-level block or warning.

Once the 3-week warmup period is complete, the status automatically changes to **Ready**, signaling the inbox is ready for full campaign volume.

### How can I tell how much longer my inbox needs to warm up?

There is no countdown timer or progress indicator in the UI showing time remaining in warmup. To estimate when warmup will complete, note the date you connected the account and enabled warmup — the initial warmup phase is 3 weeks from that point. Once that window passes, the status automatically switches from **Warming up** to **Ready**.

### I'm getting an error that my email account is already in use. What does this mean?

Clay's email sequencer runs on shared Smartlead infrastructure, and Smartlead only allows each email address to be connected once across the entire system. This error most commonly appears when the email was already connected to the sequencer in **another Clay workspace** — you don't need a separate Smartlead account for this to occur. To fix it, check your other Clay workspaces: go to `Campaigns` → `Email Accounts`, locate the address, and delete it there. Once removed from the other workspace, you can add it to the current one. If you can't identify which workspace has it, contact Clay support with the email address and we'll remove it from our end.

### Why was my campaign email sent from a different sender account than I expected?

If your emails are going out from an unexpected account, the most likely cause is that the **Assign sender account field to lead** setting has not been configured in the campaign's **Sender accounts** tab. When this field is not set, Clay distributes leads evenly across all configured sender accounts — even if your source table has a column that specifies which sender each lead should use, that column has no effect on the campaign until you explicitly map it here.

**To route each lead to a specific sender:**

1. Open the campaign's **Sender accounts** tab.
2. Scroll to the bottom and find **Assign sender account field to lead (optional)**.
3. Click the field and select the column in your source table that contains the sending account's email address for each lead. The values in that column must match one of the sender accounts already configured in the campaign.
4. Click **Save settings**. Future sends will use each lead's designated sender account. Leads whose column value is blank are distributed evenly across all configured accounts.

### Why are some leads failing with "Sender email address is not a configured sender account in this campaign"?

This error fires in the `Sync lead data to campaign` column when the **Assign sender account field to lead** setting (in the `Sender accounts` tab) is mapped to an email column, and the email address in that column for a lead does not match any of the sender accounts configured in your campaign.

Two common causes:

-   **Wrong column mapped:** The field is mapped to a column that contains your leads' own email addresses (such as a "Personal Email" column) rather than a column that holds one of your configured sender email addresses.
-   **Case mismatch:** The column contains the correct sender address but with different capitalization — for example, `John.Smith@example.com` in your table vs. `john.smith@example.com` as the registered account. Matching is case-sensitive, so even a single capital letter causes this error.

**To fix it:**

-   **If you do not intend to route specific leads to specific senders:** Remove the field mapping — open the `Sender accounts` tab, scroll to the `Assign sender account field to lead` section, and clear the selection. Leads will then be distributed evenly across all your configured sender accounts. After clearing it, re-run the `Sync lead data to campaign` column for the affected rows to re-enroll them.
-   **If you are using the wrong column:** Make sure the column you selected contains one of your configured sending account email addresses — not the lead's own email. Add those sender accounts to the campaign first if they are not already there, then re-run the `Sync lead data to campaign` column.
-   **If the issue is a case mismatch:** Add a formula column in your source table — enter `{{Your Sender Email Column}}.toLowerCase()` — and select that column in **Assign sender account field to lead** instead. Re-run the `Sync lead data to campaign` column for the affected rows.

### Can I connect a third-party email provider (such as LiteMail) as a sender account?

Yes — Clay's email sequencer sends campaigns directly and supports any email provider that supplies SMTP credentials, not just Google Workspace or Microsoft Outlook. The **Sender accounts** tab in your campaign is where you add all sending inboxes.

To connect a provider like LiteMail:

1.  In your campaign, go to the **Sender accounts** tab (or `Campaigns → Email Accounts` globally).
2.  Click **Add email accounts** and select **SMTP**.
3.  Enter the SMTP credentials your provider supplies: host, port, username, and password.
4.  Enter your **IMAP credentials** (host and port) — Clay uses these to surface replies from recipients inside the platform. Most business email providers include IMAP access alongside SMTP.
5.  Click **Add account**. The inbox appears in your Sender accounts list with its own independent daily sending limit.

Use **SMTP** for any provider that isn't Google Workspace (use Google OAuth) or Microsoft Outlook (use Outlook OAuth). See [What fields does the SMTP connection form require?](#what-fields-does-the-smtp-connection-form-require) for the full list of required fields.

### What fields does the SMTP connection form require?

The manual SMTP form requires credentials in two sections:

-   **SMTP settings** (for sending): SMTP host, port, username, password, and encryption type (SSL, TLS, or None).
-   **IMAP settings** (for receiving): IMAP host, port, and encryption type.

Both sections must be filled in before you can add the account. Clay does not provide a built-in inbox — IMAP credentials must come from an IMAP-capable mailbox you already have with a provider such as Google Workspace, Microsoft 365, Zoho, or Fastmail. Clay uses the IMAP connection to surface replies from recipients inside the platform, but the inbox itself stays with your email provider.

If your sending service is SMTP-only and does not include IMAP (for example, SendGrid or another transactional email relay), you must pair it with a separate IMAP-enabled mailbox under your domain.

### Can I use SendGrid as a sending account?

Yes. SendGrid provides an SMTP relay that works with Clay's manual SMTP connection. In the manual SMTP form, enter:

1.  **SMTP host**: `smtp.sendgrid.net`
2.  **SMTP port**: `587`
3.  **SMTP type**: TLS
4.  **Username**: `apikey` — type this literally; it is not your SendGrid account name or email address.
5.  **Password**: your SendGrid API key with the **Mail Send** permission enabled.

Because SendGrid is a send-only relay, you must also fill in the **IMAP section** with credentials from a separate IMAP-capable mailbox under your domain (for example, a Google Workspace or Microsoft 365 inbox). Without an IMAP connection, Clay cannot track replies from your recipients.

### How do I add multiple email accounts at once?

Use the `Bulk CSV upload` option on the `Add email accounts` screen (it's a top-level choice, not nested under SMTP). Download the example template from the modal and fill in one row per account with eight columns: `from_email`, `from_name`, `user_name`, `password`, `smtp_host`, `smtp_port`, `imap_host`, `imap_port`.

For Google Workspace accounts on adjacent or alternate domains, you'll need to:
1. Enable SMTP access for each domain in your Google Workspace Admin panel (Apps → Google Workspace → Gmail → End User Access → Enable IMAP and SMTP).
2. Generate an app password for each email alias (Google Account → Security → 2-Step Verification → App passwords) and use it as the `password` column value.

### Does connecting via OAuth automatically add my email aliases?

No — connecting a mailbox via OAuth only adds the specific email account you authenticate with. Email aliases associated with that account are **not** automatically connected as separate sender accounts. Warmup and campaign rotation apply per connected account, so aliases you haven't explicitly added do not participate in sending or warmup.

To use an alias as a distinct sender, connect it as its own account:

-   **SMTP:** Go to `Settings` → `Add email accounts` → `SMTP`. Set the "From" email to the alias address and enter your primary account's server credentials (username, password, SMTP host, and port).
-   **Bulk CSV upload:** Use the `Bulk CSV upload` option to add multiple aliases at once. Set each row's `from_email` to the alias address and fill in the remaining SMTP and IMAP fields using your primary account's server settings.

**For Microsoft 365 aliases:** The SMTP and bulk CSV paths work with Microsoft 365, provided your tenant has SMTP AUTH enabled and the alias has "Send As" permissions configured in your Microsoft 365 admin settings.

**Note:** If your aliases are simple forwarding addresses that route to the same underlying mailbox (rather than independent inboxes with their own SMTP access), connecting them separately does not increase your total daily sending capacity — they share the same inbox. To scale sending volume, add accounts that each have a dedicated inbox. See [Buying email accounts](buying-email-accounts.md) for a faster path to additional inboxes.

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

**Note on test emails:** When you use `Send test email` to preview your campaign, the unsubscribe link text appears at the bottom of the email but is not an active link — the real unsubscribe URL is only injected when an actual campaign email is sent to a recipient. This is expected behavior. To confirm the unsubscribe link works, send a live campaign email to a test address you control rather than using the test email feature.

**What happens when a recipient clicks unsubscribe:**

-   Their email address is automatically added to your workspace's global blocklist.
-   They are removed from all active campaigns.
-   Future emails to that address from any campaign in your workspace are blocked.

To view and manually manage your blocklist—including adding individual email addresses or domains—go to the **Campaigns** tab on your home screen and click the `Blocklist` tab. You can also block leads programmatically using the `Add email to blocklist` enrichment in the campaign events table.

**What about leads who reply asking not to be contacted?**

If a lead *replies* to your email — rather than clicking an HTML unsubscribe link — their response is categorized by Smartlead (e.g., as `Do Not Contact` or `Not Interested`), but they are **not** automatically added to the blocklist. The `Add email to blocklist` column in the campaign events table is a button by default: you can click it manually for a specific row, or automate it by setting an `Only run if` condition on the column. To trigger the blocklist action for reply-based opt-outs, set the condition to run when `Event type` equals `LEAD_CATEGORY_UPDATED` — this event fires whenever Smartlead categorizes a lead's reply. See [How are replies categorized in the Campaign Events table?](#how-are-replies-categorized-in-the-campaign-events-table) for the full list of reply categories.

### What happens if I manually add a lead to the Global Blocklist while they're already in an active campaign?

Adding an email address to the Global Blocklist stops that address from receiving emails from **all** campaigns in your workspace — including leads already mid-campaign. No separate pause step is required. Emails already in Smartlead's immediate outgoing queue at the moment you add the address (typically within the next few minutes before a scheduled send time) may still be delivered, but no further emails are queued after the blocklist takes effect.

### What happens when an email to a lead bounces?

A bounce is recorded as an `EMAIL_BOUNCE` event in your campaign events table, but the sequence does **not** automatically stop or pause for that lead — bounces do not trigger the same auto-stop behavior as replies. Remaining emails in the sequence continue to send unless you take action.

To handle bounces automatically, add an `Only run if` condition to the relevant enrichment columns in your campaign events table:
- **Pause lead in campaign** — set the condition to `Event type = EMAIL_BOUNCE` to automatically pause a bounced lead's remaining sequence steps.
- **Add email to blocklist** — use the same condition to prevent future emails to that address across all campaigns in your workspace.

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

If you need to start sending right away while waiting for the admin change to take effect, you can connect your email account via **SMTP** instead — go to your campaign's `Settings` → `Add email accounts` → `SMTP`.

If your admin has already completed those steps and you still see the error, see [I followed the admin setup steps but still see "Access blocked"](#i-followed-the-admin-setup-steps-but-still-see-access-blocked-claycoms-has-not-completed-the-google-verification-process-what-should-i-do).

### How do I authorize Clay's app in the Google Admin panel?

Follow the instructions in the modal and have your Google Workspace admin set our Clay sequencer app to `Trusted` — not `Specific Google Data`. When searching in Google Admin, the app is listed as **Clay Sequencer (Web)** — the `(Web)` suffix indicates the web client type and refers to the same Clay Sequencer app. Selecting `Specific Google Data` will not grant all the permissions Clay needs, and the access error will persist. Despite its name, `Trusted` only allows Clay to request Gmail-specific permissions (full email access, basic email settings, OpenID, and your profile) — it does not grant access to Google Drive, Calendar, Docs, or any other Google service. It can take up to 24 hours for Google to recognize the update; once it's taken hold, all accounts in your domain (e.g., [example.com](http://example.com)) can now add themselves to the Clay sequencer.

### Does the Trusted admin setting give Clay access to all Google accounts in my domain?

No — the Trusted setting is not domain-wide delegation. Marking Clay Sequencer as Trusted in the Google Workspace Admin Console removes the verification block that would otherwise prevent users in your domain from connecting their accounts, but it does not give Clay access to any mailbox automatically. Each person who wants to use the sequencer must still connect their own Google account individually: go to `Campaigns` → `Email Accounts` → `Add email accounts` → `Google OAuth` and complete the OAuth flow for their own account. Clay can only access a mailbox after that individual user explicitly authorizes it.

### I followed the admin setup steps but still see "Access blocked: clay.com has not completed the Google verification process." What should I do?

This error is expected — Clay's sequencer uses automated warmup sends, which prevents the app from passing Google's standard verification process. Admin approval in your Google Workspace Admin panel is the intended workaround; Clay's app will not become Google-verified.

If the error persists more than 24 hours after your admin marked the app as `Trusted`, confirm that they approved the app for the exact domain of the email account you're connecting (e.g., for `ryan@company.com`, the admin must approve for `company.com` specifically — not a different domain they manage). If you're connecting accounts from multiple domains, each domain requires its own separate Trusted configuration — having one domain approved does not automatically cover the others. Your admin can verify which org units are currently configured by going to Google Admin → Security → API Controls → App Access Control and checking the Clay Sequencer app's org unit count. If it's still blocked after verifying the domain, contact support.

### What exact Microsoft permissions does sequencer require?

These are disclosed when you add your account via OAuth. We request: offline\_access, openid, email, profile, Mail.Send, Mail.Send.Shared, Mail.ReadWrite, Mail.ReadWrite.Shared, [User.Read](http://User.Read), MailboxSettings.ReadWrite.

### How can I tell if a lead has finished a campaign sequence?

Clay's campaign events table doesn't include a dedicated "sequence completed" event type. You can infer whether a lead has finished the sequence using two signals:

-   **They replied** — when a lead replies to any email, an `EMAIL_REPLY` event is recorded and the sequence automatically stops for that lead. Check whether any row in the campaign events table for that lead has `Event type = EMAIL_REPLY`.
-   **They received all emails** — each `EMAIL_SENT` event includes a `sequence_number` value nested inside the Campaign event data. When this number equals the total steps in your campaign, the lead has received all emails without replying. Click a Campaign event cell, find the `sequence_number` field in the Cell details panel, and click **Add as column** to extract it into a standalone column you can filter on.

To check this from your leads table, add a **Lookup rows in other table** column pointing to your campaign events table, matching on email address. You can then use a formula column to evaluate whether any matched event has `Event type = EMAIL_REPLY`, or whether the extracted sequence number equals your campaign's total step count.

### How are replies categorized in the Campaign Events table?

Each time a reply is categorized, a `LEAD_CATEGORY_UPDATED` event is written to the campaign events table. Categorization happens two ways: a user or teammate selects a category from the dropdown in the campaign's **Replies** tab or global inbox, or AI auto-categorization assigns a label automatically (enabled for all campaigns by default). Sends and sequence steps do not trigger this event — it only fires when a reply's category is set or changed.

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
