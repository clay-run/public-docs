---
title: HTTP API
description: Facilitate seamless integration and connectivity with any APIs.
last_synced: 2026-04-26T01:40:08.701Z
---

# HTTP API

Facilitate seamless integration and connectivity with any APIs.

HTTP API helps you send or retrieve data from any tool or database using an API endpoint. From pulling Gong transcripts into your Clay table to referencing Marketo's API, you can call any API, even if Clay does not offer a native integration.

An **HTTP API** uses HTTP methods (GET, POST, PUT, DELETE) to enable communication between different systems. An API is a set of defined rules that allow applications to interact with each other, while HTTP is the protocol that defines how these requests and responses are formatted and transmitted.

**Tip:** Looking for Clay's API? Try [this guide](https://university.clay.com/docs/using-clay-as-an-api).

### Common use cases

-   Pull customer data from your CRM.
-   Create leads in your marketing platform.
-   Update contact information in your database.
-   Access public datasets (NYC Open Data, government APIs).
-   Connect to custom tools without native Clay integrations.
-   Push enriched records to a data warehouse or data lake (e.g., POST to an AWS API Gateway endpoint that writes to S3).

## Choose your path

Before you begin, decide which approach fits your needs.

### 🔄 HTTP API enrichment (most common)

Use this when you want to add API data to existing rows in your Clay table.

-   ✅ Process data row by row.
-   ✅ Add information to existing records.
-   ✅ Works with any API endpoint.

👉 Jump to enrichment setup (see below).

### 📥 HTTP API as source

Use this when you want to import data from an API to create a new table.

-   ✅ Import datasets from external APIs.
-   ✅ Build lists from third-party services.
-   ✅ Start workflows with external data.
-   ✅ Pagination support for up to 50,000 rows.

👉 Jump to source setup (see below).

### Not sure which to choose?

-   **Already have a list** of companies, people, or records in Clay? → Use **enrichment**
-   **Need to pull a list** from an external API? → Use **as source**

## Storing authentication credentials at the workspace level

Instead of entering API keys or bearer tokens manually in the `Headers` field each time, you can save your auth credentials in an **HTTP API (Headers) account**. Clay encrypts and stores the headers at the workspace level, making them reusable across any HTTP API enrichment column.

**Setting up an HTTP API (Headers) account from the enrichment panel:**

1.  Open your Clay table and click `Add enrichment`.
2.  Search for and select `HTTP API`.
3.  In the enrichment panel, click the `Select header account` dropdown.
4.  Click `+ Add account`.
5.  Under `API Request Headers`, add your auth credentials as key-value pairs — for example:
    -   **Key:** `Authorization` | **Value:** `Bearer YOUR_TOKEN`
    -   **Key:** `X-API-KEY` | **Value:** `YOUR_API_KEY`
6.  Name the account (e.g., `Stripe API Key`) and click `Save`.
7.  The saved account will now appear in the `Select header account` dropdown. Select it to apply the headers to this enrichment.

**Note:** You can also manage existing accounts at any time from `Settings → Connections`. Keep in mind that editing a saved account will affect every HTTP API enrichment column across your workspace that uses it.

## HTTP API enrichment

### Prerequisites

Before configuring HTTP API, gather these details from your API documentation:

-   **HTTP method**: GET, POST, PUT, or DELETE
-   **Endpoint URL**: The specific API endpoint address
-   **Authentication**: API key, bearer token, or other credentials
-   **Parameters**: Headers, query parameters, or body content as specified by the API

**Pro tip**: Always have the API documentation open before setting up HTTP API. Search for "{Platform\_name} API Documentation" online (e.g., "Gong API Documentation").

### Setup method: choose your approach

When you add HTTP API to your table, you'll see two tabs: **Generate** (AI-assisted) and **Configure** (manual). Choose the method that works best for you.

## ⭐ Option A: AI-assisted setup (recommended)

Clay's **Sculptor** feature uses AI to automatically generate HTTP API configurations from natural language descriptions. This is now the default and recommended approach for most users.

### When to use AI-assisted setup

-   ✅ You have API documentation available.
-   ✅ You want faster, error-free setup.
-   ✅ You're not familiar with API configuration.
-   ✅ You want to avoid manual JSON formatting.

95% of users find AI-assisted setup faster and more reliable than manual configuration.

### How it works

**Step 1: Add HTTP API enrichment**

1.  Open your Clay table.
2.  Click **Add enrichment**.
3.  Search for and select **HTTP API**.
4.  You'll automatically land on the **Generate** tab.

**Step 2: Describe what you want**

In natural language, describe what you want to accomplish.

**Examples:**

