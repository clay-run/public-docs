---
title: Best practices for B2B email direct marketing
description: Conduct effective outbound email outreach whilst also lowering the
  risk of challenges
last_synced: 2026-04-26T01:39:53.596Z
---

# Best practices for B2B email direct marketing

Conduct effective outbound email outreach whilst also lowering the risk of challenges

_Please note this article is for informational purposes only, and isn’t legal advice. You should always speak to your own legal counsel to determine your compliance obligations._

Key Takeaways:

1.  **Consider which country(ies) your recipients are in to assess your risks** - a handful of EEA countries have email DNC lists. Avoid emailing recipients listed on those lists unless you have a clear legal basis.
2.  **The clearer the provenance and relevance of the email outreach are to the recipient, the lower the risk**
3.  **Always include a simple, easily accessible opt-out mechanism** in your emails
4.  **Review and scrub email distribution lists** **frequently** (at least monthly) prior to outreach
5.  **Track consents (where required), opt-outs and communication preferences**
6.  **Train teams, audit regularly, and adjust compliance procedures** as laws or best practices evolve.

By following these best practices, Clay customers can conduct effective outbound email outreach whilst also lowering the risk of challenges across EEA jurisdictions and the UK.

### **1\. Do all countries across the EEA/UK have the same rules when it comes to direct B2B email marketing?**

As a general rule, all EEA countries’ and the UK’s data protection rules mean that Clay customers will need to establish a lawful basis for using any individual’s personal information. However, certain EEA countries have stricter rules when it comes to direct B2B email outreach compared to others.

The following considerations will help in assessing your approach in the EEA region:

-   **Check where your recipients are located (if known).**

Considering which country(ies) the intended recipients of your outreach are located in will help you in assessing your risks and identifying if there are any specific local law requirements.

-   **Think about national email DNC lists**.

**Bulgaria and Austria** have national **Do Not Contact (DNC) lists for email outreach**. These are lists which include email addresses of recipients who have opted out of unsolicited marketing emails. These lists exist to protect individuals’ preferences and reaching out to email addresses on DNC lists without proper authorisation may result in complaints or legal action.

-   **Consider the types of email addresses within your outreach campaign**.

Certain types of email address pose lower risks across the region. Generic business/corporate email addresses (such as [info@company.com](mailto:info@company.com)) pose the lowest risk.

Individuals’ corporate email addresses (such as [name.surname@company.com](mailto:name.surname@company.com)) are comparatively higher risk in some countries, although see below ways in which you can mitigate this when composing your outreach campaign.

Ensure you are **not** including any personal email addresses in your outreach (e.g. [username@gmail.com](mailto:username@gmail.com)).

### **2\. Why provenance and relevance matter.**

Provenance and relevance both help to ensure that outbound email outreach is targeted and effective whilst also documenting clear, transparent and compliant communication.

-   **Provenance** = “_who is the sender?_”. Clay customer’s email outreach should clearly identify who the email comes from, therefore avoiding anonymous campaigns or misleading communications.
-   **Relevance** = “_is the email outreach pertinent to the recipient?_”. The more tailored the outreach is to the recipient, e.g. the sector they operate it, their company, their experience or context, their current job role, the lower the risk in practice of complaints or reports.

At the same time, an email showing clear relevance, context and business interest also supports recordkeeping of Clay’ customer’s lawful basis and legitimate interest behind the outreach.

### **3\. Opt-out mechanisms and internal DNC lists**

Every organisation should set up an **opt-out process** and maintain an **internal (email) DNC list**.

-   Every email must include a **valid address or link enabling recipients to object** or unsubscribe easily to future communication or outreach via the opt-out processes in place.
    -   The opt-out process should be easily accessible and free.
    -   Depending on Clay’s customer’s opt-out mechanism, the recipient may be able to choose which communications to unsubscribe to and which to retain.
-   Ensure a **central record is maintained internally** of all opt-outs, and (if applicable) which communications the opt-outs relate to.
    -   It is preferable to automate this process, as it significantly reduces the risk of opt-outs not being documented and respected going forwards.
    -   Also ensure that, once a recipient opts-out to any (or all) email communication, their email address is **removed** from any email distribution lists as soon as possible.
    -   If a recipient opts-out of any (or all) email communication outside of the standard opt-out process (e.g. by responding to an email), ensure this is also immediately **recorded**.

Any new opt-outs should effectively supplement the internal email DNC list and processes should be put in place to ensure distribution lists are regularly checked against this DNC list.

#### **How to handle GDPR opt-outs in Clay and sync them to Salesforce and HubSpot**

Clay doesn't have a built-in GDPR opt-out or suppression list. You can still use Clay to collect opt-outs from every source, write them back to Salesforce and HubSpot, and stop opted-out contacts from being enriched or pushed anywhere. Set it up like this:

1.  **Choose one system of record for consent.** Pick Salesforce, HubSpot, or a dedicated Clay opt-out table as the source of truth. Clay moves opt-out changes between systems; it shouldn't be the only place consent is recorded.
2.  **Standardize the opt-out field in each CRM.** If you use both Salesforce and HubSpot, agree on the fields you'll write to in each one. For example, the standard Salesforce `HasOptedOutOfEmail` checkbox on Leads and Contacts, plus any custom fields for opt-out date, source, and request type.
3.  **Create an opt-out table in Clay with a [webhook](webhook-integration-guide.md) source.** Point your forms, preference center, email sequencer, consent platform, and CRM automations at the table's webhook URL. Each POST request to the webhook creates a new row. Webhooks require a Growth or Enterprise plan (see [Plan availability](webhook-integration-guide.md)).
4.  **Normalize each request** in the opt-out table, for example by lowercasing the email address and adding columns for the timestamp, the request source, and the request type (opt-out or erasure).
5.  **Add CRM write-back columns.** Use the Salesforce **Update record** (or **Create or update object**) action and the HubSpot **Update object** action to write the opt-out status to the matching Lead, Contact, or HubSpot contact. Turn on [Auto-run](auto-run.md) so these columns run on each new opt-out row.
6.  **Keep the opt-out table as your audit log.** Each row shows who opted out, where the request came from, when it arrived, and which systems were updated.
7.  **Check every other Clay table against the opt-out table.** Add a **Lookup Single Row in Other Table** column that matches on email, then add a run condition ("Only run if") to your enrichments, AI columns, and CRM or sequencer push actions so they skip any contact found in the opt-out table. See [Lookup Rows](lookup-rows.md) and [Conditional runs](conditional-runs.md).

**HubSpot subscription status limitation:** Clay's HubSpot actions write contact properties only. They can't change a contact's email subscription types or communication preferences, which HubSpot manages separately from contact properties. Manage subscription status in HubSpot itself.

Clay gives you the tools to put an opt-out process into practice. Your team and legal counsel are still responsible for deciding which contacts you can reach in which regions.

### **4\. Distribution lists**

It is key to ensure that distribution lists are kept up to date. Before creating or re-using an existing email distribution list:

-   For new distribution lists, check all email addresses against the applicable internal (and external) email DNC lists.
-   For existing ones, confirm that the most recent review / scrub was carried out less than 28 days prior to the outreach launch; otherwise, review the list prior to use.
-   Check whether there are any more recent updates / changes that you should take into account.

### **5\. Document and Audit**

Monitoring and audits help you identify gaps and maintain compliance over time.

-   Maintain records of lawful basis assessments
-   Document opt-out, DNC compliance workflows and email‑list hygiene processes
-   Train relevant teams on these procedures
-   Periodically audit email distribution lists and processes to verify that policies are followed.
