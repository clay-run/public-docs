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
    -   **Note:** The contacts table and the LinkedIn URL identifier column selected here cannot be changed after the signal is saved. To monitor a different set of contacts or use a different LinkedIn URL column, create a new signal.
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

### Can I change the contacts table or LinkedIn URL column my Job Change Signal monitors?

No — the contacts table and the LinkedIn URL identifier column a Job Change Signal monitors are selected when the signal is first created and cannot be changed afterward via **Edit Signal**. In **Edit Signal**, you can still change settings such as how often the signal runs, its filters, its name, and whether it's on or off — but the contacts table and identifier column stay locked.

To switch to monitoring a different contacts table, create a new signal pointing to the new table. To preserve your enrichment column configurations from the existing signal's results table, save it as a template first: click the table title → scroll to **Share as template** → toggle it on and copy the link. Open the link in a new tab — the resulting table will include all your enrichment column configurations, so you don't have to rebuild them from scratch.

If you only need to fix incorrect or missing LinkedIn URLs for contacts the signal already monitors, you don't need a new signal — see the next FAQ.

### I corrected my contacts' LinkedIn URLs — how do I get the Job Change Signal to re-check them?

The Job Change Signal stores a starting snapshot for each **row** in your contacts table, not for each LinkedIn URL. If you update the LinkedIn URL on a row that's already in the table, that row keeps its original snapshot and is not checked from scratch. Clicking `Save and re-run` or `Retry` in **Edit Signal**, force running the column, or turning on `Initial check` also keeps existing snapshots — only rows newly added to the contacts table get a fresh first check.

To have the Job Change Signal re-check contacts after fixing their LinkedIn URLs:

1.  Correct the LinkedIn URLs in the system your contacts table imports from (for example, your CRM), so re-imported rows carry the corrected URLs.
2.  Delete the affected rows from the signal's contacts table.
3.  Re-import those contacts into the same contacts table using a **new** source. Re-running an existing source skips records it has already imported, so it won't bring the deleted rows back.
4.  Let the signal run. Turn on `Initial check` if you also want job changes within your lookback window (3 months, 6 months, or 1 year) reported for these contacts.

Each re-imported row is checked again as a new row, so each check consumes 1 action plus 0.2 data credits.

**Convert to custom table won't re-source a signal table.** The `Convert to custom table` option in the table title menu only changes the table's type — it doesn't copy your data or columns to a new table, and it can't be undone.

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
