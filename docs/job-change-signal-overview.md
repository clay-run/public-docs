---
title: Monitor for job changes
description: Track job change trends and leverage timely insights for proactive
  decision-making.
last_synced: 2026-04-26T01:40:12.599Z
---

# Monitor for job changes

Track job change trends and leverage timely insights for proactive decision-making.

Job Change Signals notify you when monitored contacts switch roles, helping you transform existing relationships into new opportunities.

-   **Sales**: Monitor champions who may bring your solution to new companies.
-   **Customer Success**: Stay ahead of account changes and engage new decision makers.
-   **Operations**: Keep contact data fresh with automatic CRM updates.

**_Cost:_** _Each check consumes 1 action plus 0.2 data credits._

## Monitoring job changes

To set up Job Change Signals in your table:

1.  Click `Tools`, then select `Monitor for job changes`.
2.  Select your table of the contacts you want to monitor for job changes. It must contain the contact's LinkedIn URL as an identifier.
    -   **LinkedIn URL stored in Salesforce?** If the LinkedIn URL exists in Salesforce but isn't yet a column in your Clay table, add a [Salesforce Lookup Record](salesforce-integration-overview.md) column first — it returns all fields on the Contact record, including custom LinkedIn URL fields.
    -   **Note:** The contacts table selected here cannot be changed after the signal is saved. To monitor a different set of contacts, create a new signal.
3.  Optionally, enable `Initial check`.
    1.  The Job Change Signal monitors for new changes **going forward** from when you set it up — it will not automatically surface contacts who had already changed jobs before monitoring started. Enable Initial check to also scan for recent past job changes. It checks each contact's **work history** for role changes within your chosen lookback window: **3 months**, **6 months**, or **1 year**.
4.  Set how often the Signal should run.
5.  Optionally, add enrichments to gather additional data.
6.  Optionally, `Add sample results`.
    -   This lets you preview how the data will appear after any changes actually happen.
7.  Click `Save and run X rows` to finish.

**Need regular data updates instead of specific change monitoring through Signals?** Check out [scheduled columns](https://www.clay.com/university/guide/scheduled-columns) and [scheduled sources](https://www.clay.com/university/guide/scheduled-sources).

## FAQs

### Does Clay have a built-in persistent contact ID that follows someone across job changes?

No. Clay does not have a native persistent person identifier equivalent to a third-party data provider's contact ID (such as a ZoomInfo Contact ID). Instead, **the contact's professional profile URL** is the practical stable anchor — because a person's professional profile follows them across employers, it lets Clay continue tracking that contact after a job change.

For this reason, the Job Change Signal requires each contact's professional profile URL as input. When Clay detects that the person's current employer no longer matches your records, it fires an event so you can re-enrich or update your CRM.

### Can I change which contacts my Job Change Signal monitors?

No — the contacts table a Job Change Signal monitors is selected when the signal is first created and cannot be changed afterward via **Edit Signal**. Attempting to edit the signal will show the contacts table field as locked.

To switch to monitoring a different contacts table, create a new signal pointing to the new table. Clay creates a new results table for the new signal. To reuse the columns you built in the old results table, see [How do I keep my results table workflow when I replace a Job Change Signal?](#how-do-i-keep-my-results-table-workflow-when-i-replace-a-job-change-signal) below.

### Why does "Select LinkedIn Profiles" show "Please select a valid value" when I edit my Job Change Signal?

When you edit an existing Job Change Signal, the **Select LinkedIn Profiles** field shows "Please select a valid value" if the LinkedIn profile column the signal was set up with no longer matches a valid column in the People table — for example, because that column was deleted. The field is locked when editing an existing Job Change Signal, so you can't select a different column (such as a new LinkedIn profile column you added to the table) from this screen.

To start monitoring the new LinkedIn profile column:

1.  Create a new Job Change Signal on the same People table and choose the new column under **Select LinkedIn Profiles**.
2.  Move the columns you built in the old results table into the new signal's results table using a function — see [How do I keep my results table workflow when I replace a Job Change Signal?](#how-do-i-keep-my-results-table-workflow-when-i-replace-a-job-change-signal) below.
3.  To stop the old Job Change Signal from consuming credits, disable it from its column header → **Edit signal**. See [Signals in Clay](signals.md) for details.

### Can I connect a new Job Change Signal to my existing results table?

No. When you create a Job Change Signal, Clay creates its results table at the same time (named like `Job change Events from <your table> (<date>)`), and that table's `Event: Job change` column receives the signal's events. A Job Change Signal can't be re-pointed to send events to a different table, and an existing results table can't be connected to a different signal.

Two common workarounds don't connect a results table to a new signal:

-   **Duplicating the results table** — the copy stays connected to the original signal, not to your new one.
-   **Saving the results table as a template (Share as template) and opening the link** — the resulting table includes your columns but isn't connected to your new signal (opened in the same workspace, it stays connected to the original signal), and the new signal still creates its own separate results table.

To carry your formulas, enrichments, and conditions over to the new signal's results table, save them as a function instead (see the next FAQ).

### How do I keep my results table workflow when I replace a Job Change Signal?

Save the workflow columns from the old Job Change Signal results table as a [function](functions.md), then add that function to the new signal's results table. Functions are available on all paid plans (not the Free plan).

1.  Open the old Job Change Signal results table and select the workflow columns you want to keep (Shift-click the first and last column headers to select a range, or `Cmd`/`Ctrl`-click individual headers).
2.  With the columns selected, choose `Save as function` — from the right-click menu on a column header, or from the action bar that appears above the selected columns.
3.  Name the function and review its **Inputs** (the values it reads from the table, such as the LinkedIn URL or company) and **Outputs**, then save it.
4.  Open the new Job Change Signal's results table, click `Add column`, go to the `Functions` tab, and select your function.
5.  Under **Configure inputs**, map each function input to the matching column in the new results table. Checking which column fed each input in the old results table makes this mapping straightforward.

Your enrichment columns, formulas, and run conditions are stored in the function, so you don't have to rebuild them in the new results table. For more on building and editing functions, see [Functions](functions.md).

### How do I track contacts who change jobs ("movers") and refresh their details?

Use the **Job Change Signal** (see setup steps above). It monitors each contact's professional profile URL on a schedule you set. When a job change is detected, you can attach enrichment columns — such as Enrich Person, Find Work Email, or Find Phone — to pull the contact's updated company, title, and contact information automatically.

If you also want a stable custom contact ID that survives job changes, build a **formula column** using fields that don't change with employment:

-   **Personal email** — the most durable option; doesn't depend on employer
-   **Professional profile URL** — follows the person across jobs (note: the URL's custom username portion can occasionally be edited by the user, so it is not fully immutable)

Avoid basing a custom ID on work email, company name, or a CRM contact ID, since all of these can change when someone switches employers.

### Why does the signal flag contacts whose company information already matches my CRM?

The Initial check does not compare against your current CRM data. It scans each contact's work history for role changes within the lookback window you chose (3 months, 6 months, or 1 year) and surfaces all changes detected in that period — regardless of whether your CRM has since been updated to reflect those changes.

For example: if a contact changed companies 5 months ago and your CRM was updated at the time, a 6-month Initial check will still flag that contact, because the signal is reporting what it found in the contact's work history, not what currently differs from your CRM.

To filter out job changes your CRM has already captured, add a filter on your results table to exclude rows where the contact's **email domain** already matches their **Most Recent Company Domain** column. This limits your results to contacts whose job change is not yet reflected in your CRM.
