---
title: HTTP API
source_url: https://university.clay.com/docs/http-api-integration-overview
---

# HTTP API

Facilitate seamless integration and connectivity with any APIs.

## Overview

HTTP API helps you send or retrieve data from any tool or database using an API endpoint. From pulling Gong transcripts into your Clay table to referencing Marketo's API, you can call any API, even if Clay does not offer a native integration.

An **HTTP API** uses HTTP methods (GET, POST, PUT, DELETE) to enable communication between different systems. An API is a set of defined rules that allow applications to interact with each other, while HTTP is the protocol that defines how these requests and responses are formatted and transmitted.

**Tip:** Looking for Clay's API? Try [this guide](https://university.clay.com/docs/using-clay-as-an-api).

### Common use cases

- Pull customer data from your CRM.
- Create leads in your marketing platform.
- Update contact information in your database.
- Access public datasets (NYC Open Data, government APIs).
- Connect to custom tools without native Clay integrations.

## Choose your path

Before you begin, decide which approach fits your needs.

### HTTP API enrichment (most common)

Use this when you want to add API data to existing rows in your Clay table.

- Process data row by row.
- Add information to existing records.
- Works with any API endpoint.

### HTTP API as source

Use this when you want to import data from an API to create a new table.

- Import datasets from external APIs.
- Build lists from third-party services.
- Start workflows with external data.
- Note: No pagination support currently.

### Not sure which to choose?

- **Already have a list** of companies, people, or records in Clay? → Use **enrichment**
- **Need to pull a list** from an external API? → Use **as source**

## Storing authentication credentials at the workspace level

Instead of entering API keys or bearer tokens manually in the `Headers` field each time, you can save your auth credentials in an **HTTP API (Headers) account**. Clay encrypts and stores the headers at the workspace level, making them reusable across any HTTP API enrichment column.

**Setting up an HTTP API (Headers) account from the enrichment panel:**

1. Open your Clay table and click `Add enrichment`.
2. Search for and select `HTTP API`.
3. In the enrichment panel, click the `Select header account` dropdown.
4. Click `+ Add account`.
5. Under `API Request Headers`, add your auth credentials as key-value pairs — for example:
   - **Key:** `Authorization` | **Value:** `Bearer YOUR_TOKEN`
   - **Key:** `X-API-KEY` | **Value:** `YOUR_API_KEY`
6. Name the account (e.g., `Stripe API Key`) and click `Save`.
7. The saved account will now appear in the `Select header account` dropdown. Select it to apply the headers to this enrichment.

**Note:** You can also manage existing accounts at any time from `Settings → Connections`. Keep in mind that editing a saved account will affect every HTTP API enrichment column across your workspace that uses it.

## HTTP API enrichment

### Prerequisites

Before configuring HTTP API, gather these details from your API documentation:

- **HTTP method**: GET, POST, PUT, or DELETE
- **Endpoint URL**: The specific API endpoint address
- **Authentication**: API key, bearer token, or other credentials
- **Parameters**: Headers, query parameters, or body content as specified by the API

**Pro tip**: Always have the API documentation open before setting up HTTP API. Search for "{Platform_name} API Documentation" online (e.g., "Gong API Documentation").

### Setup method: choose your approach

When you add HTTP API to your table, you'll see two tabs: **Generate** (AI-assisted) and **Configure** (manual). Choose the method that works best for you.

## Option A: AI-assisted setup (recommended)

Clay's **Sculptor** feature uses AI to automatically generate HTTP API configurations from natural language descriptions. This is now the default and recommended approach for most users.

### When to use AI-assisted setup

- You have API documentation available.
- You want faster, error-free setup.
- You're not familiar with API configuration.
- You want to avoid manual JSON formatting.

95% of users find AI-assisted setup faster and more reliable than manual configuration.

### How it works

**Step 1: Add HTTP API enrichment**

1. Open your Clay table.
2. Click **Add enrichment**.
3. Search for and select **HTTP API**.
4. You'll automatically land on the **Generate** tab.

