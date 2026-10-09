---
title: Table alerts
description: Table alerts automatically monitor your Clay tables and notify you
  when something needs attention.
last_synced: 2026-05-11T17:47:40.000Z
---

# Table alerts

Table alerts automatically monitor your Clay tables and notify you when something needs attention.

**Note:** Table Alerts is available for all Enterprise users.

Table alerts automatically monitor your Clay tables and notify you when something needs attention — whether error rates spike in a column, a table grows beyond an expected size, or a table stops receiving new data. Stay on top of data quality issues and workflow health without having to check your tables manually.

## **Setting up table alerts**

Table alerts are configured per table and are **opt-in** — you must explicitly enable alerts for each table and select which alert types you want active. To set up alerts:

1.  Navigate to your table.
2.  Click the **⚠️ warning icon** in the bottom-right corner to open the `Table alerts` panel.
3.  If alerts haven't been enabled yet, you'll see _"Alerts are not enabled for this table."_ Click `Configure alerts` — or click the **⚙️** icon in the panel header — to open `Alert settings`.
4.  Toggle on `Enable alerts` to turn on alerts for this table.
5.  Under `Alert Rules`, enable and configure each alert type individually:
    -   `Column failure rate` — alerts when a column's error rate exceeds a threshold. Default: **75%**.
        -   **Muting columns:** You can selectively choose which columns trigger alerts. By default, all columns are enabled for alerting. To mute specific columns:
            -   **Right-click** on a column header and select `Mute Alerts for Column`.
            -   Click the **three dots menu** on a column and select the muting option.
            -   Use the **Column Selector** (similar to Schedule Runs UI) to enable/disable columns in bulk. This is the recommended approach for focusing alerts on critical downstream columns only.
        -   When you add a new column to your table, it's automatically enabled for alerting by default.
        -   **Use case:** This is useful for non-critical upstream columns where errors are expected or acceptable. For example, if you only care about alerts for a critical downstream column like a Google Search enrichment, you can mute all other columns and enable alerting only for your critical column.
    -   `Row count limit` — alerts when your table's row count exceeds a threshold. Default: **45,000 rows**.
    -   `Data inactivity` — alerts when a table with a signal, scheduled signal, or scheduled run has received no new data for a configured period. Default: **1 day**.
6.  Click `Save`.

**Note:** Alert rules apply to all users on the table. Alerts must be enabled before they will appear in the feed.

## **Viewing and managing alerts**

### **Finding alerts in your table**

Once alerts are enabled and thresholds are configured, alerts will fire automatically when conditions are met.

1.  Look for the **⚠️ warning icon with a number** in the **bottom-right corner** of your table. The number represents the count of unresolved grouped alerts (not individual alert logs).
2.  Click the icon to open the `Table alerts` panel.
3.  Review the feed of all triggered alerts for that table.

**Grouped alerts:** Alerts of the same type and column are automatically grouped together in the feed to reduce clutter. Each grouped alert shows:

-   `Column name` — which column exceeded the error threshold (for column failure rate alerts).
-   `Unresolved logs count` — how many times this same error has triggered (e.g., "12 unresolved logs").
-   `Latest timestamp` — when the most recent alert fired.
-   `Threshold` — the value that was exceeded (e.g., "10% error rate threshold").
-   `Error cause` — the most recent error that occurred (e.g., "invalid API key").

**Viewing grouped alert details:**

Click any grouped alert to open a details panel showing:

-   **Latest error message** — displays the most recent threshold and error that triggered.
-   **Most recent errors** — shows the errors that occurred in the latest alert.
-   **Historical log** — a clickable list of all previous alerts for this column/type, including:
    -   Timestamp when each alert triggered
    -   Threshold at that time
    -   Error causes that occurred
    -   Resolve state of each log

Click any alert to automatically scroll to and highlight the relevant column in your table for faster investigation.

### **Managing your alerts**

From the `Table alerts` panel, you can:

-   `Mark as resolved` — resolves an individual grouped alert and updates the icon count in the bottom-right corner. Resolved alerts are grayed out visually.
-   `Mark all resolved` — clears all grouped alerts at once.
-   `Mark as unresolved` — **only unmarks the most recent alert** within a grouped alert. Historical logs remain resolved because only the latest alert is relevant for addressing the current issue.
-   `Hide resolved alerts` — toggles the view to show only active, unresolved alerts.

### **Checking current thresholds**

Click the **⚙️** icon in the `Table alerts` panel header at any time to view or adjust the alert settings for that table.

## **External notifications**

By default, alerts appear inside the `Table alerts` panel. You can also receive them externally:

### **Email notifications**

1.  Open the `Table alerts` panel.
2.  Click the **🔔 bell icon** in the panel header to subscribe.
3.  Choose your notification frequency:
    -   **Immediately** (default) — receive an email every time a new alert triggers
    -   **Daily digest** — receive a single email per day with all alerts from that table
    -   **Weekly digest** — receive a weekly summary of all alerts
4.  You'll receive emails to your Clay account-associated email address based on your selected frequency.

### **Slack notifications**

Slack alerts for a table are sent by the **Clay Alerts Bot**, a separate Slack app from the Clay app used by the [Slack integration](slack-integration-overview.md) actions in your tables. Setting up Slack alerts takes two parts: a Clay workspace admin connects Slack to the Clay workspace once, and then you choose a Slack channel for each table you want alerts from.

