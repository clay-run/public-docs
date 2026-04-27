---
title: Brandfetch integration
source_url: https://university.clay.com/docs/brandfetch-integration-overview
description: Access brand data for next-level B2B personalization.
last_synced: 2026-04-27T18:09:23.800Z
upstream_hash: bcb653e54adff38a346855b843dd8e9b362508585bf28f90a67be23712f69d3f
---

# Brandfetch integration

Access brand data for next-level B2B personalization.

The Brandfetch integration in Clay enables users to access company logos, brand colors, social media profiles, and key company data.

## **Enriching data with Brandfetch**

1.  While in a Clay table, click `Add enrichment` and search for `Brandfetch`.
2.  Under `Integrations`, select one of the Brandfetch options.
3.  In the modal, you will be asked to `Select Brandfetch account`.
    -   If you have your own account, click `+ Add account` and go through authentication. Otherwise, use the Clay provided key.

### `Action` Get brand and company data X

Get company logo, colors, social media, and company data.

**Inputs**

-   **Company Domain:** The domain of the company you want to enrich.

**Outputs**

-   **Source URL**: The link to the company’s logo in an image format (e.g., .svg or .png).
-   **ID**: A unique identifier assigned to the company.
-   **Name**: The name of the company.
-   **Domain**: The domain or website URL of the company (e.g., [example.com](http://example.com)).
-   **Claimed**: Indicates whether the company data is verified (true/false).
-   **Description**: A short overview or tagline describing the company.
-   **Long Description**: An extended description providing detailed information about the company.
-   **Links**: A collection of social media or other relevant links associated with the company.
-   **Link Name**: The name or platform of the link (e.g., Twitter, Facebook).
-   **URL**: The specific URL for the link (e.g., [https://twitter.com/example](https://twitter.com/example)).
-   **Theme**: The type of logo theme, such as dark or light.
-   **Type**: Specifies the type of logo (e.g., icon, wordmark).
-   **Formats**: Available formats for the logo files (e.g., .svg, .png).
-   **Hex Code**: The hexadecimal code representing the brand’s color (e.g., #FFFFFF).
-   **Type**: The classification of the color (e.g., accent, primary).
-   **Brightness**: A numerical value representing the brightness of the color.
-   **Font Name**: The name of the font used in the company’s branding (e.g., Roboto).
-   **Type**: The font type (e.g., title, body).
-   **Origin**: The source of the font (e.g., Google Fonts).
-   **Type**: The type of image provided (e.g., banner, thumbnail).
-   **Formats**: The available formats for the images (e.g., .jpeg, .png).
-   **Quality Score**: A numerical score (e.g., 95) indicating the quality of the retrieved brand data.
-   **Is NSFW**: A Boolean value indicating whether the content is safe for work (false = safe, true = not safe).
-   **URN**: A unique resource name associated with the company (e.g., urn:example:12345).
-   **Employees**: The number of employees in the company (e.g., 100).
-   **Founded Year**: The year the company was founded (e.g., 2000).
-   **Kind**: The type or category of the company (e.g., Educational).

### **Run settings**

-   **Auto-update**
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))
