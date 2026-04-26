---
title: LeadIQ integration
source_url: https://university.clay.com/docs/leadiq-integration-overview
description: B2B sales prospecting platform.
last_synced: 2026-04-26T01:40:14.268Z
upstream_hash: 6e0feef0808d1986d61b56fc7f31f2bab4458595dc3d5670913aabc241857b18
---

# LeadIQ integration

B2B sales prospecting platform.

LeadIQ is a powerful tool for prospecting, allowing users to gather comprehensive information about potential leads, such as contact details, company information, and social profiles.

## **Enriching data with LeadIQ**

1.  While in a Clay table, click `Add enrichment` and search for `LeadIQ`.
2.  Under `Integrations`, select one of the LeadIQ options.
3.  In the modal, you will be asked to `Select LeadIQ account`.
    -   If you haven't already connected your LeadIQ account, click `+ Add account` and go through authentication.

### `Action` Scribe Email

Generate custom email based on input data, leveraging advanced AI models to deliver tailored outputs for your use case.

_This action includes a Clay provided account, but you can also connect your own account if you have one._

**Inputs**

-   **Content type:**
    -   Full Emails (a personalized email, including a greeting and call-to-action)
    -   Openers (a personalized email introduction, including a greeting and hook)
-   **Value proposition:** Text that allows you to control the value proposition used in the generated content.
-   **Lead email:** The email of the lead.
-   **Lead social URL (Optional)**
-   **Lead full name (Optional)**
-   **Lead title (Optional)**
-   **Lead company (Optional)**

### `Action` Generate Value Proposition

Generate a custom value proposition based on company domain, leveraging advanced AI models to deliver tailored outputs for your use case.

_This action has an optional Clay provided account. You can also add your own account if you have one._

**Inputs**

-   **Company domain**
-   **Limit (Optional)**

### `Action` Enrich Person

Allows you to enrich contact details for a person based on their name, LinkedIn profile, and associated company.

**Inputs**

-   **Social URL**: The social media URL of the person you want to enrich, such as their LinkedIn profile. Example: [https://www.linkedin.com/in/example-person/](https://www.linkedin.com/in/example-person/)
-   **Full Name (Optional)**
-   **Company Domain (Optional)**
-   **Search Past Companies (Optional)**
-   **Email (Optional)**
-   **Require Verified Work Phone (Optional):** Toggle to only return results if a verified work phone number is available.
-   **Require Personal Phone (Optional)**: Toggle to only return results if a personal phone number is available.
-   **Require Personal Email (Optional)**: Toggle to only return results if a personal email address is available.
-   **Require Verified Work Email (Optional)**: Toggle to only return results if a verified work email address is available.

### `Action` Enrich Company

Allows you to obtain detailed company information by enriching a single company’s profile based on social URL or company domain data.

**Inputs**

-   **Social URL (Optional):** Enter the social media URL of the company you want to enrich, e.g., [https://www.linkedin.com/company/clay-hq](https://www.linkedin.com/company/clay-hq).
-   **Company Domain (Optional)**
-   **Company Name (Optional)**

### **Run settings**

-   **Auto-update**
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))
