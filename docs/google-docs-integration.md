---
title: Google Docs integration
description: Create or update your docs from Clay.
last_synced: 2026-04-26T01:40:03.437Z
---

# Google Docs integration

Create or update your docs from Clay.

Google Docs is a word processing tool that allows you to create and edit documents online.

With this integration, you can utilize the power of Clay for your Google Docs without ever leaving your document.

## **Enriching your Google Docs with Clay**

1.  While in a Clay table, click `Add enrichment` and search for `Google Docs`.
2.  Under `Integrations`, select one of the Google Docs options.
3.  In the modal, you will be asked to `Select Google Docs account` .
    1.  If you haven't already connected your Google Docs, click `+ Add account` and go through authentication.

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

### Markdown formatting

Both the **Create Doc** and **Append text to Doc** actions support Markdown in the **Document content** field.

**Supported syntax:**

-   **Bold:** Wrap text in `**double asterisks**`. The closing `**` must immediately follow the last character — a space before `**` prevents bold from rendering (e.g., `**Stage:**` works; `**Stage: **` does not).
-   **Headings:** Use `##` for a level-2 heading (18 pt bold), `###` for level 3, and so on.
-   **Line breaks:** Include an actual newline in the content value. A single newline creates a line break in the document. When using an AI column, instruct it to output each section on a new line.
-   **Empty gap line:** Markdown discards blank lines between sections. To render a visible empty line, put `&nbsp;` on its own line with a blank line above and below it.

**About Include newline:** The **Include newline** toggle adds one newline separator before the entire appended block — it does not insert line breaks between sections inside the content itself.

### **Run settings**

-   **Auto-update**
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))
