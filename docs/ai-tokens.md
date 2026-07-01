---
title: AI Tokens
description: Understand AI Tokens
last_synced: 2026-04-26T01:39:40.311Z
---

# AI Tokens

Understand AI Tokens

# Understanding AI Tokens

In the world of Large Language Models (LLMs), **tokens** are the fundamental building blocks for processing and understanding text.

Think of tokens as small chunks, each typically representing 3-4 characters. A 100-word passage generally breaks down into approximately **125–135 tokens**.

When working with AI models, you'll encounter two types:

-   **Input tokens**: The prompts you send to the AI.
-   **Output tokens**: The AI's generated response.

**Note:** In Clay, you can control usage by setting a maximum output length in your model configuration.

## What Is TPM?

**TPM (Tokens Per Minute)** refers to how many tokens a model can process within one minute—across both input and output. Different features and providers have different TPM requirements, often tied to your API tier.

## API tier requirements

### ChatGPT Generate Text

-   **Requirement**: 30,000 TPM
-   **Access**: Works with **any paid tier** as long as the API key has access to GPT-4 or GPT-4 Turbo
-   _(Note: Free-tier or unpaid OpenAI keys may not have access)_

### ClayGent Web Research

-   **OpenAI**: Requires **Tier 2 or higher** (≥450,000 TPM)
-   **Anthropic**: Requires **Tier 4 or higher** (≥450,000 TPM)
-   **Gemini**:
    -   Requires **Tier 2**, but only works with the **Gemini 2.0 Flash model**
    -   **Gemini 1.5 models** may require additional access through **Vertex AI** or custom tiers

## Upgrade API tier

If you need higher token limits or access to advanced features, you'll need to upgrade your API tier with your chosen provider.

Here's how to find more information on upgrading, with each major provider.

