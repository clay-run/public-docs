---
title: Google Docs integration
description: Create, update, or find your docs from Clay.
last_synced: 2026-04-26T01:40:03.437Z
---

# Google Docs integration

Create, update, or find your docs from Clay.

Google Docs is a word processing tool that allows you to create and edit documents online.

With this integration, you can utilize the power of Clay for your Google Docs without ever leaving your document.

## **Enriching your Google Docs with Clay**

1.  While in a Clay table, click `Add enrichment` and search for `Google Docs`.
2.  Under `Integrations`, select one of the Google Docs options.
3.  In the modal, you will be asked to `Select Google Docs account` .
    1.  If you haven't already connected your Google Docs, click `+ Add account` and go through authentication.

### `Action` Find document

Use this action to look up a Google Doc and retrieve its content.

**Inputs**

-   **Identifier type:** How you want to identify the document. Choose one of:
    -   **Google Docs ID or URL** — provide a full Google Docs URL or the document's ID string.
    -   **Document Title** — provide the exact title of the document.
-   **Document identifier:** The URL, ID, or title of the Google Doc you want to find.
-   **Google Drive folder** *(optional, title search only)*: Limit the search to a specific Google Drive folder. This setting only applies when **Identifier type** is set to **Document Title**. When looking up a document by URL or ID, the folder restriction has no effect.

**Outputs**

-   **Total Found:** The number of matching documents found.
-   **First Match:** Details about the first matching document, including its URL, ID, full text content, and title.

**Troubleshooting: "No document found"**

If the action returns "No document found" when searching by URL or ID, it means Google could not locate the document. This almost always means one of two things:

-   The document has been deleted.
-   The document is not shared with the Google account you connected to Clay.

To check: open the document link in a browser while signed in as the connected Google account. If you see a "Request access" prompt or a 404 error, share the document with that account (or reconnect Clay using the account that owns the document), then re-run the column.

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
