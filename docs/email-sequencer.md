---
title: Email sequencer
source_url: https://university.clay.com/docs/email-sequencer
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
9.  Review the summary and click `Finish`.
10.  Back in Clay, click `Continue` in the modal, then click `Connect your Google account` and complete the OAuth sign-in.

## Create a new email campaign

1.  Start in a table that contains the lead emails you want to contact.
    -   If you haven't done this yet, click `Actions` → `Import` to add emails from a third party or CSV.
2.  Click `Tools` → `Exports` → `Create Clay email campaign`
    -   The `Sync leads to campaign` column automatically pushes 10 rows from your parent table into the campaign to draft with
    -   Tip: You can customize the sync data column to only send leads with an email address using `Only run if`.
3.  In the `Setup` tab, you can set:
    -   `Lead email address`: We automatically detect email address columns, but confirm this before proceeding.
    -   `Enable HTML`: Campaigns default to plaintext for better deliverability. Enable HTML if you want to use formatting features like fonts, bold text, and hyperlinks. This also unlocks advanced settings such as open tracking, click tracking, and unsubscribe links.
4.  Under `Message sequence`, draft and customize your emails (up to 4 per campaign). Sequences automatically stop when all emails are sent or when a lead replies (excluding out-of-office replies, which we detect and work around).
    -   Toggle `Preview` mode to see real data from your source table in the message template
    -   Within each message, use `/` to access features such as:
        -   `Clean variable`: Reference synced lead data with safe fallbacks and optional formatting.
        -   `Sender variable`: Reference identifying information from the sending account
        -   `AI snippet`: Generate copy automatically using lead data.
        -   `Spintax variable`: Choose a random value from a list
        -   `Rows from [Table]`: Directly reference synced data (Clean variables are recommended to handle empty values safely).
        -   (HTML only): If enabled, use hyperlinks, inline images, fonts, and rich text formatting.