**Step 2: Describe what you want**

In natural language, describe what you want to accomplish.

**Examples:**

- "Find me the average temperature using OpenMeteo, using latitude and longitude"
- "Get customer data from Stripe using customer ID"
- "Create a new contact in HubSpot with name and email"

**You don't need to specify:**

- Exact column names
- Technical parameters
- HTTP methods
- Header formatting

**Step 3: Add API documentation (optional)**

Paste a link to the API's documentation. This helps Sculptor better understand the API's capabilities and improve accuracy.

While helpful, Sculptor can often figure out the configuration without it.

**Step 4: Generate configuration**

Click **Generate API connection**.

Sculptor will automatically:

- Map your table columns to API parameters.
- Select the correct endpoint and method.
- Configure query parameters and optional fields.
- Set up authentication headers.
- Structure the request body for POST/PUT requests.

**Note**: Processing time can vary. Be patient while Sculptor analyzes your request.

**Step 5: Review the configuration**

Sculptor shows you a summary of what it configured:

- Which columns were mapped
- What optional fields were set
- Authentication setup
- Request structure

**Step 6: Test before running**

1. Switch to the **Configure** tab to review detailed settings.
2. Click **Test** to run on a single row.
3. Verify the response data matches your needs.
4. Adjust any settings if needed.

**Step 7: Run on your table**

Once verified, run the enrichment on your full table.

### Troubleshooting with AI

If you encounter errors, you can use Sculptor to help diagnose issues:

- Paste error messages for suggested fixes.
- Share API docs to verify configuration.
- Get help interpreting unexpected responses.

Sculptor understands common API patterns and can guide you through authentication issues, body formatting problems, and other configuration challenges.

### Tips for best results

- **Provide complete information**: Share the full API documentation URL when possible.
- **Review before running**: Verify the AI-generated configuration makes sense.
- **Test first**: Run on a single row before processing your entire table.
- **Save as template**: After successful setup, save your configuration for future use.

## Option B: Manual configuration

Choose manual configuration if you need precise control or have complex requirements. You can also switch to the **Configure** tab at any time to adjust AI-generated settings.

### Step 1: HTTP method

Select the HTTP method based on what you want to do:

- **GET** - Retrieve data (e.g., pull customer data from your CRM, fetch a list of users)
- **POST** - Create new data (e.g., create a new lead in your marketing platform, create a new contact)
- **PUT** - Update existing data (e.g., update contact information in your database, modify user information)
- **DELETE** - Remove data (e.g., remove outdated records, delete a record)

### Step 2: API endpoint URL

Enter the complete URL where your request will be sent.

### Step 3: Query string parameters

Add parameters to filter or refine your request. These appear in the URL after a `?` symbol.

**Example:**

- **Key:** email + **Value:** /Email Column
- **Key:** status + **Value:** active

### Step 4: JSON body

For POST and PUT requests, specify the data to send in the request body.

**Important JSON formatting rules:**

- String values need quotes: `"name": "Sam"`
- Numbers and booleans don't: `"age": 30`, `"active": true`
- Dynamic column references for strings need quotes: `"email": "/Email Column"`
- Dynamic column references for numbers don't: `"count": /Score Column`
- Exception: Numbers with trailing zeros (e.g., `0004`) need quotation marks

**Example body configuration:**

```json
{
  "firstName": "/First Name Column",
  "lastName": "/Last Name Column",
  "email": "/Email Column",
  "score": /Score Column,
  "subscribed": true
}
```

**Common mistake:**

```
Wrong: {"name": /Name Column}
Correct: {"name": "/Name Column"}

Wrong: {"name": "John" "age": 30}
Correct: {"name": "John", "age": 30}
```

### Step 5: Header fields

Headers provide authentication and specify data formats. Add them as key-value pairs.

**Common header examples:**

**Authorization (bearer token):**

- Key: Authorization
- Value: Bearer YOUR_API_TOKEN_HERE

