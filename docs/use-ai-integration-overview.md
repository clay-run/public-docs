---
title: Use AI
description: Leverage AI to process, categorize, and conduct web research for
  actionable insights.
last_synced: 2026-04-26T01:40:51.610Z
---

# Use AI

Leverage AI to process, categorize, and conduct web research for actionable insights.

The **Use AI** feature in Clay allows users to automate tasks like content creation, data enrichment, and web research using GPT, Claude, Gemini, and other AI models.

Here are some key capabilities of the Use AI integration:

-   Drafting personalized messages using company and individual data
-   Extracting financial information from 10-K reports to track business metrics
-   Researching companies' current customer lists from their websites

Let's walk through how to connect and use the Use AI integration.

## Enriching data with Use AI

When you add Use AI to your table, you'll see two tabs: **Generate** and **Configure**.

-   **Generate tab**: Describe what you want in plain English, and Clay will automatically build the full column setup for you—including an enhanced prompt, recommended model, and output fields.
-   **Configure tab**: Review and adjust all technical settings, or manually configure your AI column from scratch if you prefer full control.

After generating a setup, you can easily edit your original description and regenerate to refine your AI column.

### Using the Generate tab (recommended)

1.  While in a Clay table, click `Add column` and click `Use AI`.
2.  In the `Generate` tab, describe what you want to accomplish in plain English.
    -   For example: "Find the CEO's email address" or "Summarize this company's product offering from their website."
3.  Click `Generate` and Clay will automatically:
    -   Create an optimized prompt
    -   Recommend the best AI model for your task
    -   Set up appropriate output fields
4.  Review the generated setup in the **Configure** tab.
5.  Make any adjustments if needed, then run your enrichment.

### Using the Configure tab (advanced)

1.  While in a Clay table, click `Add column` and click `Use AI`.
2.  Switch to the `Configure` tab.
3.  Select the `Use case`. Choose either web research or content creation.
    1.  **Web research:** Scrape and analyze websites. Provide a website URL in your prompt and Use AI will fetch the page content for the model to analyze.
    2.  **Content creation, manipulation:** Create and manipulate data in your table. **This mode does not access the web** — if your prompt references a website URL, the model will not visit it; it only processes data that is already in your table columns.

    **Note:** If you want to analyze website content using a Content creation column, first use the **Scrape Website** enrichment to pull the page text into a table column, then reference that column in your AI prompt. For more complex web research — visiting multiple pages, following links, or multi-step browsing — a **Claygent** agent column (accessible via **Add column → [AI section]**) is the most reliable option; it has web browsing built in and supports a range of models including Clay's parallel models, Claude, GPT, Gemini, Grok, Mistral, and others.
4.  Select a `Model` from the dropdown.
    1.  Click `Compare models` to get more detailed information about each model.
    2.  _(Optional)_ Set the **Temperature** to control how creative or consistent the model's output is. Options are **Very Low**, **Low**, **Medium** (default), **High**, and **Very High** — lower values produce more predictable, repeatable results; higher values produce more varied responses. The underlying numeric value varies by model. For tasks requiring consistency — such as structured data extraction, scoring, or categorization — start with **Low** or **Very Low**.