**Step 1: Connect Slack to your Clay workspace (one time, workspace admins only)**

1.  Go to `Workspace settings`.
2.  In the `Notifications` section, click `Connect to Slack`.
3.  Authorize the Clay Alerts Bot in Slack. If you see _"Apologies, but Clay Alerts Bot can't be installed"_, see [Clay Alerts Bot can't be installed](#clay-alerts-bot-cant-be-installed-in-slack) below.

Only Clay workspace admins can connect Slack. Other members see _"Only workspace admins can configure notifications."_ The connection applies to the whole Clay workspace, so nobody needs to connect it again for each table or user. Connecting Slack under **Settings → Connections** adds the Slack integration account used by table actions, and it does **not** turn on Slack alerts.

**Step 2: Choose a Slack channel for a table's alerts**

1.  In your table, click the **⚠️ warning icon** in the bottom-right corner, then open `Alert settings`.
2.  Click the **🔔 bell icon** in the header.
3.  Under `Slack alerts`, click `Connect`.
4.  Enter the ID of the Slack channel where you want the alerts to go. To find a channel ID, right-click the channel name in Slack and click **Copy link**. The ID (it starts with `C`) is the last part of the copied URL.
5.  Choose your notification frequency:
    -   **Immediately** (default): alerts are sent to Slack as they trigger
    -   **Daily**: one message per day with all alerts
    -   **Weekly**: a weekly summary of all alerts

If you see _"Slack is not connected for this workspace. Connect Slack in workspace settings."_, a workspace admin needs to finish Step 1 first.

Slack alerts for a table are posted by the Clay Alerts Bot to the channel you selected. They don't come from your personal Slack account. To use a private channel, invite the Clay Alerts Bot to it first. Otherwise you'll get the error _"Bot is not a member of this channel. Please invite the bot to the channel."_

Slack alerts are set up table by table. There's no workspace-wide setting that turns on alerts for every table, so repeat Step 2 (and enable alerts, as described in [Setting up table alerts](#setting-up-table-alerts)) on each table you want to monitor.

## **FAQs**

### **Clay Alerts Bot can't be installed in Slack**

When you click `Connect to Slack`, Slack may show _"Apologies, but Clay Alerts Bot can't be installed. This app isn't listed in the Slack Marketplace, so only workspace owners can install it."_ The Clay Alerts Bot isn't listed in the Slack Marketplace, which means your IT team can't search for it there. Instead, it's installed directly through the `Connect to Slack` OAuth flow in Clay. To install it:

1.  Ask a Slack workspace owner (or whoever approves apps in your Slack workspace) to approve or install the Clay Alerts Bot. Your security team may need to review the scopes listed in the next FAQ.
2.  After it's approved, have a Clay workspace admin who is signed in to the right Slack workspace in the same browser click `Connect to Slack` in `Workspace settings` → `Notifications`.

### **Which Slack permissions (scopes) does the Clay Alerts Bot request?**

The Clay Alerts Bot asks for these Slack bot scopes, which are needed to post table alerts to a channel:

-   `chat:write`: post alert messages as the Clay Alerts Bot
-   `chat:write.public`: post to public channels the bot hasn't joined
-   `channels:read`: view public channels and their basic info
-   `groups:read`: view private channels the bot has been invited to
-   `users:read`: view basic info about workspace members
-   `users:read.email`: look up workspace members by email address
-   `im:write`: open direct messages with workspace members

The Clay Alerts Bot doesn't ask for any user scopes. These scopes are separate from the ones requested by the Clay Slack integration used in table actions. Those are listed in [Slack integration: Permissions & security](slack-integration-overview.md#permissions--security).

### **How do I get more or fewer alerts?**

Open the `Table alerts` panel and click the **⚙️** icon in the header to access `Alert settings`. Lowering the thresholds means alerts fire more frequently; raising them means fewer alerts fire. The defaults — 75% for column failure rate and 45,000 rows for row count limit — work well as a starting point for most workflows.

### **Are thresholds set per-table or per-workbook?**

Thresholds are configured at the **table level**, giving you individual control over thresholds and alert types for each table. Open the `Table alerts` panel for any table and click the **⚙️** icon to view or update its settings.

### **What is the data inactivity alert?**

The data inactivity alert fires when a table that has recurring data activity — a signal, scheduled signal, or scheduled run — stops receiving new data for a configured period. The default threshold is 1 day. This alert only applies to tables with recurring activity enabled; it won't fire for tables that were never regularly receiving data.

### **How often can the same alert fire?**

Alerts of the same type are rate-limited to once every 24 hours per table, so you won't receive repeated notifications in quick succession for the same condition.

### **Can I subscribe a teammate to email alerts instead of myself?**

Email alerts are tied to the Clay account of the person who clicks the **🔔 bell icon** to subscribe. Each user manages their own subscription individually.

### **What counts as a column error for the column failure rate alert?**

A column error is triggered by failures during action runs, such as missing required inputs, data validation errors, or action pre-validation failures. The alert fires when the percentage of failed runs in a column exceeds your configured threshold.

### **Do resolved alerts come back if the issue isn't fixed?**

Yes. Marking an alert as resolved clears it from your active feed, but if the underlying condition persists or recurs, a new alert will fire.

### **Does the feature cost credits?**

No, table alerts is a monitoring feature and does not consume actions or data credits.
