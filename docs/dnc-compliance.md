---
title: Do Not Contact (DNC) compliance & best practices
source_url: https://university.clay.com/docs/dnc-compliance
last_synced: 2026-04-26T01:39:53.932Z
upstream_hash: 566b91c2837cf544d699a341b4bc8f78ef15be16fa8a30acbc48b6da50fbf0fd
---

# Do Not Contact (DNC) compliance & best practices

Information about DNC compliance and best practices.

**_Last updated: 2/23/25_**

_This information is for general guidance only and isn’t legal advice. Rules on DNC compliance differ across Europe and may change. Please consult your own legal counsel before relying on this information._

### **Key Takeaways for Clay Customers**

1.  **Assess your risks and avoid calling numbers listed on national DNC registries without clear legal basis.**
2.  **Maintain robust internal DNC and opt-out lists** and operationalize them across all outreach channels.
3.  **Scrub calling lists frequently** (at least monthly) prior to outbound dialing.
4.  **Document consent and communication preferences.**
5.  **Train teams, audit regularly, and adjust compliance procedures** as laws or best practices evolve.

By following these best practices, Clay customers can conduct outbound outreach that is both effective and compliant with Do Not Contact regulations across jurisdictions.

### **1\. What Is a Do Not Contact (DNC) List?**

A **Do Not Contact (DNC) list** is a registry or suppression list that identifies phone numbers for which recipients have opted out of unsolicited marketing calls. These lists exist to protect individuals’ preferences and ensure compliance with outbound marketing regulations in jurisdictions like the United States, UK, and others. Cold calling or contacting a phone number on a DNC list without proper authorization may result in fines or legal action.

There are two primary types of DNC lists:

**National/Regulatory DNC Registries**

These are maintained by government authorities (e.g., in the U.S., National Do Not Contact Registry, in the UK, the Corporate Telephone Preference Service) and legally restrict telemarketing to listed numbers. Businesses that conduct outbound marketing calls must scrub their call lists against these registries regularly.

**Internal DNC Lists**

These are internal, company-specific suppression lists of individuals or businesses who have directly indicated that they do not want to receive any marketing calls from your organization, even if you have a previous or existing relationship with them. Maintaining and honoring internal DNC lists is a core compliance requirement. Marketing lists should also be scrubbed against the internal DNC registry on a regular basis.

### **2\. Why DNC Compliance Matters**

Non-compliance with DNC regulations can expose your business to regulatory fines, private litigation, brand reputation damage, and interruption of your outreach workflows. In the U.S., violations — such as calling numbers on the DNC registry without express permission — may  trigger civil penalties per call or complaint. In Europe, in some instances, non-compliance can also lead to personal liability for directors of your business.

Compliance also supports better customer experience: respecting communication preferences increases trust in your brand and reduces frustration or complaints.

### **3\. Core DNC Compliance Best Practices with Clay**

Clay enables outbound outreach workflows — including call lists and integrations with sales and engagement tools — so it’s critical that the following best practices are adopted by all teams using Clay data.

### **a. Scrub Against Regulatory DNC Lists**

Before initiating outbound calls:

-   Check your phone number lists **against applicable national DNC registries** (e.g., in the U.S. National Do Not Contact Registry, in the UK, the Corporate Telephone Preference Service) to ensure numbers listed by consumers are excluded. We've partnered with [Meer](http://meerapi.com/) to help you easily do this within your existing Clay workflows, they currently support US (National DNC Registry), UK (TPS/CTPS) registries, Germany ([Robinsonliste.de](http://robinsonliste.de/)), and Ireland ([comreg.ie](http://comreg.ie/)), with additional countries being added regularly.
-   In the European Union, data protection rules mean that you will need to establish a lawful basis for using any individual’s personal information. You will need to document the lawful basis and record the ways you ensure compliance with applicable legal requirements.
-   Update this scrub at least **once every 28 days** before launching calling campaigns. For extra precaution, this could be be done once every 14 days. One approach to doing this is the following:
    -   In your CRM, create a field for “Date of DNC Screening”.
    -   When you screen a number, map the outputted date from the Meer integration to this new CRM field
    -   Setup a CRM list that automatically pushes records into a Clay table once it is 27 days past the “Date of DNC Screening”, and run it through the Meer integration again.