-   "Find me the average temperature using OpenMeteo, using latitude and longitude"
-   "Get customer data from Stripe using customer ID"
-   "Create a new contact in HubSpot with name and email"

**You don't need to specify:**

-   Exact column names
-   Technical parameters
-   HTTP methods
-   Header formatting

**Step 3: Add API documentation (optional)**

Paste a link to the API's documentation. This helps Sculptor better understand the API's capabilities and improve accuracy.

While helpful, Sculptor can often figure out the configuration without it.

**Step 4: Generate configuration**

Click **Generate API connection**.

Sculptor will automatically:

-   Map your table columns to API parameters.
-   Select the correct endpoint and method.
-   Configure query parameters and optional fields.
-   Set up authentication headers.
-   Structure the request body for POST/PUT requests.

**⏱️ Note**: Processing time can vary. Be patient while Sculptor analyzes your request.

**Step 5: Review the configuration**

Sculptor shows you a summary of what it configured:

-   Which columns were mapped
-   What optional fields were set
-   Authentication setup
-   Request structure

**Step 6: Test before running**

1.  Switch to the **Configure** tab to review detailed settings.
2.  Click **Test** to run on a single row.
3.  Verify the response data matches your needs.
4.  Adjust any settings if needed.

**Step 7: Run on your table**

Once verified, run the enrichment on your full table.

### Troubleshooting with AI

If you encounter errors, you can use Sculptor to help diagnose issues:

-   Paste error messages for suggested fixes.
-   Share API docs to verify configuration.
-   Get help interpreting unexpected responses.

Sculptor understands common API patterns and can guide you through authentication issues, body formatting problems, and other configuration challenges.

### Tips for best results

-   **Provide complete information**: Share the full API documentation URL when possible.
-   **Review before running**: Verify the AI-generated configuration makes sense.
-   **Test first**: Run on a single row before processing your entire table.
-   **Save as template**: After successful setup, save your configuration for future use.
-   **Throttle request speed if needed**: If the target API enforces rate limits (e.g. Apollo, HubSpot), switch to the **Configure** tab and scroll to the **Custom rate limit** section to limit how many requests per time window Clay sends. See Step 7 in the manual configuration section below for details.

## Option B: Manual configuration

Choose manual configuration if you need precise control or have complex requirements. You can also switch to the **Configure** tab at any time to adjust AI-generated settings.

### Step 1: HTTP method

Select the HTTP method based on what you want to do:

-   **GET** - Retrieve data (e.g., pull customer data from your CRM, fetch a list of users)
-   **POST** - Create new data (e.g., create a new lead in your marketing platform, create a new contact)
-   **PUT** - Update existing data (e.g., update contact information in your database, modify user information)
-   **DELETE** - Remove data (e.g., remove outdated records, delete a record)

### Step 2: API endpoint URL

Enter the complete URL where your request will be sent.

### Step 3: Query string parameters

Add parameters to filter or refine your request. These appear in the URL after a `?` symbol.

**Example:**

-   **Key:** email + **Value:** /Email Column
-   **Key:** status + **Value:** active

### Step 4: JSON body

For POST and PUT requests, specify the data to send in the request body.

**Important JSON formatting rules:**

-   ✅ String values need quotes: `"name": "Sam"`
-   ✅ Numbers and booleans don't: `"age": 30`, `"active": true`
-   ✅ Dynamic column references for strings need quotes: `"email": "/Email Column"`
-   ✅ Dynamic column references for numbers don't: `"count": /Score Column`
-   ⚠️ Exception: Numbers with trailing zeros (e.g., `0004`) need quotation marks

**⚠️ Column references must be inserted as chips, not typed as text**

In Clay's body editor, column values appear as **colored chips** (dynamic tokens), not plain text strings. To insert a column chip:

1.  Click inside the body editor where you want the reference.
2.  Type `/` to open the column picker.
3.  Select the column name — it inserts as a colored pill.

If you type `/Column Name` as literal text without using the picker, Clay sends the string `/Column Name` to your API — **not** the column's actual value. For example, typing `/contact_status` sends `"/contact_status"` to the receiving server instead of the real value (e.g., `"ready"`). This is the most common cause of unexpected literal strings appearing in API payloads.

**Number chips and type precision**: A chip wrapped in quotes (e.g., `"count": "/Score Column"`) sends the value as a string — your server receives `"3"`, not `3`. Remove the surrounding quotes if your backend requires a native number type.

**Token mode vs. formula mode**

The Body editor has two modes, toggled via the ⚙️ gear icon in the top-right corner of the editor:

