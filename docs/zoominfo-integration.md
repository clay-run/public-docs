---
title: ZoomInfo integration
source_url: https://university.clay.com/docs/zoominfo-integration
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

### **How do I call ZoomInfo API endpoints not covered by the native integration, such as looking up records by ZoomInfo ID?**

The native ZoomInfo integration supports two actions: **Enrich Company** (by company name and website) and **Enrich Contact** (by email or name). If you need to call other ZoomInfo API endpoints—for example, to look up records by a ZoomInfo company or contact ID, or to access search functionality not available in those two actions—use Clay's **HTTP API with JWT Authentication** action instead.

This approach uses ZoomInfo's username-and-password authentication, and Clay automatically refreshes the token before it expires, so you won't encounter the hourly 401 errors that occur when managing short-lived tokens manually.

**Setting up ZoomInfo as an HTTP JWT account (one-time per workspace):**

1.  Go to **Settings → Connections**, search for **HTTP API JWT Auth**, and click **+ Add account**.
2.  Enter the following:
    -   **Username** — your ZoomInfo username (email address)
    -   **Password** — your ZoomInfo password
    -   **JWT Token Endpoint** — `https://api.zoominfo.com/authenticate`
3.  Name the account (for example, *ZoomInfo JWT*) and click **Save**.

**Configuring the enrichment:**

1.  In your Clay table, click **Add enrichment** and search for **HTTP API with JWT Authentication**.
2.  Select the ZoomInfo JWT account you just created.
3.  In the **Location of JWT token in auth response** field, enter `jwt`.
4.  Leave **Token type** as `Bearer` and **Auth header name** as `Authorization` (both defaults).
5.  Set the HTTP method, endpoint URL, and request body to match the ZoomInfo API endpoint you want to call. Pass your column values (such as a ZoomInfo ID) as inputs in the request body using [ZoomInfo's API reference](https://docs.zoominfo.com).

**Note:** This setup requires a ZoomInfo subscription with API access enabled. If you see authentication errors, see the [Invalid credentials FAQ](#im-seeing-an-invalid-credentials-error-when-running-zoominfo-enrichments-why) above.
