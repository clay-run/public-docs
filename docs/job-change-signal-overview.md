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

### How do I track contacts who change jobs ("movers") and refresh their details?

Use the **Job Change Signal** (see setup steps above). It monitors each contact's professional profile URL on a schedule you set. When a job change is detected, you can attach enrichment columns — such as Enrich Person, Find Work Email, or Find Phone — to pull the contact's updated company, title, and contact information automatically.

If you also want a stable custom contact ID that survives job changes, build a **formula column** using fields that don't change with employment:

-   **Personal email** — the most durable option; doesn't depend on employer
-   **Professional profile URL** — follows the person across jobs (note: the URL's custom username portion can occasionally be edited by the user, so it is not fully immutable)

Avoid basing a custom ID on work email, company name, or a CRM contact ID, since all of these can change when someone switches employers.

### Can I detect job changes that already happened before I set up the signal?

Yes — enable **Initial check** in step 3 of the signal setup. Initial check scans each contact's LinkedIn work history and surfaces contacts who changed roles within your chosen lookback window (3 months, 6 months, or 1 year), even if those changes happened before you set up the signal. The signal only needs each contact's LinkedIn URL to run; no additional CRM fields are required for retroactive detection.

**Using the Job Change Signal to clean up stale CRM data:** If your goal is to find contacts in your CRM (HubSpot, Salesforce, etc.) who have already moved to a new company — so you can update or re-associate their records — follow this order:

1.  Export your contacts from your CRM into a Clay table. Make sure each row includes the contact's **LinkedIn URL** — that is the only identifier the signal needs.
2.  Set up the Job Change Signal on that table and enable **Initial check** with your desired lookback window.
3.  Run the signal. It flags every contact whose current employer (as shown on their LinkedIn profile) changed within the lookback window.
4.  Use those results to update your CRM records — re-associate contacts to their new companies, correct outdated job titles, etc.
5.  Keep the signal running on a schedule to catch future job changes automatically.

**Set up and run the signal before doing a bulk removal of contacts from your CRM.** If you delete contact records first, you lose their LinkedIn URLs and can no longer check those contacts for past job changes.