-   **Token mode** (default): Write your JSON structure directly and use `/` to insert column values as colored chip references. Best for most use cases.
-   **Formula mode**: Write any Clay formula expression (e.g., `Concatenate(...)`, `If(...)`) that returns a valid JSON string. Clay evaluates the formula before sending the request. Switch to this mode when you need logic that can't be expressed with chip references alone.

**⚠️ Warning:** Typing formula syntax in token mode without switching to formula mode treats it as literal JSON text — causing a "Failed to parse body input" error at runtime.

**How chip tokens handle complex values**

In token mode, every column chip inserted via the `/` picker is automatically JSON-serialized before the request is sent — strings, numbers, objects, and arrays all serialize correctly, including columns that return nested objects.

**⚠️ Important:** This auto-serialization only applies to direct chip tokens, not to formula expressions. If you use formula mode with an expression that accesses a sub-property of an object column — for example, `{{My Column}}?.[\"Key Name\"]` where "Key Name" is itself a nested object — that intermediate JavaScript value is **not** auto-serialized. Your API will receive the string `[object Object]` instead of the actual data.

**Fix:** Extract the sub-property into its own formula column first, then reference that column as a chip in the HTTP body via the `/` picker. Chip tokens are always auto-serialized, even when the column value is a complex object or array.

**Example body configuration:**

```javascript
{
  "firstName": "/First Name Column",
  "lastName": "/Last Name Column",
  "email": "/Email Column",
  "score": /Score Column,
  "subscribed": true
}
```

**Common mistake:**

```javascript
❌ Wrong: {"name": /Name Column}
✅ Correct: {"name": "/Name Column"}

❌ Wrong: {"name": "John" "age": 30}
✅ Correct: {"name": "John", "age": 30}
```

**Per-field required toggle**

Each field in the body editor has a small toggle to its left. This toggle controls whether that field **must have a value for the row to run**:

-   **Toggle ON (enabled):** Clay requires a value in the referenced column before running. If the column is empty or null for a row, the action is blocked and the cell shows **"Some inputs missing"**.
-   **Toggle OFF (optional):** The action runs for that row even when the column is empty — Clay bypasses the blank-column validation check. Without the global **Remove empty values** toggle (Step 8), the empty field is still sent in the payload as `null`; enable **Remove empty values** as well to strip empty fields from the payload entirely. Use this for any body field that isn't always populated — whether the API considers it optional (for example, `first_name`) or your data simply doesn't have a value for that field on every row (for example, `jobs_2` and `jobs_3` when not every record has multiple jobs). If several body fields may be empty on different rows, turn the toggle off for each of those fields individually.

**Note:** The global **Remove empty values** toggle (Step 8) strips null values from the outgoing payload at runtime — it does **not** prevent "Some inputs missing" errors, which fire before the action runs when a required token is blank. Marking an input as **Optional** in the Column Mapping section also does not change per-field body toggle states — each body field's toggle must be turned off separately in the body editor.

### Step 5: Header fields

Headers provide authentication and specify data formats. Add them as key-value pairs.

**Common header examples:**

**Authorization (bearer token):**

-   Key: Authorization
-   Value: Bearer YOUR\_API\_TOKEN\_HERE

**API key in header:**

-   Key: X-API-Key
-   Value: YOUR\_API\_KEY\_HERE

**Content type (automatically set in Clay):**

-   Key: Content-Type
-   Value: application/json

**⚠️ Common mistake**: Some data providers (like Apollo) have different API keys for different endpoints. Make sure you're using the correct key for your specific endpoint.

### Step 6: Field paths to return

Specify which parts of the API response you want to retrieve. Use this to filter out unnecessary data.

**Example API response:**

```javascript
{
  "data": {
    "user": {
      "id": 12345,
      "name": "John Doe",
      "email": "john@example.com"
    }
  }
}
```

**Field path to extract email:**

```javascript
data.user.email
```

**This returns only:** `john@example.com`

**Benefits:** Faster processing, cleaner data, easier to work with.

### Step 7: Custom rate limit

Throttle how many requests Clay sends to the API within a given time window. This is a **column-level** setting — it applies uniformly to every row the column processes. Open the column settings and scroll to the **Custom rate limit** collapsible section on the **Configure** tab.

**Fields:**

-   **Request Limit** — the maximum number of requests allowed in the time window.
-   **Duration (in ms)** — the length of the time window in milliseconds (1 to 900,000 ms, i.e. up to 15 minutes).

**Constraint:** The rate limit must average at least 1 request per second — for example, `Request Limit: 1, Duration: 1000 ms` is the slowest setting allowed.

**Example — 100 requests per minute:**

```javascript
Request Limit: 100
Duration (ms): 60000
```

