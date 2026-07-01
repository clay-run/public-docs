---
title: ZoomInfo integration
description: Get detailed insights into company structures, competitive
  landscapes, and accurate contact details.
last_synced: 2026-04-26T01:40:59.430Z
---

# ZoomInfo integration

Get detailed insights into company structures, competitive landscapes, and accurate contact details.

The ZoomInfo Integration enriches company and contact records with comprehensive business metrics, organizational data, and personal information to boost your sales and marketing efforts.

It offers detailed insights into company structures, competitive landscapes, and accurate contact details—helping you prioritize prospects and improve outreach strategies.

## Setting up the ZoomInfo integration

1.  While in a Clay table, click `Add enrichment` and search for ZoomInfo.
2.  Under `Integrations`, select one of the ZoomInfo options.
3.  In the modal, you will be asked to `Select ZoomInfo account`.
    -   If you haven't already connected your account, click `+ Add account` and go through authentication.

## Using the ZoomInfo integration

### **`Action` Enrich company**

Gets key company data like revenue and competitors to help prioritize prospects, and provides company hierarchy information through various ID references.

**Inputs**

-   **Company name:** Name of the company you want to enrich
-   **Company website:** Website domain of the company you want to enrich

### **`Action` Enrich contact**

Use ZoomInfo's contact-level data to enhance data coverage in your Clay workbooks.

**Inputs**

-   **Email address:** Contact's email address_OR_
-   **First name:** Contact's first name
-   **Last name:** Contact's last name
-   **Company name:** Contact's company name

### **`Action` Search contacts**

Search ZoomInfo's database for contacts matching specific criteria. Use this action to build targeted lists of people at a specific company or to filter by role, department, or seniority level.

**Inputs**

-   **Company website:** Domain of the company whose contacts you want to search (e.g., `acme.com`). Supply this to narrow results to contacts at a specific company.
-   **Include title keywords:** Comma-separated job title keywords to include (e.g., `Sales, Marketing`). ZoomInfo limits this field to 500 characters.
-   **Exclude title keywords:** Comma-separated job title keywords to exclude (e.g., `Intern, Assistant`). ZoomInfo limits this field to 500 characters.
-   **Departments:** ZoomInfo department categories to filter by.
-   **Management level:** Comma-separated management levels to filter by (e.g., `C Level Exec, VP Level Exec, Director, Board Member`).
-   **Country:** One or more countries to filter contacts by. ZoomInfo limits this field to 500 characters.
-   **Location search type:** Whether to match on the contact's personal location, their company HQ, or a combination. Options: Person or HQ, Person and HQ, Person, HQ, Person then HQ.
-   **Minimum contact accuracy score:** Minimum accuracy score for returned contacts (e.g., `85`).
-   **Required fields:** Comma-separated fields a contact must have to be returned (e.g., `email`).
-   **Sort by:** How to sort results. Defaults to relevance (most to least).
-   **Page size:** Number of contacts to return per page, from 1 to 100. Defaults to 25.

### **Run settings**

-   **Auto-update**
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))

## **FAQs**

### **I'm seeing an "Invalid credentials" error when running ZoomInfo enrichments. Why?**

The "Invalid credentials" error can appear even when your ZoomInfo integration looks connected and active in Clay. Clay shows this generic error whenever ZoomInfo rejects the authentication request—including when the underlying issue is a **ZoomInfo API licensing problem**, not a wrong password.

This is usually due to one of the following:

-   The email or password is incorrect
-   Your ZoomInfo account does not have API access provisioned — this is a **separate entitlement** from a standard ZoomInfo subscription. Even if you have ZoomInfo credits, you may still need API access enabled or purchased through your ZoomInfo Account Manager
-   Your account has API access but lacks permissions for specific endpoints required by Clay
-   You're using SSO (Single Sign-On), which isn't supported for API access

To troubleshoot:

1.  **Verify your credentials** — Check that the email and password you entered are correct.
2.  **Confirm API access with ZoomInfo** — Contact your ZoomInfo Account Manager to confirm whether your account has API access provisioned. API access is a licensing entitlement separate from your base ZoomInfo subscription; even accounts with available credits may need it specifically enabled or purchased.
3.  **Refresh the connection in Clay** — Go to **Settings → Connections**, delete the existing ZoomInfo connection, then re-add it and re-authenticate.