5.  Go to `Settings` to add your email account:
    -   `Google OAuth` (recommended): Connect your Google Workspace account via OAuth.
        -   ⚠️ Note: You or your Workspace admin must authorize the Clay sequencer app for your domain, or you'll see an access error.
    -   `Microsoft Outlook OAuth` (recommended): Connect your Outlook account via OAuth.
        -   ⚠️ Note: You or your Workspace admin must authorize the Clay sequencer app for your domain, or you'll see an access error.
    -   `SMTP` (manual or CSV upload): Connect via SMTP credentials directly.
    -   You can also [buy email accounts directly in Clay](https://university.clay.com/docs/buying-email-accounts) if you want to increase your sending capacity.
    -   After setup, you can:
        -   `Enable warmup`: Sends and receives automated emails from the linked account to build reputation. Each account uses a unique two-word keyphrase (e.g., `clever-rocket`) to identify warmup emails. Follow the in-app instructions to set up a label and filter to easily ignore warmup messages.
        -   `Restrict access`: Limit the account to your use only (e.g., for a personal business address). Otherwise, accounts are available to anyone with edit access in your workspace.
        -   `Update send limit`: Change the daily number of emails the account can send per day
        -   `Update sender variables`: Change the sender variable values for the account
6.  Adjust your `Schedule settings`:
    -   `Timezone`: Select the timezone to send from (we recommend matching your prospects').
    -   `Days of the week`: Choose which days emails are sent.
    -   `Start/End times`: Set sending windows within the chosen timezone.
    -   `Minimum time between sends`: Adjustable from 5–30 minutes; longer delays improve deliverability.
    -   `Maximum new leads per day`: Caps the number of new leads contacted daily (in addition to account send limits).
    -   `Campaign start date` (optional): Set a future launch date, or start immediately based on your settings.
7.  Explore `Advanced settings` if needed:
    -   `Webhooks`: Route campaign events to a specific Webhook destination instead of the default Campaign Events Clay table. Example: Send Smartlead metrics to tools like OutboundSync or Enrichley for downstream routing.
    -   `Email tracking`: Configure tracking for email opens and link clicks (if HTML is enabled)
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

## Update sender signatures

You can add or update email signatures for any connected sender account.

**From a specific campaign:**

1.  Go to `Campaigns` from your home screen.
2.  Click on the name of your campaign under `Sequences`.
3.  Navigate to the `Settings` tab.
4.  Scroll to the `Sender setup` section.
5.  Under `Email accounts`, locate the sender you want to edit.
6.  Click the three-dot (⋯) menu on the right side of that sender's row.
7.  Select `Update sender variables`.
    -   You can also access this via the `Email accounts` tab.

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

### I updated my campaign, but the changes didn't save.

Be sure to press `Save settings` after making edits. We're working on making this process smoother.

### How much does the sequencer cost?

The Clay email sequencer is available on all plans. Each lead sequenced consumes 1 Action (platform orchestration work). If you use AI snippets in your messages, those consume 1 Action per run and Data Credits based on the model you select (fixed or variable pricing depending on the model) in addition to the Action for sending the email.

### Can I send multiple sequences to the same email address?

Each lead can only be sequenced once per campaign. To send multiple sequences to the same email address (like [bob@example.com](mailto:bob@example.com)), create a separate campaign for each sequence. Best practice: wait at least a couple of months between sequences to the same person unless you have a completely different offer.

### My sender account got disconnected. What happened?

Email providers like Google and Microsoft occasionally revoke access due to inactivity, security checks, or suspicious activity detection. To fix this, delete the disconnected account from your sequencer settings and re-authenticate it.

### What is email account warmup?

Warmup is the process of automatically sending and receiving emails from other inboxes in Smartlead's warmup pool so your actual campaign traffic looks similar to the emails you're already sending. We recommend you keep warmup on at all times for email accounts in the sequencer to maximize deliverability.

When you add accounts via OAuth, we will automatically set up labels and filters to make it clear what emails are warmups and reduce clutter in your inbox. Your workspace has a unique two-word filter key (e.g., `clever-rocket`) that marks all warmup emails so you can apply these labels and filters.

### Why did warmup turn itself off?

Warmup automatically disables when your emails are being throttled by your email provider. This protects your sender reputation. You can manually turn warmup back on from the `Sender Accounts` tab once the throttling issue is resolved.

### I'm getting an error that my email account is already in use. What does this mean?

Your email account is already connected to another Smartlead account. Smartlead only allows each email address to be connected to one account at a time. If you have access to the other Smartlead account, delete the email account there to free it up. Otherwise, contact support for help.

### Are personal email accounts supported (e.g., Gmail, Hotmail)?

No, only business accounts (Google Workspace, Microsoft Outlook) are supported for OAuth. Personal Gmail accounts can be connected through a legacy SMTP method (see [these docs](https://helpcenter.smartlead.ai/en/articles/4-connect-gmail-with-smtp)), but this workaround may stop working if Google discontinues it.

### I saw an error toast pop up. What should I do?

Often errors in the app are transient. We're calling Smartlead APIs under the hood, and sometimes the request has an issue—usually you can retry the operation and it will succeed (especially if it says a 502 error code). If you keep running into an error, contact support.

### How do I sync campaign data to HubSpot?

You can use our existing table integration in the campaign events table to push updates into HubSpot.

### How do unsubscribes work in the sequencer?

If HTML is enabled, you can add an unsubscribe link to the email that's appended at the bottom of the message. You can also use the `Add lead to blocklist` action in the campaign events table to block them from being sequenced in the future.

### What is a cold lead? What is a warm lead?

A cold lead is someone who doesn't already know about your business and you. A warm lead is someone who has already responded to your email or expressed interest in some other way. The kinds of emails you send to each type are completely different—you can send a lot more emails from your main domain to warm leads than you can to cold leads.

### What exact Gmail permissions does sequencer require?

These are disclosed when you add your account via OAuth. We request: full Gmail email access, basic Gmail settings access, OpenID, user email address and profile picture. Additionally, you will need to have a Google Workspace admin authorize our app to request these permissions for the domain(s) you want to add to the sequencer.

### How do I authorize Clay's app in the Google Admin panel?

Follow the instructions in the modal and have your Google Workspace admin set our Clay sequencer app to `Trusted`. It can take up to 24 hours for Google to recognize the update; once it's taken hold, all accounts in your domain (e.g., [example.com](http://example.com)) can now add themselves to the Clay sequencer.

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