**⚠️ Common mistake — setting Request Limit to your total row count:** The rate limit is a sliding window that repeats throughout the run, not a one-time total. Setting `Request Limit: 4000, Duration: 145000 ms` means Clay tries to send 4,000 requests within every 145-second window — not 4,000 requests total. Check the target API's documentation for its stated rate limit (e.g., "100 requests per minute") and match those values.

### Step 8: Remove empty values

Toggle **ON** to automatically strip fields with empty, null, or undefined values from the payload Clay sends to the API.

**Why use this:**

-   Prevents overwriting existing data with blank values when updating records.
-   Avoids sending unexpected null values to APIs that reject them.
-   Keeps requests clean and efficient.

**Note:** This toggle operates on the outgoing payload at execution time. It does **not** prevent the **"Some inputs missing"** error — that error fires before the action runs when a body field's per-field toggle is ON but the referenced column has no value. To suppress "Some inputs missing" for optional fields, turn off the per-field toggle for that field in the body editor (see Step 4 above).

### Step 9: Retry on failure

Clay can automatically retry a failed request when certain HTTP status codes or network errors occur. The **Retry on failure** toggle is **enabled by default**.

**Default retry behavior:**

-   **Status codes retried:** 408 (Request Timeout), 413 (Payload Too Large), 429 (Rate Limited)
-   **Network errors retried:** `ECONNREFUSED`, `ECONNRESET`, `ETIMEDOUT`
-   **Max retries:** 1 (configurable up to 5)

Retries fire immediately with no delay between attempts.

**Customizing retry settings:**

When **Retry on failure** is enabled, three optional sub-settings appear on the **Configure** tab:

-   **Max retries** — number of retry attempts before the row errors out (1–5; default 1).
-   **Status codes to retry** — comma-separated list of 4XX/5XX codes to retry. Use `-` for ranges (e.g., `429`, `500-503`). When provided, overrides the defaults.
-   **Error codes to retry** — comma-separated list of Node.js network-level error code strings (e.g., `ECONNRESET`, `ETIMEDOUT`, `ECONNREFUSED`). When provided, overrides the defaults. **Note:** This field only accepts Node.js error code strings — not numeric HTTP status codes. To retry on a specific HTTP status code (such as `429`), add it to **Status codes to retry** instead.

To disable all retry logic for a column, toggle **Retry on failure** OFF.

**Note:** Retry on failure responds to HTTP status codes and network errors only — not to values inside the response body. For example, if your API returns `{"status": "processing"}` in a 200 response, there is no built-in way to retry on that field value. To re-run a column based on a response field value, use **Conditional runs** ("Only run if") instead — see the Advanced options section below.

## Advanced options

### Using integration templates

Click the **Browse templates** button at the top of the integration window to access pre-configured setups for common use cases.

**Benefits:**

-   ⚡ Faster setup - Configure in seconds
-   🎯 Reduced errors - Pre-tested configurations
-   📚 Learning tool - See proper API structure

After using a template, you can adjust any settings to match your specific needs.

### Conditional runs

Set up conditional run formulas to only execute HTTP API when required data is present. This prevents unnecessary API calls, error messages, and wasted credits.

**Example:** Only run if email column is not empty.

### Testing and validation

Before running on your entire table:

1.  ✅ Test with a single row.
2.  ✅ Verify the configuration works.
3.  ✅ Check the response data.
4.  ✅ Then run on full table.

**Why:** Saves credits and catches errors early.

## HTTP API as source

HTTP API as source allows you to import data directly from any HTTP API into Clay tables as a starting point for list building.

### When to use this

Use HTTP API as source when you want to:

-   ✅ Build lists from external APIs.
-   ✅ Import datasets from third-party services.
-   ✅ Create tables from endpoints returning multiple records.
-   ✅ Start workflows with external data.

**Example use cases:**

-   Pulling trip hazards from NYC Open Data API
-   Importing event listings or class schedules
-   Fetching product catalogs from e-commerce APIs
-   Retrieving fantasy sports team data
-   Accessing government or public datasets

### Setup steps

**Step 1: Start import**

1.  Click **Tools** → **View all sources**.
2.  Search for **Import data from an HTTP API**.
3.  Select it.

**Step 2: Configure account (required)**

Select or create an account that contains your API authentication. Accounts are mandatory for sources because they securely store sensitive information like API keys and authorization tokens.

**Step 3: Configure request**

Configure your request settings:

-   **Method**: Select HTTP method (typically GET for imports)
-   **Endpoint**: Enter the API endpoint URL
-   **Query parameters**: Add key-value pairs for filtering data
-   **Headers**: Add authentication and other required headers
-   **Body**: Add request body if needed (for POST/PUT methods)

