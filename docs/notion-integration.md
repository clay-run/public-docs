---
title: Notion integration
source_url: https://university.clay.com/docs/notion-integration
last_synced: 2026-04-26T01:40:25.061Z
upstream_hash: 140b09d448acf1b0076a7f6f3b107a959298d66f36e42b9839a1f0968766d3b1
---

# Notion integration

Update your Notion pages and databases.

Notion is a productivity tool for note taking, project management, and much more.

With this integration, you can utilize the power of Clay for your Notion workspace without ever leaving your table.

## Setting up the Notion integration

1.  While in a Clay table, click `Add enrichment` and search for `Notion`.
2.  Under `Integrations`, select one of the Notion options.
3.  In the modal, you will be asked to `Select Notion account` .
    1.  If you haven’t already connected your Notion, click `+ Add account` and go through authentication.

## Using the Notion integration

### ‍`Action`Create page

Use this action to create a page in Notion.

‍**Inputs**

-   **Parent page:** The existing Notion page that you’d like to create a page within.
-   **Page title:** The title of the new page.
-   **Page content:** The content of the new page.

### `Action` Append content to page

Use this action to add content to existing Notion pages.

‍**Inputs**

-   **Page ID:** The Notion page you want to add content to.
-   **Page content:** The content you want to add.

### `Action` Create database item

Use this action to create a new item within a Notion database.

‍**Inputs**

-   **Database ID:** The Notion database you’d like to add to.
-   **Name:** The name of the new item that will be added.
-   **Properties** (Optional): Edit the database Notion properties for this item, such as tags or dates.

### `Action` Update database item

Use this action to update an item within a Notion database.

‍**Inputs**

-   **Database ID:** The Notion database you’d like to add to.
-   **Item ID:** The ID of the item to update.
-   **Properties** (Optional): Edit the database Notion properties for this item, such as tags or dates.

### `Action` Lookup object by title

Use this to search a Notion page or database.

‍**Inputs**

-   **Object type:** The Notion Page or database you’d like to look into.
-   **Title:** The title you want to find.
