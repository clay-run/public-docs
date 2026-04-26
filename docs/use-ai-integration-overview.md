---
title: Use AI
source_url: https://university.clay.com/docs/use-ai-integration-overview
last_synced: 2026-04-26T01:40:51.610Z
upstream_hash: 5e052c3431d3995a65e673b1d74a3a9eecf97f653b75c2eeb1aa3f8ac9d4cefb
---

# Use AI

Leverage AI to process, categorize, and conduct web research for actionable insights.

The **Use AI** feature in Clay allows users to automate tasks like content creation, data enrichment, and web research using GPT, Claude, or Gemini AI models.

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
    1.  **Web research:** Scrape and analyze websites.
    2.  **Content creation, manipulation:** Create and manipulate data in your table.
4.  Select a `Model` from the dropdown.
    1.  Click `Compare models` to get more detailed information about each model.
5.  Write a `Prompt`.
    -   For guidance on writing effective prompts, see our doc on [writing prompts](https://www.clay.com/university/guide/ai-metaprompter-guide).
6.  _(Optional – Content creation, manipulation only)_ Provide context for task.
7.  Add and define outputs.
    -   **Fields**
        -   In the text field, enter the field names where you want the output to appear.
        -   Use the dropdown menu to select the appropriate data type for each output field.
    -   **JSON Schema**
8.  _(Optional – Content creation, manipulation only)_ Click `Examples` and `Add examples` to show AI what responses should look like.

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

Clay's Use AI feature leverages three powerful AI models: GPT, Claude, and Gemini.

To learn more about each model's capabilities and prompting best practices, refer to their official documentation:

-   [Anthropic](https://docs.anthropic.com/en/docs/about-claude/models)
-   [OpenAI](https://platform.openai.com/docs/models)
-   [Google Gemini](https://ai.google.dev/gemini-api/docs/models/gemini)

### Connecting your own API keys

By default, Use AI uses the Clay-managed account, though you can select other accounts during setup.

While you don't need your own GPT, Claude, or Gemini API key to use the AI features, having one may reduce costs.

1.  Select the desired `Model` from the dropdown.
2.  Click on the `Account` dropdown and click `+ Add account`.