**API key in header:**

- Key: X-API-Key
- Value: YOUR_API_KEY_HERE

**Content type (automatically set in Clay):**

- Key: Content-Type
- Value: application/json

**Common mistake**: Some data providers (like Apollo) have different API keys for different endpoints. Make sure you're using the correct key for your specific endpoint.

### Step 6: Field paths to return

Specify which parts of the API response you want to retrieve. Use this to filter out unnecessary data.

**Example API response:**

```json
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

```
data.user.email
```

**This returns only:** `john@example.com`

**Benefits:** Faster processing, cleaner data, easier to work with.

### Step 7: Rate limiting

Control how many API requests you can send within a given time frame. Check your API documentation for rate limits.

**Example configuration:**

```
Request limit: 10
Duration (ms): 1000
```

**This means:** 10 requests per second

### Step 8: Remove empty fields from request

Toggle **ON** to automatically exclude empty, null, or undefined fields from your request.

**Why use this:**

- Prevents overwriting existing data with blank values.
- Avoids API errors from unexpected null values.
- Keeps requests clean and efficient.

## Advanced options

### Using integration templates

Click the **Browse templates** button at the top of the integration window to access pre-configured setups for common use cases.

**Benefits:**

- Faster setup - Configure in seconds
- Reduced errors - Pre-tested configurations
- Learning tool - See proper API structure

After using a template, you can adjust any settings to match your specific needs.

### Conditional runs

Set up conditional run formulas to only execute HTTP API when required data is present. This prevents unnecessary API calls, error messages, and wasted credits.

**Example:** Only run if email column is not empty.

### Testing and validation

Before running on your entire table:

1. Test with a single row.
2. Verify the configuration works.
3. Check the response data.
4. Then run on full table.

**Why:** Saves credits and catches errors early.

## HTTP API as source

HTTP API as source allows you to import data directly from any HTTP API into Clay tables as a starting point for list building.

### When to use this

Use HTTP API as source when you want to:

- Build lists from external APIs.
- Import datasets from third-party services.
- Create tables from endpoints returning multiple records.
- Start workflows with data from external sources.

**Example use cases:**

- Pulling trip hazards from NYC Open Data API
- Importing event listings or class schedules
- Fetching product catalogs from e-commerce APIs
- Retrieving fantasy sports team data
- Accessing government or public datasets

### Setup steps

**Step 1: Start import**

1. Click **Actions** → **View all sources**.
2. Search for **Import data from an HTTP API**.
3. Select it.

**Step 2: Configure account (required)**

Select or create an account that contains your API authentication. Accounts are mandatory for sources because they securely store sensitive information like API keys and authorization tokens.

**Step 3: Configure request**

Configure your request settings:

- **Method**: Select HTTP method (typically GET for imports)
- **Endpoint**: Enter the API endpoint URL
- **Query parameters**: Add key-value pairs for filtering data
- **Headers**: Add authentication and other required headers
- **Body**: Add request body if needed (for POST/PUT methods)

**Step 4: Specify results path**

This is a critical step unique to sources. Tell Clay exactly where in the API response your data array is located.

**Example:** If your API returns:

```json
{
  "items": [...],
  "total": 10
}
```

You'd specify `items` as the results path.

Most APIs nest their data within a specific field rather than returning an array at the root level.

**Step 5: Configure optional settings**

- **Use static IP**: Enable for allow-listing requirements
- **Remove empty values**: Exclude null or empty fields
- **Follow redirects**: Set max redirects if needed
- **Response timeout**: Specify timeout in milliseconds
- **Retry on failure**: Configure retry attempts and conditions

**Step 6: Preview and import**

1. Preview the API response to verify the data structure.
2. Map the API response fields to table columns.
3. Import the data to create your new table.

### Limitations

**Important considerations:**

- **Array output required**: Make sure the results path points to an array in the API response.
- **No pagination support**: Currently limited to single API calls. If your API returns paginated results, you'll only get the first page (typically 10-100 records).
- **Results path matters**: Take time to examine your API response structure. Some APIs nest data several levels deep (e.g., `data.results.items`).
- **Account security**: Your API credentials are stored securely and won't be exposed in the table configuration.

## Best practices

### Start with documentation

Always review the API documentation before configuration. It contains everything you need: methods, endpoints, authentication, headers, parameters, and response formats.

### Use templates first

Browse HTTP API templates for pre-configured setups. Templates save time and reduce configuration errors.

### Test with one row

Before running on your entire table:

1. Test with a single row.
2. Verify the configuration works.
3. Check the response data.
4. Then run on full table.

**Why:** Saves credits and catches errors early.

### Secure authentication

- Never hardcode API keys in requests.
- Use Clay's built-in authentication features.
- Store credentials securely.

### Configure rate limits

If the API documentation specifies limits, configure them in your enrichment.

**Example:** 100 requests per minute

```
Request limit: 100
Duration: 60000 ms
```

### Optimize with field paths

For large API responses, specify only needed fields:

```
data.users.email
data.users.name
```

**Benefits:** Faster processing, cleaner data, easier to work with.

### Use conditional runs

Set up conditional run formulas to only execute HTTP API when required data is present.

**This prevents:**

- Unnecessary API calls
- Error messages
- Wasted credits

### Document complex setups

For complex HTTP API configurations:

- Add notes about what each setting does.
- Document field mappings.
- Include example responses.

**Benefits:**

- Makes troubleshooting easier.
- Simplifies replication to other tables.

## Troubleshooting

### "Body parse error" (400 error)

This error indicates a formatting issue in your JSON body.

**Common fixes:**

**1. Add quotes around string variables**

```
Wrong: {"name": /Name Column}
Correct: {"name": "/Name Column"}
```

**2. Check punctuation**

```
Wrong: {"name": "John" "age": 30}
Correct: {"name": "John", "age": 30}
```

Ensure keys are separated by commas. Watch for extra spaces, colons, and brackets.

**3. Remove hidden characters**

- Copy your body into a plain text editor.
- Look for invisible characters from API docs.
- Clean and repaste into Clay.

**4. Verify correct API key**

Some providers have multiple API keys for different endpoints. Example: Apollo has separate keys for different APIs.

### Hidden characters in API documentation

When copying from API documentation:

1. Paste into a plain text editor first.
2. Check for hidden characters.
3. Remove any found.
4. Copy clean text into Clay.

This reveals any hidden characters that might cause parsing errors.

### Multiple API keys

Some data providers (like Apollo) have different API keys for different endpoints. Make sure you're using the correct API key for the specific endpoint you're calling.

### Using AI to diagnose issues

If you encounter errors, use Sculptor to help:

- Paste error messages for suggested fixes.
- Share API docs to verify configuration.
- Get help interpreting unexpected responses.

## FAQs

### Why do I need quotation marks around dynamic string variables?

As of October 2024, you must enclose dynamic string variables in quotation marks when using the HTTP API enrichment column. This ensures proper JSON formatting.

**Example:**

```
Correct: {"email": "/Email Column"}
Wrong: {"email": /Email Column}
```

### What if a data provider has multiple API keys?

Some data providers have multiple API keys for different APIs. For example, Apollo has several APIs you can create keys for. Make sure you're using the correct API key for the specific endpoint you're calling.

### How do I handle hidden characters in API documentation?

When copying from API documentation, paste your code into a plain text editor first. This reveals any hidden characters that might cause parsing errors. Remove them before pasting into Clay.

### When should I use HTTP API as source vs. enrichment?

- Use **enrichment** if you already have a list of records in Clay and want to add API data to them.
- Use **as source** if you need to pull a list from an external API to create a new table.

### Can I use HTTP API with pagination?

Currently, HTTP API as source does not support pagination. The import will retrieve only the data from a single API response. Pagination support may be added based on customer demand.
