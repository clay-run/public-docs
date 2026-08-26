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

### **`Action` Enrich contact(s) by ID**

Enrich up to 25 contacts at once using their ZoomInfo contact IDs. Use this action when you already have ZoomInfo contact IDs and want to bulk-retrieve full contact details in a single run.

**Inputs**

-   **Contact IDs:** ZoomInfo contact IDs to enrich, entered as a comma-separated list. Only the first 25 IDs are enriched per call.
-   **Output fields (optional):** The contact fields to return. Defaults to all available fields if none are specified.

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

The ZI0001 error (*"The token provided is invalid. Please provide a valid bearer token and try again."*, shown under the title "Unauthorized access") appears when ZoomInfo rejects Clay's authentication token. There are two distinct causes with different fixes:

**Cause 1 — Transient token propagation (retry fixes it)**

ZoomInfo's OAuth tokens can take a moment to propagate after a refresh. There may be a brief window where a new token hasn't fully registered on ZoomInfo's end, causing enrichments to temporarily return a 401 rejection.

**Fix:** Re-run the affected cells. In most cases they succeed immediately on retry.

**Cause 2 — Expired or revoked OAuth connection (reconnect required)**

ZoomInfo's OAuth tokens and sessions expire and must be periodically renewed. This can happen when the connected user's ZoomInfo password changes, their session is invalidated, or the OAuth session reaches its expiration. When this is the cause, retrying will keep returning ZI0001 on every attempt — retrying alone will not resolve it.

**Fix:**

1.  Go to **Settings → Connections** and find your ZoomInfo OAuth connection.
2.  Reconnect it by clicking to re-authenticate and signing in to ZoomInfo again.
3.  Re-run a single row first to confirm the enrichment returns data, then run the rest of your table.

**Tip:** If your ZoomInfo connection is shared across multiple tables or team members, consider using a **ZoomInfo service account** (a shared login not tied to an individual user) rather than a personal account. This prevents one person's password change or session expiry from interrupting enrichments for the whole team.

If ZI0001 persists after reconnecting, contact Clay support to investigate your ZoomInfo account configuration.

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

### **What is the difference between the built-in ZoomInfo integration and using the ZoomInfo API directly in Clay?**

Clay offers two ways to use ZoomInfo data, and the right choice depends on your use case.

**ZoomInfo enrichment (built-in Clay integration)**

The built-in ZoomInfo integration is the easiest way to use ZoomInfo inside Clay. When you add a ZoomInfo action to a Clay table, you get a set of pre-built actions powered by your connected ZoomInfo credentials:

-   **Enrich Contact** — Pull contact details using a name, email address, or company name
-   **Enrich Company** — Get firmographic data like revenue, employee count, and competitors
-   **Search contacts** — Find contacts using filters like job title, department, or country
-   **Enrich contact(s) by ID** — Bulk enrich up to 25 contacts at once using their ZoomInfo contact IDs

These actions handle authentication, rate limiting, and error handling automatically. Each run costs 1 Clay credit and draws on your connected ZoomInfo account. For most enrichment needs — contact data, company data, and prospecting searches — the built-in integration is the quickest path.

**ZoomInfo API via Clay's HTTP Connector**

If you have direct API access provisioned from ZoomInfo, you can also call the ZoomInfo API via Clay's [HTTP API integration](http-api-integration-overview.md). This approach is better suited for advanced use cases that go beyond what the pre-built actions support — for example, calling ZoomInfo endpoints not covered by the built-in actions (such as intent data or custom field selections).

For most use cases, start with the built-in integration. Use the HTTP Connector path only when you need a specific ZoomInfo endpoint or data type not available through the four built-in actions.

### **Does using the ZoomInfo API via Clay's HTTP Connector require a ZoomInfo subscription?**

Yes. To call the ZoomInfo API directly via Clay's HTTP Connector, you need an active ZoomInfo plan that includes API access. ZoomInfo's API access is a separate entitlement from a standard ZoomInfo subscription — even if you have ZoomInfo credits available, you may need API access specifically provisioned or purchased through your ZoomInfo Account Manager. Contact your ZoomInfo Account Manager to confirm whether your plan includes API access before setting up an HTTP API connection to ZoomInfo in Clay.

### **Why is the email field blank even though ZoomInfo shows "Contact found"?**

ZoomInfo's "Enrich Contact" action can return an email address in one of two different fields depending on the record:

-   **`email`** — a single email value that maps directly to Clay's pre-built email output field. When ZoomInfo populates this field, your email column fills in automatically.
-   **`emailAlt`** — an array of alternate email addresses returned in the raw ZoomInfo response. This field is not pre-mapped as a click-selectable output, so it does not automatically populate your email column.

When ZoomInfo only populates `emailAlt` for a record (and leaves `email` empty), your email column will appear blank even though the row shows "Contact found" and email data is present in the enrichment result.

**To capture both fields, add a formula column:**

1.  Add a formula column to your table next to the ZoomInfo enrichment column.
2.  In the formula input, describe the logic in plain language — for example: *"Return the email from the ZoomInfo result. If it's empty, return the value from the first item in the emailAlt array."* Clay's AI formula generator will write the correct formula for you.
3.  Use this formula column as your email source everywhere downstream instead of the direct email output field.
