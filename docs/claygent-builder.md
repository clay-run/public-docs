---
title: Claygent builder
source_url: https://university.clay.com/docs/claygent-builder
description: Build smarter agents faster
last_synced: 2026-05-11T17:47:40.000Z
---

# Claygent builder

Build smarter agents faster

Claygent builder is the centralized hub for building, testing, and deploying Claygents — Clay's AI agents designed for judgment-based GTM work like account research, lead scoring, outbound copywriting, and persona classification.

With Claygent builder, you can build agents conversationally using Sculptor, test for free on your production data, add business context and documents directly to your prompts, and deploy agents across all your workflows from one place.

For example, you could create:

-   **Lead scoring agent**: Evaluates prospects against your ICP and outputs a score (1-100) with rationale.
-   **Outbound email agent**: Writes personalized cold emails using your ICP definition, tone guidelines, and enriched data.
-   **Account research agent**: Summarizes what a company is doing right now, surfaces recent news, funding events, and hiring signals.
-   **Persona classification agent**: Categorizes contacts by tier, buying role, or persona type.

## Getting to Claygent builder

Click `Agents` in the left-hand navigation bar.

Three ways to start building:

-   **From scratch** — blank canvas with full text editor and Sculptor available on the side.
-   **With Sculptor** — describe what you want in plain language and Sculptor drafts the full agent for you (fastest path).
-   **From a template** — pre-built starting points for prospecting, account scoring, contact scoring, and copywriting.

### Creating a Claygent from an existing table

If you've already built a Claygent prompt in a table that works well, you can save it as a reusable agent:

1.  Click on your `Use AI` column name.
2.  Select `Edit column`.
3.  Click `Create Claygent` in the top right.
4.  Your prompt, variables, and test cases transfer to Claygent Builder.
5.  Now you can deploy it across other tables.

This is useful when you've refined a prompt in one table and want to reuse it elsewhere without starting from scratch.

## Building an agent with Sculptor

Sculptor is Clay's conversational agent builder. Describe what you want your agent to do in natural language, and Sculptor generates the prompt, variables, output format, and test cases.

**Example prompt for Sculptor:**

_"Build an agent that scores a lead against our ICP and outputs a score from 1 to 100 with a short rationale explaining the score."_

Sculptor will:

1.  Define the prompt logic.
2.  Set up variables (company name, contact title, industry, etc.).
3.  Format the output (score plus reasoning).
4.  Create test cases so you can see it in action.

### Iterating with Sculptor

You can refine your agent by telling Sculptor what to adjust:

_"Adjust the scoring so company fit is weighted at 60% and persona fit at 40%. Also break out company size as its own factor."_

Sculptor rewrites the prompt and shows a "Prompt updated by Sculptor" confirmation. This saves the new prompt text — it does **not** re-run the test automatically. Click **Run** in the test panel to see how the updated prompt performs. Every change is saved automatically in version history.

## Configuring your agent

### Business context

Your company description, ICP, and buyer personas auto-populate from workspace settings. Your Claygent pulls from this automatically to write on-brand output.

If you haven't filled yours in yet, go to `Settings`, enter your domain, and Clay will research for you.

### Document uploads

Attach tone guides, messaging docs, PDFs, or CSVs directly into your agent. For copywriting agents, this ensures the Claygent writes in your voice, not a generic AI voice.

### Web search

Enable web search when your agent needs live research (recent company news, hiring signals, etc.). Disable it when working from data already in your table to keep runs faster and more consistent.

**Note:** For Clay parallel models (Argon, Neon, Helium, and similar), web search is a required component — the toggle appears greyed out because it is always active and cannot be turned off for these models. This is expected behavior, not a missing feature.

### Find contacts and jobs tool

Give your Claygent access to find people and jobs data directly. This enables prospecting workflows like "find the best person who would manage growth at a company" — where the right title varies by company size.

### Custom MCP server