**Step 4: Specify results path**

This is a critical step unique to sources. Tell Clay exactly where in the API response your data array is located.

**Example:** If your API returns:

```javascript
{
  "items": [...],
  "total": 10
}
```

You'd specify `items` as the results path.

Most APIs nest their data within a specific field rather than returning an array at the root level.

**Step 5: Configure optional settings**

-   **Pagination**: Automatically fetch multiple pages of results up to 50,000 rows. See [Pagination](#pagination) below.
-   **Use static IP**: Route requests through Clay's fixed egress IPs for firewall allow-listing. See [IP allowlisting](#ip-allowlisting) below.
-   **Remove empty values**: Exclude null or empty fields
-   **Follow redirects**: Set max redirects if needed
-   **Response timeout**: Specify timeout in milliseconds (minimum 1,000 ms; maximum 100,000 ms). Clay rejects values above 100,000 ms with the error **"Response timeout must be less than 100000ms."**
-   **Retry on failure**: Configure retry attempts and conditions

**Step 6: Preview and import**

1.  Preview the API response to verify the data structure.
2.  Map the API response fields to table columns.
3.  Import the data to create your new table.

### Pagination

HTTP API as source supports automatic pagination for up to 50,000 rows. To enable it, open the **Pagination** dropdown in the source configuration and choose a mode:

-   **Update query parameter(s)**: Injects parameters into the query string on each subsequent request. Use the reserved tokens `$offset` (total records fetched so far), `$page` (1-based page number), or `$pageZeroIndex` (0-based page number) as values — or reference a field from the previous response using dot notation (e.g. `meta.next_cursor`).
-   **Update body parameter(s)**: Same as above, but merges parameters into the request body instead of the query string.
-   **Response contains next URL**: Reads a full URL from the response body (e.g. at path `links.next`) and uses it as the endpoint for the next request. Stops when that path is empty or matches the current URL.

**Additional stop conditions (optional):**

-   **Stop when this path is empty**: Enter a dot-path into the response (e.g. `has_more`). Pagination stops when the value at that path is falsy.
-   **Total pages path**: Enter a dot-path that resolves to the total page count (e.g. `pagination.totalPages`). Pagination stops once that many pages have been fetched.

Pagination always stops at 50,000 rows regardless of other settings.

**Availability:** HTTP API as source (including pagination) is available on Explorer and above plans.

### Limitations

**⚠️ Important considerations:**

-   **Array output required**: Make sure the results path points to an array in the API response.
-   **Results path matters**: Take time to examine your API response structure. Some APIs nest data several levels deep (e.g., `data.results.items`).
-   **Account security**: Your API credentials are stored securely and won't be exposed in the table configuration.

## IP allowlisting

If your server or firewall requires incoming requests to originate from a known set of IP addresses, you can enable **Use static IP** on HTTP API columns. This routes requests from those columns through Clay's fixed egress IP addresses, which you can add to your server's allow-list.

**Availability:** This feature is available for Enterprise customers. Contact your Clay account team or support before enabling — static IP must be activated for your workspace first.

### Enabling static IP for an HTTP API enrichment column

1.  Contact your Clay account team or support to have static IP enabled for your workspace.
2.  Open the HTTP API column settings in your Clay table.
3.  At the bottom of the column configuration, toggle on **Use static IP**.

All requests from that column will then originate from Clay's fixed IP addresses. Your account team can provide the current list of IP addresses to add to your allow-list.

**Note:** Static IP for HTTP API is per column, not workspace-wide — you control exactly which columns route through fixed IPs.

### Enabling static IP for HTTP API as source

In Step 5 of the source configuration (**Configure optional settings**), toggle on **Use static IP**.

### Other integrations

For **Snowflake**, **Salesforce**, and **Databricks** connections on Enterprise plans, all requests already route through static IPs by default — no extra setup is needed in Clay. Add Clay's fixed IP addresses to your allow-list on the provider side.

## Best practices

### ✓ Start with documentation

Always review the API documentation before configuration. It contains everything you need: methods, endpoints, authentication, headers, parameters, and response formats.

### ✓ Use templates first

Browse HTTP API templates for pre-configured setups. Templates save time and reduce configuration errors.

### ✓ Test with one row

Before running on your entire table:

1.  Test with a single row.
2.  Verify the configuration works.
3.  Check the response data.
4.  Then run on full table.

**Why:** Saves credits and catches errors early.

### ✓ Secure authentication

-   Never hardcode API keys in requests.
-   Use Clay's built-in authentication features.
-   Store credentials securely.

### ✓ Set a custom rate limit

If the API documentation specifies rate limits, configure the **Custom rate limit** setting on the **Configure** tab of your HTTP API column. This is a column-level setting — it applies uniformly to all rows. The rate limit must average at least 1 request per second, and the duration can be up to 900,000 ms (15 minutes).

**Example:** 100 requests per minute

```javascript
Request Limit: 100
Duration: 60000 ms
```

**Note:** The rate limit is a sliding window applied repeatedly throughout the run — not a total request count. Set **Request Limit** to the API's documented per-window limit (e.g., 100 requests per 60,000 ms), not to your total number of rows.

### ✓ Optimize with field paths

For large API responses, specify only needed fields:

```javascript
data.users.email
data.users.name
```

**Benefits:** Faster processing, cleaner data, easier to work with.

### ✓ Use conditional runs

Set up conditional run formulas to only execute HTTP API when required data is present.

**This prevents:**

-   Unnecessary API calls
-   Error messages
-   Wasted credits

### ✓ Document complex setups

For complex HTTP API configurations:

-   Add notes about what each setting does.
-   Document field mappings.
-   Include example responses.

**Benefits:**

-   Makes troubleshooting easier.
-   Simplifies replication to other tables.

## Troubleshooting

### "Token has expired" or "Unauthorized" (401 error)

This error means the API credentials in your HTTP API action are no longer valid. Many platforms — including sequencers, CRMs, and outreach tools — issue tokens that expire after a period of time.

**How to fix:**

1.  **Generate a new token** in the external platform (e.g., your sequencer or CRM). Check that platform's settings or developer docs for where to create or rotate API keys.
2.  **Update the token in Clay:**
    -   **If you saved the token in a header account:** Go to `Settings → Connections`, find your HTTP API (Headers) account, and click **Edit**. Existing header values are not shown (they're stored encrypted for security) — re-enter all your headers from scratch, including `Authorization: Bearer YOUR_NEW_TOKEN` and any other keys you had configured, then save. This updates every HTTP API column in your workspace that uses that account at once.
    -   **If you entered the token directly in the column:** Open the HTTP API column settings, go to the `Headers` section, and replace the old token value with the new one.
3.  **Test with a single row** to confirm the new token works before re-running your full table.

**Tip:** Saving credentials in a header account (`Settings → Connections`) is the easiest way to manage token rotation — when a token expires, you only need to update it in one place instead of editing every column individually.

### "Clay received a 429 error from the API" (Too Many Requests)

A 429 error means the external API is rejecting requests because Clay is sending them faster than the API's rate limit allows. To fix this:

1.  Check the external API's documentation for its rate limit — for example, "10 requests per second" or "100 requests per minute."
2.  Open your HTTP API column settings and go to the **Configure** tab.
3.  Scroll to the **Custom rate limit** section and set:
    -   **Request Limit** — the number of requests allowed in the time window (e.g., `10`).
    -   **Duration (in ms)** — the length of that window in milliseconds (e.g., `1000` for 1 second, `60000` for 1 minute).
4.  Save and re-run. Clay throttles requests automatically to stay within this limit.

**Example — 10 requests per second:**

```javascript
Request Limit: 10
Duration (ms): 1000
```

See [Step 7: Custom rate limit](#step-7-custom-rate-limit) for full field details and constraints.

**Tip:** Clay also retries 429 responses once by default (see [Step 9: Retry on failure](#step-9-retry-on-failure)). Configuring a custom rate limit prevents 429s from occurring in the first place, rather than just retrying after they happen.

### "Body parse error" or in-editor JSON syntax error

This error indicates a formatting issue in your JSON body. It can appear in two forms:

-   **Inline (before running):** A red message below the body editor — for example, *"Expected ',' or '}' after property value in JSON at position X (line Y column Z)"*. This appears as you type and means your JSON has a syntax problem: a stray character, missing comma, unclosed quote, or unexpected text placed after a column chip.
-   **After running:** A 400 response with "Body parse error" returned by the server.

Both have the same root cause — malformed JSON — and the same fixes.

**Common fixes:**

**1\. Add quotes around string variables**

```javascript
❌ Wrong: {"name": /Name Column}
✅ Correct: {"name": "/Name Column"}
```

**2\. Check punctuation**

```javascript
❌ Wrong: {"name": "John" "age": 30}
✅ Correct: {"name": "John", "age": 30}
```

Ensure keys are separated by commas. Watch for extra spaces, colons, and brackets.

**3\. Remove hidden characters**

-   Copy your body into a plain text editor.
-   Look for invisible characters from API docs.
-   Clean and repaste into Clay.

**4\. Verify correct API key**

Some providers have multiple API keys for different endpoints. Example: Apollo has separate keys for different APIs.

**5\. Formula expression entered in token mode**

If you used a Clay formula (e.g., `Concatenate()`, `If()`) to build the JSON body and the editor is in its default **token mode**, Clay treats the formula syntax as literal JSON — causing a parse error.

**Fix:** Click the ⚙️ gear icon in the Body editor and select **Formula**. This switches to a full Clay formula editor where your expression is evaluated before the request is sent. Alternatively, remove the formula and rewrite the body in token mode using `/` to insert column values as chip references — for example, `{"email": "/Lead's Email", "score": /Lead Score}`.

### "Some inputs missing" error

This error appears in the cell when a body field's per-field toggle is **ON** (required to run) but the referenced column has no value for that row. Expanding the cell detail shows the more specific message: **"Body has the error(s): [field name] is blank"**.

**How to fix:**

**Option 1 — Turn off the per-field toggle for that field**

In the body editor, find the field causing the error and click the small toggle to its left to switch it from ON to OFF. The action will now run for rows where that column is empty. Without the **Remove empty values** toggle, the empty field is still sent as `null` in the payload — enable **Remove empty values** (Step 8) as well if you want empty fields omitted from the payload entirely. If multiple body fields can be empty on different rows — for example, `jobs_1`, `jobs_2`, `jobs_3` where not every record has three jobs — turn off the per-field toggle for **each** of those fields individually (and enable Remove empty values to omit empty entries from the payload).

**Option 2 — Add a conditional run**

Under **Advanced options → Conditional run**, add a formula that only runs the action when the required column has a value — for example, `!!{{Email}}` to skip rows where the email column is empty.

**Note:** Turning on the global **Remove empty values** toggle does **not** fix this error on its own. "Remove empty values" strips null values from the outgoing payload at execution time, but "Some inputs missing" fires before execution when a required body field's column is blank. You need to turn off the per-field toggle first (so the action runs), then optionally enable Remove empty values (so the empty field is omitted from the payload rather than sent as null).

### Clicking Run does nothing — no loading, no error, no cell update

If clicking **Run** on your HTTP API column produces no loading indicator, no response, and no cell update — whether via the column header dropdown or the Play icon on individual cells — the body formula likely has column references that can't be resolved.

**How to confirm:** Right-click the column header and choose **Edit column**. If you see a red error inside the body editor — for example, *"Settings contains deleted column for 'body' input"* — one or more column references in the body were saved as display names rather than internal field IDs. This can happen when column chips are edited in ways that bypass the `/` picker, or when referenced columns were renamed after the body was configured. Clay silently blocks all execution when this settings error is present: the Run option may be absent from the column header dropdown entirely, and clicking the cell-level Play icon produces no result.

**How to fix:**

1.  Open the HTTP API column editor.
2.  In the **Body** field, delete all existing column chip references.
3.  Re-insert each column value by typing `/` inside the body editor and selecting the column from the picker — this saves each reference as an internal field ID rather than a display name.
4.  Save and test on a single row.

**Note:** If the column was working before and stopped responding, try a hard refresh first (**Mac:** Cmd + Shift + R · **Windows:** Ctrl + Shift + R) to rule out a browser display glitch. If clicking Run still produces nothing after the refresh, use the body fix above.

### Column value appears as `[object Object]` in the request body

The API receives the literal string `[object Object]` instead of JSON data.

**Why this happens:** In token mode, every column chip inserted via the `/` picker is automatically JSON-serialized before the request is sent. In formula mode, expressions that access sub-properties of object columns — such as `{{Column}}?.[\"Key Name\"]` where "Key Name" is itself a nested object — are **not** auto-serialized. When Clay coerces that JavaScript object to a string, it produces `[object Object]`.

This most commonly surfaces when:
-   You're pulling values out of a complex enrichment result (e.g. function inputs, AI output objects) using `?.[\"Key\"]` inside a formula expression.
-   You're using `_.join()` or string concatenation in formula mode where one of the values is a nested object.

**Fix:**

1.  Create an **intermediate formula column** that extracts the value you need — e.g. `{{Enrichment Column}}?.[\"Key Name\"]`.
2.  In your HTTP body (token mode), insert that formula column as a **chip** via the `/` picker.

The chip token is automatically serialized, even when the column value is a complex object or array.

### Hidden characters in API documentation

When copying from API documentation:

1.  Paste into a plain text editor first.
2.  Check for hidden characters.
3.  Remove any found.
4.  Copy clean text into Clay.

This reveals any hidden characters that might cause parsing errors.

### Multiple API keys

Some data providers (like Apollo) have different API keys for different endpoints. Make sure you're using the correct key for your specific endpoint.

### Using AI to diagnose issues

If you encounter errors, use Sculptor to help:

-   Paste error messages for suggested fixes.
-   Share API docs to verify configuration.
-   Get help interpreting unexpected responses.

### "Response timeout must be less than 100000ms" error

This error appears when you set the **Response timeout** field to a value above its maximum of 100,000 ms (100 seconds). Clay enforces a hard limit on this field and rejects higher values before the request is sent.

**How to fix:** Lower the response timeout to 100,000 ms or below.

**If your API routinely takes longer than 100 seconds to respond:** Design your endpoint to acknowledge the request quickly — within the timeout window — and offload the heavy processing to an asynchronous job. Write the results back to Clay via a [webhook](webhook-integration-guide.md) or a follow-up API call once processing completes.

## FAQs

### Does using HTTP API consume Data Credits?

No. HTTP API calls consume 1 Action per run but do not use any Data Credits. Since HTTP API calls reach external endpoints directly — rather than purchasing data through Clay's marketplace — no Data Credit charge applies. This holds regardless of which HTTP method you use (GET, POST, PUT, or DELETE). For a full breakdown of how Actions and Data Credits work together, see [Actions & Data Credits](https://www.clay.com/university/guide/actions-data-credits).

### Why do I need quotation marks around dynamic string variables?

As of October 2024, you must enclose dynamic string variables in quotation marks when using the HTTP API enrichment column. This ensures proper JSON formatting.

‍**Example:**

```javascript
✅ Correct: {"email": "/Email Column"}
❌ Wrong: {"email": /Email Column}
```

### What if a data provider has multiple API keys?

Some data providers have multiple API keys for different APIs. For example, Apollo has several APIs you can create keys for. Make sure you're using the correct API key for the specific endpoint you're calling.

### How do I handle hidden characters in API documentation?

When copying from API documentation, paste your code into a plain text editor first. This reveals any hidden characters that might cause parsing errors. Remove them before pasting into Clay.

### When should I use HTTP API as source vs. enrichment?

-   Use **enrichment** if you already have a list of records in Clay and want to add API data to them.
-   Use **as source** if you need to pull a list from an external API to create a new table.

### Can I use HTTP API with pagination?

Yes. HTTP API as source supports automatic pagination for up to 50,000 rows. Three modes are available: update query parameters on each request (useful for offset/limit or page-based APIs), update body parameters, or follow a next URL returned in the response (useful for cursor-based APIs). See [Pagination](#pagination) for full setup details.

### Can I use HTTP API to push enriched data to AWS (e.g., S3 via API Gateway)?

Yes. Use the **HTTP API enrichment** with a **POST** method to send enriched records to an AWS API Gateway endpoint. Set up API Gateway to trigger a Lambda function that writes the payload to S3 (or another AWS data store).

**Important — AWS authentication method matters:** This pattern works when your API Gateway is configured with **API key or header-based authentication**. API Gateway endpoints secured with **AWS IAM (SigV4 signing)** are not compatible with Clay's standard header-based auth. Confirm your API Gateway's authentication method before building the workflow.

**Note:** HTTP API enrichment processes one row at a time — each cell sends a separate POST request to your endpoint. There is no native batch mode.

### Can I paste a cURL request directly into Clay?

There is no "paste cURL" button, but you can replicate any cURL request by manually mapping its components to the HTTP API configuration fields.

Given a cURL command like:

```bash
curl -X POST "https://api.example.com/contacts" \
  -H "Authorization: Bearer YOUR_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"email": "jane@example.com", "company": "Acme"}'
```

Map each part as follows:

| cURL component | Where it goes in Clay |
|---|---|
| `-X POST` (or `-X GET`, etc.) | **Method** dropdown |
| The URL (`https://api.example.com/contacts`) | **Endpoint URL** field |
| `-H "Authorization: Bearer ..."` | **Headers** (key: `Authorization`, value: `Bearer YOUR_TOKEN`) |
| `-H "Content-Type: application/json"` | **Headers** (key: `Content-Type`, value: `application/json`) |
| `-d '{...}'` / `--data '{...}'` | **Body** field — replace static values with Clay column references (e.g. `"/Email Column"`) |
| `?key=value` query params in the URL | **Query string parameters** section |

**Decide which Clay feature to use:**

-   **Pulling records in as rows** (e.g. fetching a list from an API to start a table): use **HTTP API as source** (Tools → View all sources → Import data from an HTTP API).
-   **Calling an API once per row** (e.g. enriching existing records): use the **HTTP API enrichment column** (Add enrichment → HTTP API).