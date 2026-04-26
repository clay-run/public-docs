---
title: Ironclad integration
source_url: https://university.clay.com/docs/ironclad-integration
last_synced: 2026-04-26T01:40:12.276Z
upstream_hash: 05112ca6d89ff100e7ebfe3187ef88356c0547ab190065044b944a57436fea28
---

# Ironclad integration

Retrieve and utilize detailed workflow information, automatically populate data into internal systems, and send structured contract updates.

Ironclad is a contract lifecycle management platform that streamlines contract creation, negotiation, execution, and post-signature management.

With this integration, you can retrieve and utilize detailed workflow information, automatically populate data into internal systems, and send structured contract updates via Slack.

## **Enriching data with Ironclad**

1.  While in a Clay table, click `Add enrichment` and search for `Ironclad`.
2.  Under `Integrations`, select `Run HTTP Request in Ironclad`.
3.  In the modal, you will be asked to `Select Ironclad account`.
    -   If you haven't already connected your Ironclad account, click `+ Add account` and go through authentication.

### `Action` Ironclad HTTP Request

Make custom HTTP requests to the Ironclad API endpoints to retrieve and process workflow information for contract management and stakeholder communication.

**Inputs**

-   **Method (Optional):** HTTP method for the API call (GET, POST, PATCH, PUT, DELETE). Default: `GET`
-   **Endpoint (Required):** Ironclad API endpoint URL (e.g., `https://api.ironcladapp.com/v1/contracts`)
-   **Query String (Optional):** Query parameters as key-value pairs (e.g., `{"status": "active"}`)
-   **Headers (Optional):** Additional HTTP headers as key-value pairs (e.g., `{"x-as-user-email": "user@example.com"}`)
-   **Body (Optional):** JSON data for POST, PUT, and PATCH requests (e.g., `{"email": "user@example.com", "name": "User"}`)
-   **Remove empty values (Optional):** Remove null/empty values from request. Default: `true`

**Output**

-   Contract details
-   Workflow information
-   Counterparty data
-   Contract terms
-   Renewal details
-   Error messages (if applicable)

### **Run settings**

-   **Auto-update**
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))
