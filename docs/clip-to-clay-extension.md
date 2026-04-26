---
title: Clip to Clay extension
source_url: https://university.clay.com/docs/clip-to-clay-extension
last_synced: 2026-04-26T01:39:45.854Z
upstream_hash: 408ddd809c30d587a2c584322b8b20053f66fcd3a7c09b421c74b0ca5ff1617c
---

# Clip to Clay extension

Learn how to clip your web pages into a Clay table.

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

## Clip to Clay

The Clip to Clay extension lets you quickly save full webpages into your Clay tables. It’s useful for capturing unstructured data or bookmarking key pages.

### Setting up

To get started:

1.  [Install the Clip to Clay Chrome extension](https://chromewebstore.google.com/detail/clip-to-clay/peaelamodldoacgjbgemamnljcjehiif).
2.  Open the Clay table you want to use, click the table name, and select `Show in Chrome Extension`.
    -   Only tables added this way will appear in the extension.

### Using Clip to Clay

To save a webpage:

1.  Visit the webpage you want to save and open the Clip to Clay extension.
2.  Select your destination Clay table.
    -   If the table doesn’t appear, check that:
        -   You’re in the correct workspace.
        -   The table has been enabled for the extension.
3.  Click `Add to Table` to save the page.

### Viewing history and customizing fields

To view your saved clips:

1.  Open Clip to Clay and click `History`.
2.  Browse your previously saved links and their destination tables.
3.  Click `Go to Table` to open the saved page in your Clay workspace.

To customize your history view:

1.  Open the Clay table connected to the extension.
2.  Click the table name, then click `Configure Chrome Extension Fields`.
3.  Choose which fields you want to display and click `Save`.
4.  Your clipping history will now reflect the selected fields.
