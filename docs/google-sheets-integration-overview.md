---
title: Google Sheets integration
description: Cloud-based spreadsheet for real-time collaboration. Covers using
  Google Sheets as a Clay table source (including dedup fields and import
  history), enrichment actions, and pushing rows from Google Sheets into Clay
  using Apps Script.
last_synced: 2026-04-26T01:40:04.431Z
---

# Google Sheets integration

Cloud-based spreadsheet for real-time collaboration.

Google Sheets in Clay enables seamless integration between your Clay tables and Google Sheets, allowing you to easily sync and manage data across both platforms.

## Using Google Sheets as a source

You can pull rows from a Google Sheet directly into a Clay table as a source. Each time the source runs, Clay reads rows from the spreadsheet and adds or updates rows in your table.

### Setting up a Google Sheets source

1.  In a Clay table, click `Tools` → `Import` (or `Sources`, depending on your account).
2.  Search for `Google Sheets` and select the source option.
3.  Connect your Google account and select your spreadsheet.
4.  Choose the **Sheet ID** (tab) to import from.
5.  Select **Fields to deduplicate by** — one or more columns that together uniquely identify each row (see below).
6.  Optionally, set a **Lookup column** and **Lookup value** to filter which rows are imported (only rows where that column matches the lookup value will be included).

### Fields to deduplicate by

**Fields to deduplicate by** is a required setting. Clay uses the values of these column(s) to compute a unique ID for each row. This ID is what Clay uses to track which rows have already been imported and to match incoming rows against existing ones on re-runs.

**Choosing the right dedup fields is critical for predictable imports:**

-   **Use a single, truly unique field** — such as an email address, LinkedIn URL, or a custom record ID. This ensures every row gets a distinct ID, so Clay can accurately track and update individual records.
-   **Avoid using non-unique fields** — such as Company Name. If multiple rows in your sheet share the same value for the dedup field (for example, five contacts all at the same company), Clay assigns those rows the same unique ID and treats them as the same record. All five rows will collapse into a single row in the table.
-   **Avoid selecting many fields at once** — deduplicating across a large number of fields means a row is only recognized as "already imported" when *all* of those field values match exactly. Minor differences in any one field create a new unique ID, which can cause unexpected duplicate rows on re-runs.

### Why the source says "X rows found" but fewer rows appear in the table

If your source reports finding more rows than actually appear in your table, the cause is almost always the **Fields to deduplicate by** configuration:

-   Rows that share the same values for the dedup fields get the same unique ID. Clay collapses them into a single record — even if other columns differ.
-   Rows whose unique ID matches a row already in the table are updated in place rather than creating new rows.

**Example:** If **Company** is your only dedup field and five rows all list `AltiSales` as the company, Clay assigns the same unique ID to all five. The source finds all five rows in the sheet, but only one record is created in your Clay table.

### Why rows I deleted don't reappear when I re-run the source

Clay's Google Sheets source tracks every record it has imported by storing its unique ID (derived from **Fields to deduplicate by**). This import history persists even after you delete rows from the table. When you re-run the source against the same sheet data, Clay recognizes those records as already-seen and skips them — which is why deleted rows don't reappear even though the source "finds" them.

**To re-import previously deleted rows or start fresh:**

-   **Delete and re-add the source:** Click the source column title → `Sources` → the source name → `Delete source`. Then add a new Google Sheets source pointing to the same spreadsheet. A fresh source has no import history, so it will pull all rows in.
-   **Duplicate the table:** Creates a new table with a fresh source definition that has no prior import history.

**Note:** If you want to refresh data in existing rows, enable **Update existing rows** in the source's Run settings (under the source column → `Edit source` → `Run settings`). When enabled, re-running the source will update matching rows with the latest values from the sheet.

## Pushing rows from Google Sheets into Clay

To automatically send new rows from a Google Sheet to a Clay table — for example, when a form response arrives or a row is added manually — use Clay's **Webhook source** combined with a **Google Apps Script** that POSTs each new row to your webhook URL.

**Plan requirement:** The Webhook source requires an Explorer plan or above. Free-plan workspaces cannot use webhook sources.

### Step 1: Create a webhook table in Clay

1.  In a workbook, click `+ Add` at the bottom.
2.  Search for `Webhooks` and select **Monitor webhook**.
3.  Copy the webhook URL Clay generates — you'll paste it into the script in the next step.

### Step 2: Add the Apps Script to your Google Sheet

1.  Open your Google Sheet.
2.  Go to **Extensions → Apps Script**.
3.  Replace the default code with the following script:

```javascript
var CLAY_WEBHOOK_URL = 'YOUR_CLAY_WEBHOOK_URL'; // replace with your webhook URL

function sendNewRowsToClay() {
  var sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();
  var data = sheet.getDataRange().getValues();
  var headers = data[0];
  var props = PropertiesService.getScriptProperties();
  var lastProcessedRow = parseInt(props.getProperty('lastProcessedRow') || 1);

  for (var i = lastProcessedRow; i < data.length; i++) {
    var rowData = {};
    for (var j = 0; j < headers.length; j++) {
      rowData[headers[j]] = data[i][j];
    }
    UrlFetchApp.fetch(CLAY_WEBHOOK_URL, {
      method: 'post',
      contentType: 'application/json',
      payload: JSON.stringify(rowData)
    });
  }

  props.setProperty('lastProcessedRow', data.length);
}
```

4.  Replace `YOUR_CLAY_WEBHOOK_URL` with the URL from Step 1.
5.  Click **Save**.

The script uses script properties to track how many rows have been sent, so only new rows are pushed on each run. Each POST creates exactly one new row in your Clay table.

### Step 3: Set a time-based trigger

To run the script automatically on a schedule:

1.  In Apps Script, click **Triggers** (clock icon in the left sidebar) → **Add Trigger**.
2.  Set **Choose which function to run** to `sendNewRowsToClay`.
3.  Set **Select event source** to **Time-driven**.
4.  Choose your preferred interval (for example, every hour or every 15 minutes).
5.  Click **Save**.

For full details on webhook request format, rate limits, and troubleshooting, see [Webhooks in Clay](webhook-integration-guide.md).

## Enriching data with Google Sheets

1.  While in a Clay table, click `Tools` and search for `Google Sheets`.
2.  Under `Enrichments`, select one of the Google Sheets options.
3.  In the modal, you will be asked to `Select Google Sheets account`.
    -   If you haven't already connected your Google Sheets, click `+ Add account` and go through authentication.

### `Action` Add row

Add a row to a Google Sheet via its URL.

**Inputs**

-   **Google Spreadsheet URL**

### `Action` Lookup row

Lookup a row in a Google Sheet using a column and a value.

**Inputs**

-   **Google Spreadsheet URL**

### `Action` Lookup, add, or update row

Lookup a row in a Google Sheet using a column and a value. Optionally, you can add a row if nothing is found, or update a row if something is found.

**Inputs**

-   **Google Spreadsheet URL**

### **Run settings**

-   **Auto-update**
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))

## Troubleshooting

### 401 error when connecting your Google account

If you see a **401 error** from Google when connecting your Google account to Clay (for example, "The server cannot process the request because it is malformed"), Google is blocking Clay's authorization request. This is most commonly caused by a Google Workspace admin restriction on your account.

-   **If you're on a personal Google account**, try disconnecting and reconnecting your Google account. In Clay, go to your workspace `Settings` → `Connections`, remove the Google account, and re-add it.

-   **If you're on a Google Workspace (company) account**, your Google Workspace admin needs to add Clay as a trusted app:

    1.  In the [Google Workspace Admin Panel](https://admin.google.com/), go to `Security` → `API Controls` → `App Access Control`.
    2.  Click `Configure new app`.
    3.  Search for `Clay` and select it from the results.
    4.  Choose which org units should have access, then click `Continue`.
    5.  Select `Trusted` under **Access to Google Data** and click `Continue`.
    6.  Review the summary and click `Finish`.

    **Note:** Changes in Google Admin can take up to 24 hours to apply. Once complete, return to Clay and reconnect your Google account.

### Sheet ID and column mapping fields are not visible

If you open a Google Sheets action or source and the **Sheet ID** or column mapping fields do not appear, the most likely cause is that the connected Google account does not have access to the spreadsheet — for example, if you connected a different Google account than the one that owns or was shared on the sheet.

**To fix:** In Clay, go to your workspace `Settings` → `Connections`, remove the Google Sheets connection, and reconnect with the Google account that has access to the spreadsheet. Once reconnected, the Sheet ID and column mapping fields will appear.

### Lookup rows are slow or return errors

If rows using a **Lookup row** or **Lookup, add, or update row** enrichment run slowly or fail with errors, the Google Sheets API rate limit is the most likely cause. According to Google's published API documentation, the Google Sheets API enforces a default limit of 300 read requests per minute per project. When Clay's integration exceeds this limit, Google temporarily blocks further requests until the quota resets — typically after one minute.

Clay automatically retries rate-limited requests using exponential backoff, so most quota errors resolve without manual intervention. If rows remain in an error state after automatic retries are exhausted, re-running them after a brief pause will usually succeed once the quota window has reset.
