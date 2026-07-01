---
title: Claygent builder
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

**Note:** The Use AI column editor also has a **Templates** dropdown with a **Save as template** option. This is different from **Create Claygent** — "Save as template" stores the column's current configuration as a reusable column template that appears in the "Templates for Use AI" browser (open via Templates → **Browse templates**, then filter to **Created by: You**). Column templates are not standalone Claygents and will not appear in the Claygents section of the sidebar. Use **Create Claygent** when you want an agent you can deploy and manage across multiple tables.

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

Sculptor rewrites the prompt and shows a "Prompt updated by Sculptor" confirmation. This saves the new prompt text — it does **not** re-run the test automatically. Click **Run** in the test panel to see how the updated prompt performs. Click **Save** to persist your changes to version history.

### Resuming previous conversations

Sculptor saves conversation history for each Claygent. Click the **chat history** button (clock icon) in the Sculptor panel to browse and resume previous conversations for the Claygent you are currently viewing.

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

-   **`object` field with `additionalProperties: false` but no `properties` defined — sub-fields always come back empty.** An `object` field that sets `"additionalProperties": false` without a `"properties"` map is syntactically valid JSON Schema, but it tells the AI provider that no sub-fields are permitted. The model always returns `{}` for that field — the column runs and completes with no error message, but none of the structured data you expected appears. Fix: add a `"properties"` map listing every sub-field you want the AI to populate:

    ```json
    "engagementSummary": {
      "type": "object",
      "description": "Summary of engagement metrics.",
      "properties": {
        "totalPosts": { "type": "number" },
        "avgLikes": { "type": "number" }
      }
    }
    ```

-   **Field named `confidence` overrides Clay's built-in confidence indicator.** Clay automatically adds a `confidence` field to your output schema with enum values `low`, `medium`, `high`, and `very high` — but only when your schema does not already define one. This field drives the red/yellow/green color indicator on each response cell. If you define your own field named `confidence` (for example, as a numeric score), Clay skips injecting its own, and your custom field's values are used for the color indicator instead. Numeric values are mapped through thresholds to the text enum — for example, `0.98` maps to `very high` — which may not match the color you intend for your own scoring scale. To fix it, rename your custom field — for example, to `confidence_score` — and rerun the column. Clay will then inject its own `confidence` field and the color indicator will work as designed.

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

Edits to a Claygent are not auto-saved — click the **Save** button in the editor to persist your changes as a new version. The Save button is disabled when there are no unsaved changes. To access version history:

1.  Open the Claygent in Claygent builder.
2.  Click the **version badge** (e.g., **v3**) next to the Claygent's name at the top of the editor.
3.  The version history panel opens, listing all versions from newest to oldest.

To inspect any version, click its row to expand it — you can review the prompt, model settings, inputs, output format, and tools for that version. There is no automated side-by-side diff; compare versions by expanding them individually.

To restore a previous version, click the **revert** icon next to any non-current version. That version immediately becomes the current one.

## FAQs

### What kinds of work are Claygents best for?

Claygents handle judgment-based, nondeterministic work in your GTM stack — work that requires reasoning, not just lookups. Main use cases:

-   **Account and lead research** — summarize what a company is doing, recent news, hiring signals.
-   **Lead scoring and contact scoring** — evaluate prospects against your ICP with weighted factors.
-   **Account scoring** — same idea at the company level.
-   **Outbound copywriting** — write personalized emails using your ICP and enriched data.
-   **Persona classification** — categorize contacts by tier, role, or buying persona.

### How do I find contact information for people who don't have professional networking profiles?

Use Claygent with web search enabled to pull publicly available contact details directly from a company's website. Many organizations — especially smaller businesses — list staff contacts on a `/contact` page or in a site directory. Point Claygent at those URLs and instruct it to extract names, titles, email addresses, or phone numbers it finds there.

To get started, enable **Web search** in your Claygent's **Configuration** panel so the agent can browse live URLs. Then write a prompt that tells the agent which company URL to visit and what contact fields to return. For guidance on structuring an effective prompt for contact extraction, see [Writing AI prompts in Clay](ai-metaprompter-guide.md).

### Who can create or edit agents?

Agent access follows your workspace permissions. Editors can create and modify agents, while viewers can reference approved agents in tables.

### Does testing cost credits?