Clay customers should integrate DNC status in their data workflows where available (e.g., using data enrichment that flags numbers on DNC lists). This reduces manual checking and minimizes risk.

### **b. Maintain and Honor Internal DNC Lists**

-   Every organization should have an internal **opt-out process and internal DNC list** for prospects and customers who request no further calls.
-   When a recipient asks not to be contacted, record and remove the number from all active call lists **as quickly as possible** and prior to any future outreach.
-   U.S. regulators have said that your process should let consumers opt out by using any reasonable means, and shouldn’t be limited to “magic words” like “stop,” “quit,” “end,” “revoke,” “opt out,” “cancel,” or “unsubscribe."

### **c. Provide Clear Opt-Out Mechanisms**

-   When calling, ensure your scripts and processes provide an easy way for people to **opt out of future calls**.
-   If wearing multiple hats (sales + support), track opt out preferences centrally (e.g., CRM and Clay interactions) so they propagate to all systems.

### **d. Respect Time-of-Day Calling Rules**

While DNC lists focus on “who not to call,” many jurisdictions also mandate **when you may contact a number** (e.g., U.S. guidelines restrict calls to business hours). Always verify local rules around permissible calling windows.

### **e. Document and Audit**

-   Document your DNC compliance procedures in writing.
-   Train your team on these procedures.
-   Periodically audit calling logs and processes to verify that DNC policies are followed.

Monitoring and audits help you identify gaps and maintain compliance over time.

### **4\. Understanding Exceptions**

Some calls are exempt from DNC list restrictions depending on the jurisdiction, the nature of the call, and existing relationships:

-   **Existing Business Relationships (EBR)**: In certain regulatory environments, you may contact a prospect you have an active relationship with, even if their number is on a DNC registry — but only under specific conditions and for a limited period.
-   **Express Written Consent**: If a contact has given clear written consent to receive marketing calls, and didn’t later opt out, outreach may be permissible.

Always document consent clearly and tie it to the specific number and purpose of call.

### **5\. How Clay Supports Compliant Outreach**

Clay does not replace legal compliance tools, but users can implement the following within Clay workflows:

**Flag and filter contacts by DNC status using our partner’s DNC screening integration service,** [**Meer**](http://meerapi.com/)

-   Check numbers in your CRM or outputted from data waterfalls to identify and exclude contacts flagged with a DNC status.

**Sync internal opt-out lists**

-   Coordinate opt-out data from sales engagement tools, CRM, or internal databases back into Clay so all downstream enrichments and workflows respect opt-out preferences.
-   To set this up, you could store your complete list of opted out contacts in either your CRM or a Clay table, and then use a look-up action in all future prospecting workflows to avoid re-enriching or engaging these opted out contacts.

**Automate suppression logic**

-   Where possible, automate suppression lists and exclusion rules so that contacts who are on national registries or internal DNC lists are not included in calling campaigns.

**Controls to handle contacts in different regions differently.**

-   **People Search Filters.** Starting from a blank workbook in Clay, you can build searches for People. These searches include filtering functionality which can be configured to include or exclude different countries or regions. Note that these filters can also be used to exclude predefined lists of people for targeting, for example to support a company-maintained DNC list.
-   **Selective CRM Uploads.** When you source contacts in this way through Clay, the data is not automatically synced to your CRM. You must then add Salesforce actions, such as “Create Contact” to your Clay workflow. When you create or update contacts in your CRM, you can add further logic to prevent data from excluded geos being sent. See General Filtering Recommendations below for more.
-   **Conditional Logic.** All actions (enrichments) in Clay have the same settings for “Only run if” which allow for building logical flows to implement compliance procedures, ICP filtering, and so on. This means that you can add a third check to your workflows before you sync data back to the CRM. For example: Only uploading contacts from the United States to your CRM.
