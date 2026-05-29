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

### **I'm not able to set up the ZoomInfo connection with my credentials. Why?**

This is usually due to one of the following:

-   The email or password is incorrect
-   Your ZoomInfo account doesn't have API access enabled
-   Your account has API access but lacks permissions for specific endpoints required by Clay
-   You're using SSO (Single Sign-On), which isn't supported for API

To troubleshoot:

1.  **Verify your credentials** — Check that the email and password you entered are correct.
2.  **Check API access** — Contact ZoomInfo support to confirm your account has API access enabled and is provisioned for the required API endpoints.
3.  **Refresh the connection in Clay** — Go to **Settings → Connections**, delete the existing ZoomInfo connection, then re-add it and re-authenticate.

If issues persist, reach out to ZoomInfo support to resolve any remaining account restrictions.