No. You can have up to 10 test cases per Claygent at a time for free. You can delete and add new test inputs to keep testing. Once you deploy and run your agent in a table, standard runs follow your normal billing.

### How much does it cost to run a Claygent in production?

Credit cost depends on the AI model you select. Claygent defaults to **Argon** for web research — Clay's model for open-ended web lookups — which costs **3 credits per row**. Switching to **Helium** (1 credit per row) is a cost-effective alternative for simpler web research tasks. For a full model pricing reference, see [How AI is priced](ai-pricing.md).

If your goal is to find people associated with companies at scale — rather than open-ended web research — **Find People** is significantly more cost-effective: the **Find Contacts at Company** action costs 0.5 credits per row on current pricing plans (1 credit per row on legacy plans), versus 3 credits per row for Argon-based Claygent. Use Claygent when you need judgment-based research (summarizing company news, scoring leads, writing personalized outreach). Use Find People when you need structured contact lookups at scale.

When selecting a third-party model (Claude, GPT-4o, Gemini, etc.) in Claygent, the **Account** dropdown in your column settings or workflow node configuration controls how billing works. Selecting the default **Clay-managed account** means Clay's API key handles the request, and the run deducts **Data Credits** at the variable rate for that model — the `~` prefix on the cost estimate shown in the column sidebar (for example, `~4.8`) indicates a variable charge that is reconciled after each row completes. To avoid spending Data Credits on AI, click **Account** → **+ Add account** to connect your own Anthropic, OpenAI, or Gemini API key; with your own key, each Claygent row counts as **1 Action** but no Data Credits are charged. For a full model-by-model credit reference, see [How AI is priced](ai-pricing.md).

**Note:** The **Account** dropdown and the option to use your own API key are available in both **table columns** and **Workflow Claygent nodes**.

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

### How do I mark a Claygent input as optional?

Each input in the Claygent builder shows **(required)** or **(optional)** next to its name. To change whether an input is required:

1.  Open your Claygent in Claygent builder.
2.  In the **Inputs** section, click the pencil icon next to the input you want to edit.
3.  Toggle **Required input** off to make it optional — the Claygent still runs when that input is empty, and the blank value is omitted from the prompt for that row.
4.  Click **Save**.

Toggle **Required input** back on if you want the Claygent to skip rows where that input is blank. New inputs you add via **Add input** default to optional.

**Note:** The **Inputs** section with the **Required input** toggle is available in workspaces where Claygent builder is enabled. If you don't see it, contact support to request access.

### Why is my Claygent column showing "Some inputs missing"?

When a Claygent cell shows **"Some inputs missing"**, one or more inputs in the **#INPUTS#** section of your column are marked as required but the referenced column is blank for that row. The cell will not run for affected rows.

There are two ways to resolve this:

-   **Fill in the missing data.** Ensure the referenced column has a value for every row you want to run.
-   **Make the input optional.** Click the column name → **Edit column**, scroll to the **#INPUTS#** section, and toggle off the **Required to run** switch next to each input that doesn't always have data. When an input is optional, the cell will still run for rows where that field is blank — the empty value is simply omitted from the prompt for that row.

### How do I get individual Claygent result fields into their own table columns?

After your Claygent column has run, you can extract any field from its results into a dedicated table column directly from the cell details panel:

1.  Click any cell in the Claygent column that has results to open the **cell details** panel on the right.
2.  Each field the agent returned — such as Email, URL, Phone, City, or any field from your output schema — appears listed with its value for that row.
3.  Next to the field you want, click **Add [field name] as new column** → **Create column**. Clay creates a new table column populated with that field's value across all rows.
4.  To route the field's values into a column you've already created, click **Map to an existing column** and select it from the list.

Repeat for each field you want to extract into its own column.

**Tip:** If you know which fields you need before running, define them as named output fields in the column settings (click the column name → **Edit column** → **Outputs** section). Named fields appear in the cell details panel and can also be referenced by downstream formula columns using the `/` property picker.

### How do I chain Claygents when the first one sometimes returns empty values for certain output fields?

When chaining Claygent A → Claygent B, whether B runs for a given row is controlled by B's input variable settings — not by how A's output schema defines its fields.

**Two distinct "required" settings to know:**

-   **Required in A's output schema** — tells the AI model which fields to try to return. If a field is listed as required in the schema but the model finds no data, A still completes and that field comes back empty. This setting does not affect whether B runs.
-   **Required to run in B's Variable Config** — the **Required to run** toggle on each input variable in B's **#INPUTS#** section. When enabled (the default), a blank value for that input causes B to show **"Some inputs missing"** and skip that row.