5.  Write a `Prompt`.
    -   For guidance on writing effective prompts, see our doc on [writing prompts](https://www.clay.com/university/guide/ai-metaprompter-guide).
    -   **Tip:** You can mix static text and column references in the same prompt. To reference a column, type `/` in the prompt editor and select the column from the menu — it will appear as `{{Column Name}}` in your prompt. **Do not type `{{Column Name}}` as literal text** — only references inserted via the `/` shortcut are substituted with actual row data when the column runs; text you type in `{{...}}` form is treated as a plain string and will not be filled in. Use column references for values that differ from row to row (like a website URL or LinkedIn profile unique to each contact). Criteria that stay the same for every row — like a specific industry, keyword, or criterion you're screening for — can be typed directly in the prompt. For example, to check whether each person has ever worked in consulting, write: *"Based on {{Profile URL}}, has this person ever worked in consulting? Return Yes or No."* No "consulting" column needed.
    -   **Tip — optional column references:** Every `{{Column Name}}` reference you add is **required to run** by default. If that column is blank for a row, the cell will show **"Some inputs missing"** and skip that row. To allow the column to run when a field is empty, hover over the `{{Column Name}}` token in the prompt — a **Required to run** toggle appears inline on that token. Switch it off for any input that doesn't always have data.
6.  _(Optional – Content creation, manipulation only)_ Provide context for task.
7.  Add and define outputs.
    -   **Fields**
        -   In the text field, enter the field names where you want the output to appear.
        -   Use the dropdown menu to select the appropriate data type for each output field.
    -   **JSON Schema**
        -   Paste or type a JSON Schema object to tell the AI exactly how to structure its response. The root must be `"type": "object"` with a `"properties"` map.
        -   **Every array field must include `"items"`.** A field with `"type": "array"` must also specify `"items"` to define what type of values the array contains. For example:
            ```json
            "keyIndicators": {
              "type": "array",
              "description": "Short phrases supporting ICP fit.",
              "items": { "type": "string" }
            }
            ```
        -   **JSON must be strictly valid — no trailing commas.** Standard JSON does not allow a comma after the last property in an object or array. A stray trailing comma (e.g., `"items": { "type": "string" },` when it is the last property in that object) will cause the error: `Your JSON Schema configuration is invalid. Please try using the "Generate from prompt" button in the column config to create a valid schema, or check your JSON Schema for formatting errors.`
        -   **Keywords such as `minimum`, `maximum`, `minLength`, `maxLength`, `pattern`, `minItems`, `maxItems`, and `uniqueItems` are not supported and will prevent the column from running.** Remove them from your schema if present. To document a constraint, add it to the field's `"description"` instead — for example, `"description": "Confidence score from 0 to 1"` rather than `"minimum": 0, "maximum": 1`.
        -   To skip writing schema by hand, click **Generate from prompt** to let Clay generate a valid schema from your prompt automatically.
8.  _(Optional – Content creation, manipulation only)_ Click `Examples` and `Add examples` to show AI what responses should look like.

**Tip — testing prompt changes on a sample:** To iterate on a prompt without running your entire table, select a few rows, right-click, and choose **Run [N] rows** (or select specific cells and choose **Run [N] cells**). This lets you validate results before spending credits on every row. Note that when an AI column produces new output, any downstream columns that reference it will automatically re-run — this is expected behavior. To prevent downstream columns from triggering while you refine a prompt, use [Sandbox mode](sandbox-mode.md), which isolates your changes to a test copy of the table. See [Run progress and row management](run-progress.md) for full details on running specific rows.

## Generating images with Use AI

1.  While in a Clay table, click `Add column` and click `Use AI`.
2.  Select the `Use case` → `Image generation`.
3.  Select a `Model` from the dropdown.
    -   Click `Compare models` to see detailed information about each model.
4.  Write a `Prompt`.
5.  Choose your preferred dimensions and optionally add a reference image URL.

### **Run settings**

-   **Auto-update**
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))

## Selecting specific AI models

Clay's Use AI feature supports multiple AI providers, including GPT (OpenAI), Claude (Anthropic), Gemini (Google), and DeepSeek.

**Note:** The models listed in this section are available in the **Use AI** action. Claygent supports a broad set of models — including Clay's parallel models (Argon, Neon, Helium), Claude, GPT, Gemini, xAI/Grok, Mistral, and others. **DeepSeek V4 Pro** is available in both Use AI and Claygent (currently in beta — contact support to enable); to use it, select **DeepSeek V4 Pro** from the model dropdown.

To learn more about each model's capabilities and prompting best practices, refer to their official documentation:

-   [Anthropic](https://docs.anthropic.com/en/docs/about-claude/models)
-   [OpenAI](https://platform.openai.com/docs/models)
-   [Google Gemini](https://ai.google.dev/gemini-api/docs/models/gemini)

### Connecting your own API keys

By default, Use AI uses the Clay-managed account, though you can select other accounts during setup.

While you don't need your own GPT, Claude, or Gemini API key to use the AI features, having one may reduce costs.

1.  Select the desired `Model` from the dropdown.
2.  Click on the `Account` dropdown and click `+ Add account`.

**Note:** Connecting your own OpenAI API key does not enable OpenAI's Batch API. Clay sends all AI column requests in real-time using the standard API — regardless of which account is connected. You will not get OpenAI's batch pricing (50% discount) or the extended processing window (up to 24 hours). If you need to process a large volume of data at batch pricing, the workaround is to export your data from Clay, run it through the OpenAI Batch API externally, then re-import the results.

## Using additional or custom LLMs

Use AI supports a fixed set of built-in AI providers (such as GPT, Claude, Gemini, and DeepSeek). Custom or additional LLMs — including open-source models like LLaMA, or models accessed through a proxy such as LiteLLM — cannot be added directly to the Use AI enrichment interface.

**Workaround: HTTP API enrichment**

To call a custom or additional LLM from Clay, use the [HTTP API enrichment](https://university.clay.com/docs/http-api-integration-overview) to send requests to any OpenAI-compatible endpoint:

-   **Hosted proxy services** (e.g., LiteLLM, Azure OpenAI, AWS Bedrock): Configure the HTTP API enrichment to call the provider's OpenAI-compatible endpoint. See [LiteLLM's API documentation](https://docs.litellm.ai/docs/providers/openai_compatible) for endpoint and authentication details.
-   **Self-hosted open-source models** (e.g., LLaMA): Host the model at a reachable HTTP endpoint, then configure the HTTP API enrichment to call it.

**Limitations compared to Use AI:**

-   You will not have access to Use AI's built-in features such as structured output configuration, model comparison, or web research (Claygent) mode.
-   Each table row generates one API call to your LLM endpoint.

## Troubleshooting

### Cells showing "Some inputs missing"

When a cell shows **"Some inputs missing"**, one or more column references in your prompt are marked as required but the underlying column is blank for that row. The cell will not run for affected rows.

There are two ways to resolve this:

-   **Fill in the missing data.** Ensure that the columns referenced in your prompt have values for the rows you want to run.
-   **Make the inputs optional.** In the column prompt, hover your cursor over a `{{Column Name}}` reference token — a **Required to run** toggle appears inline on that token. Switch it off for any input you want to be optional. When toggled off, the cell will still run even if that column is blank — the empty field is simply omitted from the prompt for that row.

### AI column running but producing unexpected output

If an AI column runs without errors but produces output that doesn't match what you expected — for example, a name-normalization column returning a value from the wrong source, or any column that seems to ignore the data you're looking at — the most likely cause is that the prompt's `{{Column Name}}` references point to a different column than you intended.

**The AI only receives data from the columns explicitly referenced in its prompt.** It does not automatically read all columns in a row — it sees only the values you inject via `{{Column Name}}` tokens. If a reference points to the wrong column, the AI processes that column's data and returns a result that is correct for *that* data, even though it's not what you expected.

**To verify which column the AI is reading:**

1.  Open the column settings (click the column name → **Edit column**).
2.  In the **Prompt** field, look at each `{{Column Name}}` token — these are the only columns the AI reads per row.
3.  Confirm each reference points to the column containing the data you want processed. For example, if your goal is to normalize raw names like "Eng. Sami" and strip the honorific, the reference must point to the column that contains the full raw name — not a separate column (such as "First Name") that may already hold a clean value.
4.  To fix a reference, delete the incorrect `{{Column Name}}` token and re-insert the correct column by typing `/` in the prompt and selecting it from the menu.
5.  Save the updated column and re-run the affected rows.

**Tip:** Adding concrete input/output examples in the **Examples** section (Configure tab → **Examples** → **Add examples**) helps the AI handle edge cases specific to your data — for instance, names with honorifics, middle initials, or unusual formatting not covered by your initial prompt.

### AI column output shows as a JSON object (response, reasoning, confidence, stepsTaken)

When a Use AI web research column or Claygent column runs, the result is stored as a structured JSON object. This object automatically includes these fields:

-   **`response`** — the main text answer; this is the value shown as the cell's text preview in the table.
-   **`reasoning`** — the model's step-by-step thinking notes.
-   **`confidence`** — Clay's built-in quality indicator (`low`, `medium`, `high`, or `very high`), which drives the color dot on each cell.
-   **`stepsTaken`** — descriptions of each research step the AI took (for example: `"Searched Google for: 'company headquarters'"` or `"Visited https://example.com to find: 'company revenue'"`).

If this JSON object appears in a downstream column, that column is referencing the full AI column object instead of a specific sub-field.

**To get just the `response` text into a cell:** In a formula column, use the `/` property picker and select `YourAIColumn > response`. You can also use dot notation directly: `{{YourAIColumn}}.response`.

**To write data into named fields (recommended):** Open the column settings (click the column header → **Edit column**), go to the **Configure** tab, and add named output fields in the **Outputs** section (for example: `City`, `Industry`, `Revenue`). Each named field becomes a separately extractable sub-field you can pull into other columns with the `/` picker.

### Claygent column `response` field contains explanation text instead of expected output

In a Claygent column that uses the **default output schema** (no custom output fields defined), the model is asked to populate two fields as part of the same structured output: `response` (the intended main answer) and `reasoning` (the model's thinking notes). Because both fields are produced by the model as structured outputs in the same response, the model can sometimes put verbose explanation prose in `response` and the actual structured answer you want — such as a comma-separated list or a single category value — in `reasoning`.

To fix this:

-   **Define named output fields (recommended).** Open the column settings, go to the **Configure** tab, and add explicit output fields in the **Outputs** section — for example, a `services` field of type `string`. When you define your own fields, the model targets those instead of the generic `response`/`reasoning` defaults, making output significantly more predictable. See the [Output schema section in the Claygent builder docs](claygent-builder.md) for details.
-   **Tighten your prompt.** Add an explicit instruction specifying the exact output format and that no explanation should be included — for example: *"Return ONLY a comma-separated list of applicable service categories. Do not include any justification or reasoning."*
-   **Lower the Temperature.** In the column settings, set **Temperature** to **Low** or **Very Low**. Lower values make output more consistent and help the model follow format instructions reliably.
-   **Add a downstream formula column as a safeguard.** For rows where the fields have already swapped, add a formula column that checks whether `response` looks like explanation text — for example, by detecting whether it reads as a full sentence — and falls back to the `reasoning` field when it does. This cleans up already-run data; the fixes above prevent the problem for future runs.

### Cells showing "Budget Credit Limit Reached"

For AI columns using variable-priced models (such as GPT-4.1, Claude Sonnet, or Gemini 2.5 Pro) with Clay's managed account, a **Clay Credit Budget** setting appears in the column configuration. This sets the maximum number of Clay credits that can be spent on a single row. If the estimated cost of running a row exceeds this limit, the cell shows **"Budget Credit Limit Reached"** and does not complete. Clicking the cell reveals the full message with the estimated cost and your current budget.

To fix this, open the column settings and increase the **Clay Credit Budget** value. Consider the length of your prompt and system prompt when choosing a limit, as longer prompts cost more credits per row.

**Note:** This setting only applies to expensive variable-priced models when using Clay's managed account. Users who connect their own API key are billed directly by the AI provider and this cap does not apply.

### Cells showing "API key is missing"

If your AI column cells show an **"API key is missing"** error, the column is configured to use a model that requires your own API key, but no key has been connected for that model.

There are two ways to resolve this:

-   **Switch to a Clay-managed account (recommended).** Open the column settings, find the **Account** dropdown, and select the default Clay-managed account. This uses Clay's shared credits and does not require your own API key.
-   **Connect your own API key.** If you prefer to use a specific provider (OpenAI, Anthropic, or Google Gemini), open the column settings, click the **Account** dropdown, click **+ Add account**, and follow the prompts to add your key.

**Note:** If you updated the model using Sculptor and the error persists, the change may not have saved correctly. Open the column settings directly (click the column name → **Edit column**) and confirm the **Model** and **Account** fields reflect what you expect, then re-save and re-run.

### OpenAI key shows "Success" but cells fail with "The API key is invalid"

If your OpenAI API key shows a green **Success** status in Clay's connection manager but Use AI columns fail at runtime with **"The API key is invalid. Please check your API key and try again."**, your key is likely configured with **OpenAI data residency** (for example, US data residency).

OpenAI's data residency keys require API calls to be routed to a regional hostname — for example, `us.api.openai.com` — rather than the standard `api.openai.com`. Clay's native OpenAI integration always routes to `api.openai.com`, so data residency keys are incompatible with the built-in Use AI integration. The connection validation probe behaves differently from a full completion request, which is why the key shows green in Clay's settings but fails when the column actually runs.

**Workarounds:**

1. **Use a standard (non-data-residency) OpenAI API key.** Create a new API key in your OpenAI dashboard without data residency enabled, and connect that key in Clay. Standard keys route to `api.openai.com` and work with Clay's native integration.

2. **Use HTTP API enrichment pointed at the regional endpoint.** If you must use a data-residency key, bypass the native OpenAI integration and call OpenAI's API directly using the [HTTP API enrichment](http-api-integration-overview.md):
   - Set the endpoint URL to `https://us.api.openai.com/v1/chat/completions` (replace `us` with your region if different).
   - Add an `Authorization` header with the value `Bearer <your-api-key>`.
   - Set the request body to a valid OpenAI chat completions payload (e.g., `{"model": "gpt-4o", "messages": [{"role": "user", "content": "{{YourColumn}}"}]}`).

   This routes to the correct regional hostname and works with data-residency keys, though you won't have access to Use AI's structured output configuration, model comparison, or web research features.

### AI column stops working after editing with Sculptor

If you used Sculptor to adjust an AI column and the column now shows an error or stops producing results, something in the prompt was likely broken during the Sculptor edit. Here's what to check:

-   **A `{{column}}` variable pointing to a deleted or renamed column.** If Sculptor reorganized your prompt, or you renamed a column after setting up the AI column, any variable referencing the old column name will fail. Affected rows will show **"Missing input"** and be skipped. Open the column settings directly (click the column name → **Edit column**), review each variable reference in the prompt, and confirm every `{{column}}` maps to an existing column in your table.
-   **A backtick or template literal accidentally added.** Sculptor can introduce backtick characters (`` ` ``) around values in prompts. This causes a formula parse error before the column runs. Check your prompt text for stray backticks and remove them.
-   **A malformed JSON output schema.** If your column uses a structured JSON output schema and Sculptor rewrote it, the schema may now be invalid — for example, an array field missing `items`, or a trailing comma. The column will show its own schema-specific error message. Click **Generate from prompt** in the column settings to regenerate a valid schema.

**Tip:** When troubleshooting, make changes directly in the column settings panel rather than through Sculptor. Test on a single row before running the full table.

### AI column returning fabricated email addresses

If an AI column was set up to "find" or "search for" email addresses and is returning results that look real but bounce — or include unexpected domains like `@linkedin.com`, `@gmail.com`, or an unrecognizable company domain — the column is generating (hallucinating) those addresses rather than retrieving real ones.

**AI columns in content creation mode generate output from the model's training data. They do not search the live web or query email-provider databases.** When asked to find an email address, the model produces a plausible-looking result that may not correspond to a real, deliverable address.

For reliable email finding, use a dedicated email finder instead:

-   The **[Work Email waterfall](https://university.clay.com/docs/work-email-waterfall)** queries multiple verified providers in sequence and stops as soon as one returns a valid match — this is the recommended approach for most use cases.
-   Individual providers such as Findymail, LeadMagic, Hunter, Dropcontact, and Datagma are also available as standalone enrichments under **Add enrichment**.

**Note:** The **web research** mode in Use AI can scrape specific website URLs you provide as inputs, but it is not designed for email discovery. For finding work email addresses, dedicated enrichment providers are the reliable choice.

### Cells showing "Cell data size exceeds limit" when using Scrape Website output

If your AI column shows a **"Cell data size exceeds limit"** error after referencing a **Body Text** column extracted from a Scrape Website enrichment, the problem is a mismatch between data size and cell type. When the Scrape Website enrichment runs, it stores its full output in the enrichment column itself (200 kB capacity). If you extract the Body Text into a separate standalone column, that extracted column is a basic text field with an 8 kB limit — and a typical webpage's body text far exceeds this.

**Fix: reference the Scrape Website enrichment column directly instead of the extracted Body Text column.**

1.  In your AI column prompt, type `/` to open the reference picker.
2.  Select **Scrape Website** (the enrichment column itself) and navigate into it to choose only the specific properties your prompt needs — such as the page title, meta description, or other targeted fields.
3.  Avoid selecting the full Body Text if the page is large; pick the targeted properties instead.

Pulling properties directly from the enrichment column gives you access to the full 200 kB capacity and lets you pass only the fields you need, keeping the input small.

**Alternatively**, configure the Scrape Website enrichment to return less data. Open the enrichment column settings and deselect output fields you don't need (for example, uncheck **Body Text** if your prompt only requires the title and description).

**Skipping rows where scraped data is missing:** If you want the AI column to skip rows where the Scrape Website column returned no data, add a run condition. Open the AI column's **Run Settings**, click **Add run condition**, and set it to `/Scrape Website is not empty`. See [Conditional runs](conditional-runs.md) for full details.

### Cells showing "Rate limit wait time exceeded" with your own OpenAI API key

If cells in a **Use AI** column show a **"Rate limit wait time exceeded"** error and you have your own OpenAI API key connected, the error means Clay has hit the token-per-minute (TPM) rate limits on your key. Clay automatically waits for the rate-limit window to reset before retrying, but if your key's TPM limits are persistently below what the operation requires, rows will remain stuck.

Clay reads rate-limit headers in OpenAI's responses to detect your key's available TPM. If the detected limit is below what the column needs to run at a sustainable pace, Clay pauses and retries — but the error persists until the limit clears or is increased.

**Resolution options:**

1. **Switch to Clay's managed OpenAI account (recommended for "Create or modify content" columns).** Open the column settings, click the **Account** dropdown, and select the default Clay-managed account. Clay's managed account handles rate limits automatically — no tier upgrade needed on your end.

2. **Upgrade your OpenAI API usage tier.** In your OpenAI account, increase your usage tier to raise your TPM limits. Clay requires at least **30,000 TPM** for "Create or modify content" Use AI columns. Claygent (web research) columns require substantially higher TPM — see [AI Tokens](ai-tokens.md) for the specific requirements by provider.

To check your current OpenAI rate limits and request a tier increase:
- [Usage](https://platform.openai.com/usage)
- [Limits](https://platform.openai.com/settings/organization/limits)
- [Usage Tiers](https://platform.openai.com/docs/guides/rate-limits#usage-tiers)

### Scrape Website returns empty results on login-required pages

If Clay's **Scrape Website** enrichment returns a login screen or empty results instead of the content you expected, the page is likely gated behind user authentication.

Clay's Scrape Website action includes JavaScript rendering (enabled by default) and can handle many dynamic websites. However, it fetches pages as an anonymous browser — it has no access to your account credentials or session cookies. When a page requires users to be signed in before the content loads (such as conference attendee lists on event platforms, paywalled databases, or private CRM dashboards), Clay receives only the login screen or a restricted preview rather than the protected data.

**Why this happens:** Even with JavaScript rendering on, Clay cannot authenticate as you. Sites that gate content behind a login — where the list, report, or dataset only appears after you sign in — are not accessible to any external scraper, regardless of JavaScript settings.

**Workarounds:**

-   **Export directly from the platform.** Most event management platforms, databases, and portals offer a built-in data export for logged-in users. Look for a "Download attendee list," "Export," or "Download CSV" option inside the platform once you're signed in.
-   **Import the exported file into Clay.** Once you have the data as a CSV, upload it to a Clay table via **Tools → Import** and select your file. See [How to import your CSV into Clay](csv-import-overview.md) for step-by-step instructions, then add enrichment columns to fill in missing details like email addresses, social profiles, and full names.
-   **Capture the underlying API request (advanced).** If the platform doesn't offer a built-in export, open your browser's DevTools **Network** tab while signed in, navigate to the page, and find the underlying API call that loads the data. You can replay that authenticated request — which carries your login cookies or token — to extract the raw data manually.

### Scraping data spread across multiple pages

Clay's Scrape Website action runs on one URL at a time. If the content you need is spread across many pages — for example, a directory paginated across 20 or 30 pages — you can scrape all pages in Clay by treating each page URL as its own row:

1.  Create a column in your table that holds each page URL. You can add each page URL as a row manually, or use a formula column that appends a page number to the base URL (for example, `"https://example.com/directory?page=1"`, `"https://example.com/directory?page=2"`, and so on).
2.  Add a Scrape Website enrichment column that references that URL column.
3.  The enrichment will run against every row, scraping each page in parallel.

This approach works well when each page URL loads its content directly and does not require a login. For pages behind authentication walls, see [Scrape Website returns empty results on login-required pages](#scrape-website-returns-empty-results-on-login-required-pages) above.