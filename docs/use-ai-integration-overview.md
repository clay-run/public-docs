---
title: Use AI
source_url: https://university.clay.com/docs/use-ai-integration-overview
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

    **Note:** If you want to analyze website content using a Content creation column, first use the **Scrape Website** enrichment to pull the page text into a table column, then reference that column in your AI prompt. For more complex web research — visiting multiple pages, following links, or multi-step browsing — a **Claygent** agent column (accessible via **Add column → [AI section]**) is the most reliable option; it has web browsing built in and works with any AI model.
4.  Select a `Model` from the dropdown.
    1.  Click `Compare models` to get more detailed information about each model.
    2.  _(Optional)_ Set the **Temperature** to control how creative or consistent the model's output is. Options are **Very Low**, **Low**, **Medium** (default), **High**, and **Very High** — lower values produce more predictable, repeatable results; higher values produce more varied responses. The underlying numeric value varies by model. For tasks requiring consistency — such as structured data extraction, scoring, or categorization — start with **Low** or **Very Low**.
5.  Write a `Prompt`.
    -   For guidance on writing effective prompts, see our doc on [writing prompts](https://www.clay.com/university/guide/ai-metaprompter-guide).
    -   **Tip:** You can mix static text and column references in the same prompt. Use `{{Column Name}}` syntax only for values that differ from row to row — like a LinkedIn URL or job title that's unique per person. Criteria that stay the same for every row — like a specific industry, keyword, or criterion you're screening for — can be typed directly in the prompt. For example, to check whether each person has ever worked in consulting, write: *"Based on {{Profile URL}}, has this person ever worked in consulting? Return Yes or No."* No "consulting" column needed.
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
-   **Make the inputs optional.** Open the column settings (click the column name → **Edit column**), scroll to the prompt section, and toggle off the **Required to run** switch next to each column reference that should be optional. When a reference is optional, the cell will still run even if that column is blank — the empty field is simply omitted from the prompt for that row.

### Cells showing "Budget Credit Limit Reached"

For AI columns using variable-priced models (such as GPT-4.1, Claude Sonnet, or Gemini 2.5 Pro) with Clay's managed account, a **Clay Credit Budget** setting appears in the column configuration. This sets the maximum number of Clay credits that can be spent on a single row. If the estimated cost of running a row exceeds this limit, the cell shows **"Budget Credit Limit Reached"** and does not complete. Clicking the cell reveals the full message with the estimated cost and your current budget.

To fix this, open the column settings and increase the **Clay Credit Budget** value. Consider the length of your prompt and system prompt when choosing a limit, as longer prompts cost more credits per row.

**Note:** This setting only applies to expensive variable-priced models when using Clay's managed account. Users who connect their own API key are billed directly by the AI provider and this cap does not apply.

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
