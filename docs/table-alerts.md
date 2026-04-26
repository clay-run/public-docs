---
title: Table alerts
source_url: https://university.clay.com/docs/table-alerts
last_synced: 2026-04-26T01:40:45.731Z
upstream_hash: e34c36c747d3f38a0364e60e07395eb3ff5f1644adec0dbc30d00b617b43bb9e
---

# Table alerts

Table alerts automatically monitor your Clay tables and notify you when something needs attention.

**Note:** This a beta feature for Enterprise Plans only. Reach out to your growth strategist if you’re interested in learning more.

Table alerts automatically monitor your Clay tables and notify you when something needs attention — whether error rates spike in a column, a table grows beyond an expected size, or a table stops receiving new data. Stay on top of data quality issues and workflow health without having to check your tables manually.

## **Setting up table alerts**

Table alerts are configured per table and are **opt-in** — you must explicitly enable alerts for each table and select which alert types you want active. To set up alerts:

1.  Navigate to your table.
2.  Click the **⚠️ warning icon** in the bottom-right corner to open the `Table alerts` panel.
3.  If alerts haven't been enabled yet, you'll see _"Alerts are not enabled for this table."_ Click `Configure alerts` — or click the **⚙️** icon in the panel header — to open `Alert settings`.
4.  Toggle on `Enable alerts` to turn on alerts for this table.
5.  Under `Alert Rules`, enable and configure each alert type individually:
    -   `Column failure rate` — alerts when a column's error rate exceeds a threshold. Default: **75%**.
    -   `Row count limit` — alerts when your table's row count exceeds a threshold. Default: **45,000 rows**.
    -   `Data inactivity` — alerts when a table with a signal, scheduled signal, or scheduled run has received no new data for a configured period. Default: **1 day**.
6.  Click `Save`.

**Note:** Alert rules apply to all users on the table. Alerts must be enabled before they will appear in the feed.

## **Viewing and managing alerts**

### **Finding alerts in your table**

Once alerts are enabled and thresholds are configured, alerts will fire automatically when conditions are met.

1.  Look for the **⚠️ warning icon with a number** in the **bottom-right corner** of your table.
2.  Click the icon to open the `Table alerts` panel.
3.  Review the feed of all triggered alerts for that table.

Each alert shows:

-   `Column name` — which column exceeded the error threshold (for column failure rate alerts).
-   `Threshold` — the value that was exceeded (e.g., "10% error rate threshold").
-   `Error cause` — the reason for failure (e.g., "missing inputs").
-   `Row count status` — whether your table has exceeded the row limit (for row count limit alerts).
-   `Inactivity duration` — how long the table has gone without new data (for data inactivity alerts).

Click any alert to automatically scroll to and highlight the relevant column in your table for faster investigation.

### **Managing your alerts**

From the `Table alerts` panel, you can:

-   `Mark as resolved` — resolves an individual alert and updates the icon count in the bottom-right corner.
-   `Mark all resolved` — clears all alerts at once.
-   `Hide resolved alerts` — toggles the view to show only active, unresolved alerts.

### **Checking current thresholds**

Click the **⚙️** icon in the `Table alerts` panel header at any time to view or adjust the alert settings for that table.

## **External notifications**

By default, alerts appear inside the `Table alerts` panel. You can also receive them externally:

### **Email notifications**

1.  Open the `Table alerts` panel.
2.  Click the **🔔 bell icon** in the panel header to subscribe.
3.  You'll receive an email to your Clay account-associated email address every time a new alert triggers for that table.

### **Slack notifications**

1.  Go to your `Workspace Settings`.
2.  Connect your Slack workspace to Clay's delivery system (workspace admin access required).
3.  Return to the `Table alerts` panel.
4.  Click `Connect Channel`.
5.  Select the Slack channel where you want to receive alerts.

## **FAQs**

### **How do I get more or fewer alerts?**

Open the `Table alerts` panel and click the **⚙️** icon in the header to access `Alert settings`. Lowering the thresholds means alerts fire more frequently; raising them means fewer alerts fire. The defaults — 75% for column failure rate and 45,000 rows for row count limit — work well as a starting point for most workflows.

### **Are thresholds set per-table or per-workbook?**

Thresholds are configured at the **table level**, giving you individual control over thresholds and alert types for each table. Open the `Table alerts` panel for any table and click the **⚙️** icon to view or update its settings.

### **What is the data inactivity alert?**

The data inactivity alert fires when a table that has recurring data activity — a signal, scheduled signal, or scheduled run — stops receiving new data for a configured period. The default threshold is 1 day. This alert only applies to tables with recurring activity enabled; it won't fire for tables that were never regularly receiving data.

### **How often can the same alert fire?**

Alerts of the same type are rate-limited to once every 30 minutes per table, so you won't receive repeated notifications in quick succession for the same condition.

### **Can I subscribe a teammate to email alerts instead of myself?**

Email alerts are tied to the Clay account of the person who clicks the **🔔 bell icon** to subscribe. Each user manages their own subscription individually.

### **What counts as a column error for the column failure rate alert?**

A column error is triggered by failures during action runs, such as missing required inputs, data validation errors, or action pre-validation failures. The alert fires when the percentage of failed runs in a column exceeds your configured threshold.

### **Do resolved alerts come back if the issue isn't fixed?**

Yes. Marking an alert as resolved clears it from your active feed, but if the underlying condition persists or recurs, a new alert will fire.

### **Does the feature cost credits?**

No, table alerts is a monitoring feature and does not consume actions or data credits.
