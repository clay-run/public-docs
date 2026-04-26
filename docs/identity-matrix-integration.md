---
title: Identity Matrix integration
source_url: https://university.clay.com/docs/identity-matrix-integration
last_synced: 2026-04-26T01:40:10.344Z
upstream_hash: 84d63f4d53ad4da840cd6750d79a72e83a2fcc9d9809c38d4f0f98b1da3c3697
---

# Identity Matrix integration

Enhances contact data by providing hashed email addresses

Identity Matrix enhances contact data by providing hashed email addresses and LinkedIn URLs, improving advertising targeting and match rates.

This integration focuses on United States contacts and supports email inputs from various sources to increase audience targeting precision.

## **Enriching data with Identity Matrix**

1.  While in a Clay table, click `Add enrichment` and search for `Identity Matrix`.
2.  Under `Integrations`, select one of the Identity Matrix options.
    -   If you have your own account, click `+ Add account` and go through authentication. Otherwise, use the Clay provided key.

### `Action` Find hashed email

Enriches contact records by retrieving hashed email addresses and LinkedIn URLs, optimizing targeting for advertising campaigns.

**Inputs**

-   **Email:** A person's personal or work email address.

**Output**

-   **Hashed emails:** List of hashed email formats (includes hash type, e.g. `SHA256`)
-   **LinkedIn URL:** Associated LinkedIn profile URL if available
-   **Received at:** Timestamp when the data was received
-   **Callback ID:** Unique identifier for the request