-   [OpenAI](https://platform.openai.com/docs/guides/rate-limits/usage-tiers#usage-tiers)
-   [Anthropic](https://docs.anthropic.com/en/api/rate-limits)
-   [Gemini](https://support.google.com/gemini/answer/14517446?hl=en-MY)

## Monitoring API Usage

Each platform provides tools to track your usage:

-   [OpenAI](https://platform.openai.com/account/usage)
-   [Anthropic](https://docs.anthropic.com/en/api/rate-limits)
-   [Gemini](https://cloud.google.com/gemini/docs/monitor-gemini)

## AI pricing in Clay

When using AI features in Clay, you'll consume both **Actions** and **Data Credits**:

-   **Actions**: Each AI enrichment consumes 1 Action (platform orchestration work)
-   **Data Credits**: Cost varies by model—Clay offers both fixed and variable AI pricing

Clay uses two pricing structures for AI models:

-   **Fixed pricing**: A flat number of data credits per task (applies to most models, including Clay's own models like Neon, Helium, and Argon)
-   **Variable pricing**: Data credits based on actual token usage plus a 20% premium (applies to advanced reasoning models used for sophisticated web research)

You can control AI spending by:

-   Setting maximum output length in your model configuration
-   Setting custom budgets for each run
-   Choosing more cost-effective models for simpler tasks
-   Selecting fixed-price models when cost predictability is important

To learn more about how AI is priced in Clay, see our guide on [how AI is priced](https://www.clay.com/university/guide/how-ai-is-priced).

## Clay credits vs. personal API keys

When you're using Clay's AI tools, you have two options for managing your API access: using [Clay credits](https://www.clay.com/university/guide/credits) or connecting your own personal API keys.

Each option has different benefits and considerations in terms of cost, convenience, and management requirements. Let's explore these options:

### Clay credits

-   Clay manages rate limits, tier access, and scaling for you
-   No need to worry about upgrading API tiers manually
-   Pricing varies by model (fixed or variable depending on which model you select)
-   Cost visibility in Clay UI shows data credit consumption

**Output token limit with Clay's managed key:** When using Clay's shared key (Clay credits) with a **premium model** (such as GPT-4o, Claude Sonnet, or Gemini 2.5 Pro), output tokens are capped at **4,000 per request**. If your column's maximum output length exceeds this, you'll see the error: **"Maximum tokens is too large. Please use a private key or contact support."** This cap does not apply to compact or budget models (such as GPT-4o mini or Claude Haiku). To work around this limit when using premium models, lower your column's maximum output setting to 4,000 or fewer, or connect your own API key (see "Personal API Keys" below).

### Personal API Keys

-   Can reduce data credit costs (you only pay Actions, not Data Credits)
-   Requires **meeting provider-specific tier requirements**
-   You manage your own API billing directly with the provider
-   No output token cap from Clay's side (the model's own context length still applies)

**Note:** When using a personal API key, price breakdowns won't appear in the Clay UI. You'll need to monitor your usage and upgrade tiers manually.

**If you see "Rate limit wait time exceeded" errors when running many rows simultaneously with a personal OpenAI API key:** Clay runs multiple rows in parallel, which can exhaust your OpenAI account's tokens-per-minute (TPM) or requests-per-minute (RPM) limits faster than expected. Clay automatically retries rate-limited requests, but if the limit persists, cells will return a **"Rate limit wait time exceeded"** error. To resolve this:

-   **Upgrade your OpenAI API tier** — higher tiers provide significantly more TPM and RPM capacity. See [OpenAI usage tiers](https://platform.openai.com/docs/guides/rate-limits/usage-tiers#usage-tiers) for details.
-   **Switch to Clay credits** — Clay manages OpenAI rate limits, tier access, and scaling on your behalf, so individual key limits don't apply (see "Clay credits" above).

**If you hit Gemini API rate limits with a personal API key:** The Gemini API enforces rate limits on calls from Clay independently of Google AI Studio — AI Studio may show available capacity while API calls are still throttled. To resolve rate limit errors:

-   **Switch to Clay credits** — Clay automatically manages Gemini rate limits, tier access, and scaling on your behalf (see "Clay credits" above).
-   **Upgrade your Google Cloud API tier** — higher tiers provide increased rate limits. See [Gemini rate limits](https://ai.google.dev/gemini-api/docs/rate-limits) for tier details.
-   **Monitor your current consumption** — use the [Gemini API usage dashboard](https://cloud.google.com/gemini/docs/monitor-gemini) to review rate limits and identify caps or reset windows.

**If you see "The model provider's rate limits are low" with a private Gemini API key:** AI columns using a personal Google Gemini API key can show the error **"The model provider's rate limits are low. Please try again later or increase your limits."** even when your own account's TPM quota has not been reached. This happens because personal Gemini keys use the Google AI Studio API, which runs on shared infrastructure — Google pools AI Studio requests from all customers into shared capacity provisioning. When that shared pool is under heavy load from other users, requests can be rejected regardless of your individual quota.

**Clay's managed Gemini account (Clay credits) routes requests through Google Vertex AI with dedicated GCP capacity**, which is not subject to the same shared-capacity constraints. To resolve this error:

-   **Switch to Clay credits** — open the column settings, click the **Account** dropdown, and select the default Clay-managed account. This routes your requests through Vertex AI's dedicated capacity.
-   **Retry the affected rows** — if you need to keep your personal key, the error is typically intermittent. Re-running failed cells usually succeeds once Google's shared capacity pressure eases.

**If enrichment cells show "Retrying" when using a personal Anthropic API key:** Clay runs rows in parallel, which can quickly exhaust Anthropic API rate limits — especially on lower tiers. When Clay receives a rate-limit response from Anthropic, it sets the affected cells to a "Retrying" state and waits before attempting again. If the rate limit persists, cells may remain in this state for an extended period or ultimately fail. To resolve this:

-   **Run fewer rows at a time** — lower-tier Anthropic accounts have lower requests-per-minute (RPM) and tokens-per-minute (TPM) limits. Running smaller batches reduces the chance of hitting these limits. See [Anthropic API rate limits](https://docs.anthropic.com/en/api/rate-limits) for your tier's specific limits, and [Anthropic API settings](https://console.anthropic.com/settings/limits) to check your current tier.
-   **Upgrade your Anthropic API tier** — higher tiers provide significantly more TPM and RPM capacity, which reduces retry frequency when running large tables.
-   **Switch to Clay credits** — Clay manages Anthropic rate limits, tier access, and scaling on your behalf, so individual key limits don't apply (see "Clay credits" above).
