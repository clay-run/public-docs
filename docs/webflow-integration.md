---
title: Webflow integration
source_url: https://university.clay.com/docs/webflow-integration
description: Create, retrieve, and update items in Webflow from Clay.
last_synced: 2026-04-26T01:40:53.914Z
upstream_hash: 0813e843f2b227c9d3589d71b6c59da11afd2b5c0ccab7b3963c3ffbd92b205d
---

# Webflow integration

Create, retrieve, and update items in Webflow from Clay.

Webflow is a powerful no-code website development platform that enables users to create professional, responsive websites without writing any code.

With this integration, you can create, retrieve, and update items in your Webflow collections directly from Clay, enabling seamless data synchronization between platforms.

## **Enriching data with Webflow**

1.  While in a Clay table, click `Add enrichment` and search for `Webflow`.
2.  Under `Integrations`, select one of the Webflow options.
3.  In the modal, you will be asked to `Select Webflow account`.
    -   If you haven't already connected your Webflow account, click `+ Add account` and go through the authentication.

### `Action` Create collection item

Creates a new item in a specified Webflow collection.

**Inputs**

-   **Site**
-   **Collection**
-   **Is draft (Optional):** Check this to create items as drafts.
-   **Is archived (Optional):** Check this to create items as archived.

### `Action` Get collection item

Retrieves a single item from a specified Webflow collection.

**Inputs**

-   **Site**
-   **Collection**
-   **Name (Optional)**
-   **Slug (Optional)**

### `Action` Update collection item

Updates an existing item in a specified Webflow collection.

**Inputs**

-   **Site**
-   **Collection**
-   **Item ID**
-   **Is draft (Optional):** Check this to create items as drafts.
-   **Is archived (Optional):** Check this to create items as archived.

### Run settings

-   **Auto-update**
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))

## Best practices & troubleshooting

-   **Publish new fields at least once:** Webflow's API requires a custom field to have a value in a published Collection Item and a site republish before it becomes accessible.
-   **Format slugs correctly:** Slugs must use lowercase letters and hyphens (-) instead of spaces or underscores.
    -   **Correct:** `company-overview`, `summer-sale`, `contact-us`
    -   **Incorrect:** `Company Overview`, `company@2022`, `My_Page!`
-   **Ensure Item ID** comes from a recent `Get collection item` lookup.
-   **Remap all fields** you want to preserve, as any omitted fields will reset to defaults.
-   **Image fields** must use either a direct, CORS-enabled image URL or be uploaded directly to Webflow.
-   **Remove any** control characters and unsupported HTML from ri**ch text/long text** fields.
