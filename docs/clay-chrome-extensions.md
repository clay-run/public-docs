---
title: Clay Chrome extensions
source_url: https://university.clay.com/docs/clay-chrome-extensions
last_synced: 2026-04-26T01:39:43.902Z
upstream_hash: 3f598ba523e0a110f86274a46dbd6b703865a56fb1e5b105bd8ae83dd5e19d1f
---

# Clay Chrome extensions

Extract structured data from any webpage with the Clay Chrome Extension.

Clay offers two powerful Chrome extensions that help you gather and organize information from the web:

-   **Clay for Chrome** lets you extract structured data from webpages, either from a list or an individual page.
-   **Clip to Clay** allows you to quickly save entire webpages to your Clay tables.

Both tools integrate seamlessly with your Clay workspace, making it easier to collect, organize, and act on web data.

## Clay for Chrome

The Clay for Chrome extension allows you to extract structured data from webpages. You can capture data from a single page, lists across multiple pages, or even custom-defined structures. Once extracted, the data can be added directly to your Clay table, downloaded as a CSV, or copied to your clipboard.

### Autodetected lists

The extension automatically detects list-like structures on the page and formats them into a table.

With autodetected lists, you can:

-   Export the list as a CSV or copy it to your clipboard.
-   Add to Clay by opening the list in a new window and saving it directly to your table.

### Custom recipes

You can create custom recipes to extract data in two main formats:

-   **Pages with lists.** Extract multiple items from a structured list, such as a directory or table.
-   **Individual pages.** Extract specific data from single-item pages, such as profiles or product pages.

### Creating a list recipe

To create a recipe that extracts data from list-style pages:

1.  [Install the Clay for Chrome extension](https://chromewebstore.google.com/detail/clay-for-chrome/acmfklpkefjlldbkdgmjoiknfgidadoh?hl=en).
2.  Open the Clay for Chrome extension on a webpage with a list.
3.  Click `Select Data to Add from Page`.
4.  Choose `Select a List` and click multiple items to help the extension detect patterns.
5.  Add attributes for each item:
    -   For images, select the `Image Attribute` (e.g., logos).
    -   For text, select the `Text Attribute` (e.g., name, location).
6.  Repeat this process for each attribute you want to capture.
7.  Name and save your recipe.

### Creating an individual page recipe

To create a recipe for scraping structured data from profile or detail pages:

1.  Open the Clay for Chrome extension on the page you want to scrape.
2.  Click `Select Data to Add from Page`, then choose `Select a Single Attribute`.
3.  Map each attribute you want to extract:
    -   For example: name, website, LinkedIn, Twitter, or Crunchbase.
4.  Adjust the `URL Matching` settings to apply the recipe to similar pages:
    -   Replace specific URL components with variables (e.g., `:company_name`).
5.  Name and save your recipe.

## Third party Clay tools

-   [**Exportly.ai**](https://www.exportly.ai/) is a Chrome extension that brings Clay's data and AI tools right into your browser. You can find verified contact details, add prospects to your Clay tables, and write personalized outreach without leaving the page you're on.
-   [**The Swarm**](https://www.theswarm.com/integrations/clay) is a powerful networking tool that helps you discover relationship paths to companies and people. Through this integration, you can leverage your network connections to find warm introductions to both companies and individuals.
