---
title: Google Docs integration
source_url: https://university.clay.com/docs/google-docs-integration
description: Create or update your docs from Clay.
last_synced: 2026-04-26T01:40:03.437Z
upstream_hash: 554b4cd8ea567f3da797d903c0adc93676563a8a464bac9c331fb0ddeaedae10
---

# Google Docs integration

Create or update your docs from Clay.

Google Docs is a word processing tool that allows you to create and edit documents online.

With this integration, you can utilize the power of Clay for your Google Docs without ever leaving your document.

## **Enriching your Google Docs with Clay**

1.  While in a Clay table, click `Add enrichment` and search for `Google Docs`.
2.  Under `Integrations`, select one of the Google Docs options.
3.  In the modal, you will be asked to `Select Google Docs account` .
    1.  If you haven’t already connected your Google Docs, click `+ Add account` and go through authentication.

### `Action` Create Doc

Use this action to create a Doc in Google Docs.

**Inputs**

-   **Google Drive folder:** The folder you want to create the new doc in.
-   **Document title:** The title of the new doc.
-   **Document content:** The content of the new doc.

### `Action` Append text to Doc

-   **Google Doc:** The ID of the Google Doc you want to append text to.
-   **Document content:** The content of the new doc.
-   **Include newline:** Create a newline before appending the text.

**Tip:** You can use Markdown formatting when creating or appending docs with the Google Docs integration! Learn how in this Loom video:

### **Run settings**

-   **Auto-update**
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))