Connect any external MCP (Model Context Protocol) server to your Claygent as a tool. This lets your agent interact with services like Salesforce, HubSpot, Gmail, or Google Calendar, and gives you access to thousands of connectors through catalogs like [Smithery](https://smithery.ai/) and [Pipedream](https://mcp.pipedream.com/).

**Note:** Custom MCP server connections are available on Enterprise plans. Self-serve customers can request access by contacting support to join the beta.

**Model requirement:** Custom MCP tools require a non-Clay model with your own private API key — Clay's shared parallel models (Neon, Argon, Helium, and similar) do not support tool calling and will show "Tools are not available for the selected model." To use custom MCP, select a Claude Sonnet/Opus 4 series or GPT-5 series model in the model picker and connect your own Anthropic, OpenAI, or Gemini API key via the account dropdown.

To add a custom MCP server from Claygent builder:

1.  Open your Claygent and go to the **Configuration** panel.
2.  Scroll to the **Tools** section and click **Add custom MCP server**.
3.  Give the connection a name.
4.  Enter the MCP server URL.
5.  Enter an API key if the server requires one (open endpoints don't need a key).
6.  Click **Save**.

You can also add MCP server connections workspace-wide from `Settings` → `Connections` → `+ Add connection` → `Custom MCP Server`. Connections added there appear automatically in your Claygent's MCP connections list.

**Tips for using custom MCP servers:**

-   **Be specific in your prompt.** Tell the Claygent exactly which service to access and what to do — for example, _"Use the Salesforce tool to add \{Company Name\} as a lead in my workspace."_
-   **Limit to 2–3 servers per run.** Enabling too many MCP servers at once can confuse the agent and produce inconsistent results.
-   **Chain servers for multi-step workflows.** For example: add a lead in Salesforce, research their background online, then draft a summary doc in Notion.
-   **OAuth is not currently supported.** Use API key authentication or open (unauthenticated) endpoints.

### Model selection

Swap between different AI models in the configuration panel to test output quality without touching your prompt.

Clay's parallel models differ in power and cost:

-   **clay-argon** — Strongest model for deep research and complex multi-step analysis.
-   **clay-neon** — Good balance of capability and speed for moderately complex tasks.
-   **clay-helium** — Fastest and most cost-effective among Clay parallel models.

**For classification and categorization tasks** (assigning a contact or record to a fixed list of labels using data already in your table), lighter models such as **clay-helium**, **GPT-4o mini**, or **Claude Haiku** work better than Argon. Argon is designed for deep research and complex reasoning — on a simple "pick one label from this list" task, it tends to return multi-sentence explanations and reasoning traces rather than a clean single-value response. Lighter models follow concise output instructions more reliably and cost less per run.

To get a clean single-value response (for example, "Sales" rather than "This contact is best categorized as Sales because their title indicates..."):

1.  Switch the model to **clay-helium**, **GPT-4o mini**, or **Claude Haiku**.
2.  Define a JSON output schema (see **Output schema** below) with a single `string` field for the category name.
3.  Add one or two examples in your prompt showing the expected output format — for example: _"Example output: Sales"_. The **Sculptor** tool can generate these automatically.

**Note:** Switching to a non-parallel model (GPT-4o mini, Claude Haiku, etc.) also disables mandatory web search, which keeps runs faster and more consistent when classifying from data already in your table.

### Output schema

When you need a Claygent to return structured data — multiple typed fields instead of free text — define a **JSON Schema** in **Define column outputs** in the column settings.

Common errors when writing schema by hand:

-   **Missing `items` on an array field.** Every field with `"type": "array"` must include an `"items"` object that specifies the element type. Without it, the AI provider rejects the schema and you will see: `Invalid schema for function 'returnData': In context=('properties', 'fieldName'), array schema missing items`. Fix it by adding `"items"`:

    ```json
    "keyIndicators": {
      "type": "array",
      "description": "Short phrases supporting ICP fit.",
      "items": { "type": "string" }
    }
    ```

-   **Trailing comma in the JSON.** Standard JSON does not allow a comma after the last property in an object or array. A stray trailing comma — for example `"items": { "type": "string" },` when `items` is the last property — causes a parse error displayed as: `Your JSON Schema configuration is invalid. Please try using the "Generate from prompt" button in the column config to create a valid schema, or check your JSON Schema for formatting errors.` Note: if you see the "array schema missing items" error but `items` is already present, a trailing comma elsewhere in that object is the likely cause — the in-app AI debugger may point to the wrong issue.

-   **Numeric enum with integer type (Grok models).** Grok models have stricter structured output requirements than other providers. Combining `"type": "integer"` with a numeric `"enum"` array — for example `"enum": [1000, 500, 100]` — causes a `Bad Request` (400) error that surfaces as `Error: Bad Request` on every row. Other providers (Claude, GPT-4o, Gemini) accept this combination without error. Two fixes:
    -   **Remove the enum**: delete the `"enum"` array and keep only `"type": "integer"`, letting the model return any integer.
    -   **Switch to strings**: change `"type"` to `"string"` and quote the enum values (`"1000"`, `"500"`, `"100"`).

To avoid writing schema by hand, click **Generate from prompt** to have Clay auto-generate a valid schema from your prompt.

## Testing before you deploy

**Note:** You can have up to 10 test cases at a time for free (you can delete and add new test cases to keep testing). Test runs don't cost credits.

Run test cases to see your Claygent stream its reasoning live. You can:

-   Import test data from existing table rows.
-   Generate test inputs with AI.
-   Save test cases as a reusable suite.
-   Compare outputs across different versions.

### Testing different models

Compare outputs across different AI models without changing your prompt. Switch models in the configuration panel and run tests side-by-side to find the best performance for your use case.

This is especially useful when you want to balance output quality against cost and speed.

## Deploying your agent

Once you're happy with the output:

1.  Go to any table and add an AI column.
2.  Under Claygent options, select `Saved Claygents`.
3.  Select the agent you just built.
4.  Variables automatically map to your table columns.
5.  Save and run.

You can also deploy directly from Claygent builder by clicking `Add to table`.

## Centralized management

From the Claygent builder home, you can see every table where each agent is running.

When your ICP changes or you need to adjust agent logic:

1.  Update the agent once in Claygent builder.
2.  Changes propagate everywhere it's deployed.
3.  No need to find and update each column individually.

This is the difference between managing duplicate prompts across multiple tables versus having a single source of truth.

## Version history

Every change you make is saved automatically. You can:

-   View all previous versions.
-   See what changed between versions.
-   Roll back to any previous version.

Access version history from the Claygent builder editor.

## FAQs

### What kinds of work are Claygents best for?

Claygents handle judgment-based, nondeterministic work in your GTM stack — work that requires reasoning, not just lookups. Main use cases:

-   **Account and lead research** — summarize what a company is doing, recent news, hiring signals.
-   **Lead scoring and contact scoring** — evaluate prospects against your ICP with weighted factors.
-   **Account scoring** — same idea at the company level.
-   **Outbound copywriting** — write personalized emails using your ICP and enriched data.
-   **Persona classification** — categorize contacts by tier, role, or buying persona.

### Who can create or edit agents?

Agent access follows your workspace permissions. Editors can create and modify agents, while viewers can reference approved agents in tables.

### Does testing cost credits?

No. You can have up to 10 test cases per Claygent at a time for free. You can delete and add new test inputs to keep testing. Once you deploy and run your agent in a table, standard runs follow your normal billing.

### How much does it cost to run a Claygent in production?

Credit cost depends on the AI model you select. Claygent defaults to **Argon** for web research — Clay's model for open-ended web lookups — which costs **3 credits per row**. Switching to **Helium** (1 credit per row) is a cost-effective alternative for simpler web research tasks. For a full model pricing reference, see [How AI is priced](ai-pricing.md).

If your goal is to find people associated with companies at scale — rather than open-ended web research — **Find People** is significantly more cost-effective: the **Find Contacts at Company** action costs 0.5 credits per row on current plans, versus 3 credits per row for Argon-based Claygent. Use Claygent when you need judgment-based research (summarizing company news, scoring leads, writing personalized outreach). Use Find People when you need structured contact lookups at scale.

### Can I test different models without changing my prompt?

Yes. Switch models in the configuration panel and rerun tests to compare output quality across different AI models.

### What happens if I update an agent while it's running in a table?

In-flight runs finish on the version that started them. New runs pick up the latest version automatically.

### Can I still edit prompts directly in tables?

Yes, but centralizing in Claygent builder gives you version control, free testing, and the ability to update once and deploy everywhere. It's the better choice for agents you'll reuse or iterate on.

### Sculptor updated my prompt but the output looks the same — what happened?

When Sculptor rewrites your prompt, it saves the new prompt text and shows a "Prompt updated by Sculptor" confirmation. It does **not** automatically re-run the test. The test output you see is from the previous run. Click **Run** (or **Run all**) in the test panel to execute the test with the updated prompt and see the new output.

### The web search toggle is greyed out — why?

For Clay parallel models (Argon, Neon, Helium, and similar), web search is always on and cannot be toggled off — it's a required part of how these models work. The greyed-out toggle is expected; web search is active. If you want to turn web search off, switch to a non-parallel model in the model selector.

### Can I connect a custom MCP server to a standalone Claygent (created outside a table)?

Yes. Custom MCP servers work in both standalone Claygents (built in Claygent builder) and in table-embedded AI columns. In Claygent builder, open your agent's **Configuration** panel, scroll to the **Tools** section, and click **Add custom MCP server**. You'll be prompted to name the connection, provide the server URL, and optionally add an API key for authenticated endpoints.

This feature is available on Enterprise plans; self-serve customers can contact support to request beta access.

### Why does my Claygent show "Tools are not available for the selected model"?

This message appears when you have a Clay parallel model (Neon, Argon, Helium, or similar) selected. These models don't support tool calling — including custom MCP servers, the "Find contacts and jobs" tool, and other tool-based features.

To use tools with your Claygent:

1.  Open the **Configuration** panel and click the model picker.
2.  Select a Claude Sonnet/Opus 4 series or GPT-5 series model.
3.  Click the **Account** dropdown and connect your own Anthropic, OpenAI, or Gemini API key.

Once you're on a supported model with a private API key, the tools in the **Tools** section will become active.

### My Claygent columns are showing an error — what does that mean?

If your Claygent columns are failing with an error like **"This action is no longer operational as a data provider. Please use another action."**, it means those columns are using an older version of the Claygent action that is no longer supported. The column settings panel may still appear editable, but the column cannot run.

You need to replace each affected column with a new **Use AI** column. Here's how:

1.  Open the old Claygent column and copy your prompt and any JSON output schema.
2.  Click **Add column** in your table and select **Use AI**.
3.  Paste your prompt into the new column.
4.  If you had a JSON output schema, paste it into the **JSON Schema** field under outputs.
5.  Save and rerun the column.

Repeat for each affected column in your table. Once the new Use AI column is running correctly, you can delete the old Claygent column.

### My object inputs show "Success" in the test panel instead of their actual content — is that normal?

Yes, this is expected. When a Claygent variable is connected to an object value — such as a JSON enrichment payload or a structured data column — the test panel input preview shows **"✅ Success"** rather than rendering the full object contents. This is a known display limitation; your agent receives and processes the complete object data correctly.

To inspect exactly what data was passed to your agent, deploy your Claygent to a table, run it, then click the cell to open the **cell details panel** and examine the full input and output values there.

### Can Claygent detect tracking pixels or marketing technologies on a website?

Yes, with an important limitation. Claygent fetches page content using third-party scraping services and analyzes the HTML and text — it does not trace JavaScript execution events, intercept network requests, or follow `<script src>` links the way a browser developer tool would. When prompting Claygent to look for tracking pixels or marketing technologies, write the prompt to analyze page content (for example: *"Look at this company's website and check whether the page HTML contains tracking pixel tags such as the Facebook Pixel or Google Tag Manager"*) rather than instructions that assume DevTools-style network monitoring.

**JavaScript-rendered pixels**: Claygent has a JavaScript rendering fallback, but it only activates when a page returns essentially empty static HTML. Most marketing websites return non-empty HTML even when some content is JavaScript-loaded — meaning the JS rendering path typically does not trigger. Pixel tags that are injected dynamically by JavaScript after page load (common for Facebook Pixel, Google Tag Manager, TikTok Pixel, etc.) are likely to be missed on typical marketing sites. There is no single-step solution in Clay for detecting JS-rendered pixels.

**Alternative**: The **BuiltWith** integration (**Find Technology Stack** action) can confirm whether a particular technology is present on a site, but it does not return specific pixel IDs or tracking codes.

## Tips for success

**Importing test cases**: Instead of manually creating test data, import real rows from your tables. Click `Import from table` in the test panel to pull actual data and see how your agent performs on real-world inputs.

**Variable mapping**: When deploying a Claygent to a new table with different column names, Builder will auto-suggest mappings. Review these carefully to ensure the correct data flows through.

**Start simple**: Build your agent with a basic prompt first, test it, then layer in complexity. It's easier to debug and refine when you're working incrementally.