**Recommended pattern for chaining:** If you want B to run whenever A ran — even when some of A's specific output fields are empty — use a run condition on B instead:

1.  Open B's column settings → **Run Settings** → **Add run condition** (or **Only run if**).
2.  Set the condition to: `/[Claygent A column] has a value`

This gates B on whether A returned any result for that row, regardless of which sub-fields were populated. You can also combine conditions with OR logic — for example, `/scale_signals has a value OR /other_field has a value` — for more flexibility.

**To gate strictly on a specific field:** Leave that input variable's **Required to run** toggle on in B. B will only run for rows where that specific field from A has a value.

### My Claygent columns are showing an error or returning blank results — what does that mean?

If your Claygent columns are failing with an error like **"This action is no longer operational as a data provider. Please use another action."** — or are running and consuming credits but returning blank, empty cells — it means those columns are using an older version of the Claygent action that is no longer supported. The column settings panel may still appear editable, but the column cannot produce results.

You need to recreate each affected column using the current Claygent action. Here's how:

1.  Open the old Claygent column and copy your prompt and any JSON output schema.
2.  Click **Add column** in your table and select **Claygent** from the AI section.
3.  Paste your prompt into the new column.
4.  If you had a JSON output schema, paste it into the **JSON Schema** field under outputs. **Tip:** Keep the same output field names as the original column to minimize changes needed in any downstream formula columns that reference those fields.
5.  Save and rerun the column.

Repeat for each affected column in your table. After recreating, update any downstream formula columns that reference the old column's outputs to point to the new column instead. Once everything is running correctly, delete the old Claygent column.

**Note:** This error is distinct from the model deprecation warning. If you see an orange **"Deprecated"** badge next to a model name in your column settings, that is a separate indicator — it does not stop the column from running immediately. In that case, simply open the column settings, click the **Model** dropdown, and select a currently supported model to clear the warning.

### My Claygent column shows "Failed to parse formula for 'prompt'" or "Unable to parse the output schema for the column" — what do these mean?

These are two distinct configuration errors that can appear on a Claygent column:

-   **"Failed to parse formula for 'prompt' with error: {offset:XX}"** — The prompt field contains an invalid formula. Clay stores prompt text as a formula so that `{{column}}` references work, and if the formula has a syntax error at the character position shown by `offset`, the column cannot run. Common causes: a stray backtick (`` ` ``), an unmatched brace or quote, or characters introduced when copying text from a source that encodes content as HTML — for example, pasting from a chat window or email client that converts `<`, `>`, and `&` into HTML entities (`&lt;`, `&gt;`, `&amp;`).

-   **"Unable to parse the output schema for the column"** — The JSON output schema cannot be parsed. Common causes: HTML entities in the schema (`&lt;` instead of `<`, `&amp;` instead of `&`, etc.), a trailing comma after the last property in a JSON object or array, a flat description map (`{"fieldName": "description text"}`) used instead of a proper JSON Schema (the schema must have `"type": "object"` at the root and a `"properties"` map — never use a plain `{"key": "value description"}` format), a root-level `"type": "array"` (the root schema must always be `"type": "object"`), enum values written as a pipe-separated string (`"enum": "Yes | No | Unknown"`) instead of a JSON array (`"enum": ["Yes", "No", "Unknown"]`), or other invalid JSON syntax.

**To fix the prompt formula error:** Open the column settings (**click the column name → Edit column**) and inspect the Prompt field. Remove any stray backticks, unmatched braces or quotes, or HTML entities. If you copied the prompt from a chat tool or email, paste it into a plain-text editor first to strip hidden formatting before pasting into Clay.

**To fix the output schema error:** Open the column settings, go to the **Define column outputs** section, and inspect the JSON schema. Replace any HTML entities with their plain equivalents (`&lt;` → `<`, `&gt;` → `>`, `&amp;` → `&`), and remove any trailing commas. If you used a flat description map, rewrite it as a proper JSON Schema — each field needs at least `"type": "string"` (or another JSON Schema type), and any field constrained to a fixed set of values uses `"enum"` as an array of strings. If you wrote `"enum"` as a pipe-separated string, convert it to a JSON array. Alternatively, click **Generate from prompt** to have Clay regenerate a valid schema automatically.

**If the column remains broken after these fixes:** Copy your corrected prompt and schema, then recreate the column from scratch — a column with persistent settings errors cannot always be repaired in place. See the FAQ entry above, **My Claygent columns are showing an error or returning blank results**, for step-by-step instructions on recreating a column.

### My object inputs show "Success" in the test panel instead of their actual content — is that normal?

Yes, this is expected. When a Claygent variable is connected to an object value — such as a JSON enrichment payload or a structured data column — the test panel input preview shows **"✅ Success"** rather than rendering the full object contents. This is a known display limitation; your agent receives and processes the complete object data correctly.

To inspect exactly what data was passed to your agent, deploy your Claygent to a table, run it, then click the cell to open the **cell details panel** and examine the full input and output values there.

### Why are my Claygent cells showing the wrong confidence color even though my confidence value is high?

Clay uses a built-in `confidence` field — with text values `low`, `medium`, `high`, and `very high` — to drive the red/yellow/green color indicator on each response cell. Clay automatically adds this field to your output schema, but only when your schema does not already define a field named `confidence`.

If your JSON output schema includes a field named `confidence` with numeric values (for example, a score like `0.98`), Clay's normalizer maps those numbers to the text enum through thresholds — so `0.98` is mapped to `very high`, not to whatever color your own scoring scale intends. This can produce indicator colors that don't match your expectations.

To fix this, rename your custom field in the JSON schema to something like `confidence_score`. Then rerun the column. Clay will inject its own `confidence` field, and the color indicator will use the correct text-enum values.

### Can Claygent detect tracking pixels or marketing technologies on a website?

Yes, with an important limitation. Claygent fetches page content using third-party scraping services and analyzes the HTML and text — it does not trace JavaScript execution events, intercept network requests, or follow `<script src>` links the way a browser developer tool would. When prompting Claygent to look for tracking pixels or marketing technologies, write the prompt to analyze page content (for example: *"Look at this company's website and check whether the page HTML contains tracking pixel tags such as the Facebook Pixel or Google Tag Manager"*) rather than instructions that assume DevTools-style network monitoring.

**JavaScript-rendered pixels**: Claygent has a JavaScript rendering fallback, but it only activates when a page returns essentially empty static HTML. Most marketing websites return non-empty HTML even when some content is JavaScript-loaded — meaning the JS rendering path typically does not trigger. Pixel tags that are injected dynamically by JavaScript after page load (common for Facebook Pixel, Google Tag Manager, TikTok Pixel, etc.) are likely to be missed on typical marketing sites. There is no single-step solution in Clay for detecting JS-rendered pixels.

**Alternative**: The **BuiltWith** integration (**Find Technology Stack** action) can confirm whether a particular technology is present on a site, but it does not return specific pixel IDs or tracking codes.

### Why does a column referencing my Claygent output show "Cell data size exceeds limit (8 kB)"?

Clay enforces two different cell size limits: Claygent action columns hold up to **200 kB**, while basic columns — text fields and formula columns that reference or extract from those action columns — are limited to **8 kB**. When a Claygent produces verbose output (such as detailed research logs or step-by-step notes) and that value is extracted into a standalone text column or referenced by a formula column, the result must fit within the 8 kB limit for that basic column.

Changing the column data type will not bypass this limit — the constraint is on the column type, not the data format.

**Fix: reduce output size at the source.** Edit your Claygent prompt or output schema to produce more concise results for the fields being referenced downstream. For example, if your agent records step-by-step research notes, instruct it to summarize each step in 50 characters or fewer. This keeps each output field well within the 8 kB limit.

**Alternatively**, reference the Claygent action column directly in downstream formulas — using `/` to navigate into specific properties — rather than extracting large fields into standalone text columns. Accessing a property of the action column reads from its 200 kB store; only columns that *hold* a copy of the value as text are subject to the 8 kB limit.

## Tips for success

**Importing test cases**: Instead of manually creating test data, import real rows from your tables. Click `Import from table` in the test panel to pull actual data and see how your agent performs on real-world inputs.

**Variable mapping**: When deploying a Claygent to a new table with different column names, Builder will auto-suggest mappings. Review these carefully to ensure the correct data flows through.

**Start simple**: Build your agent with a basic prompt first, test it, then layer in complexity. It's easier to debug and refine when you're working incrementally.