If issues persist, reach out to ZoomInfo support to resolve any remaining account restrictions.

### **I'm seeing a ZI0001 "The token provided is invalid" or "Unauthorized access" error. Why?**

The ZI0001 error (*"The token provided is invalid. Please provide a valid token and try again."*, shown under the title "Unauthorized access") is a **transient issue**, not a credential setup problem. It occurs because of how ZoomInfo handles OAuth token refresh cycles: there can be a brief window after a token is issued or refreshed when the new token hasn't fully propagated on ZoomInfo's end, causing enrichments to temporarily return a 401 rejection.

**Fix:** Re-run the affected cells. In most cases they succeed immediately on retry.

If ZI0001 persists across multiple cells after retrying, or if you see it consistently on every run, contact Clay support so we can investigate your ZoomInfo connection.

### **Why are some rows returning "out of credits" errors when I still have ZoomInfo credits?**

If you see a mix of successful enrichments and "out of credits" errors across rows in the same run, the likely cause is that your ZoomInfo account has **exceeded its enrichment limit**. The underlying error returned to Clay is: *"Your ZoomInfo account has exceeded its enrichment limit. Please contact your ZoomInfo Account Manager."*

When a table run starts with enough remaining enrichment headroom to fulfill some rows but not all, you'll see partial results: earlier rows succeed and later rows fail with this error. Re-running the column will continue to return the same error until your enrichment limit is raised or reset by ZoomInfo.

**What to do:** Contact your ZoomInfo Account Manager or representative and ask them to check your **enrichment limit** and usage. They can see your enrichment usage in their system and can request an increase to your allocation if needed.

### **How do I stamp a "ZoomInfo Last Updated Date" and "ZoomInfo Enriched Status" on records to prevent double-enrichment downstream?**

When syncing ZoomInfo-enriched records to a CRM, you may want to stamp the enrichment date and a status label so that downstream tools (such as a deduplication or enrichment platform) can detect records Clay already enriched and skip re-enriching them. Use two formula columns whose formulas return a value only when ZoomInfo returned data, and empty otherwise.

**Step 1: Add a formula column for the enrichment date**

1.  Add a formula column to your table and name it something like **ZoomInfo Last Updated Date**.
2.  Reference a ZoomInfo output field that is only populated on a successful enrichment (e.g., `{{ZoomInfo Email}}`). Use a conditional expression to return today's date when that field has a value, and nothing when it doesn't:
    ```javascript
    {{ZoomInfo Email}} ? moment().format("YYYY-MM-DD") : null
    ```
    If ZoomInfo returned data, the formula stamps today's date. If the ZoomInfo enrichment returned nothing, the formula outputs nothing.

**Step 2: Add a formula column for the enrichment status**

1.  Add a second formula column and name it something like **ZoomInfo Enriched Status**.
2.  Use the same conditional pattern to return a static label when ZoomInfo returned data:
    ```javascript
    {{ZoomInfo Email}} ? "Clay Enriched" : null
    ```

**Step 3: Map both columns to your CRM**

In your CRM update action (e.g., a Salesforce update), map the date and status formula columns to the corresponding fields on the record. Your downstream enrichment tool can then read these fields and skip records where they are already populated.

**Distinguishing Clay-enriched vs. records enriched by another tool**

If you need to tell apart records that Clay enriched from those enriched by a different platform (e.g., another tool that also enriches via ZoomInfo), use a shared source field in your CRM that each tool writes to:

1.  Pull the existing enrichment source field from your CRM into your Clay table (e.g., a field that the other tool populates with its own label when it enriches a record).
2.  On your ZoomInfo enrichment column, open **Run Settings → Only run if** and enter a JavaScript formula expression that skips records where the source field already indicates another tool enriched it — for example:
    `{{Enrichment Source}} !== "Ringlead Enriched"`
3.  When Clay enriches a record, write a value like **"Clay Enriched"** back to that same source field in your CRM update action.

This way, each tool's label in the shared source field tells the other tool to leave the record alone.

For more on conditional formula expressions in formula columns, see [Formulas](formula-generator.md). For run conditions on enrichment columns, see [Conditional runs](conditional-runs.md).
