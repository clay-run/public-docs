---
title: AI Tokens
source_url: https://university.clay.com/docs/ai-tokens
last_synced: 2026-04-26T01:39:40.311Z
upstream_hash: e76788a436ea719a65ef09ac82d75d3a9d7cede5e2ef35a9bd2947b54c6f8506
---

# AI Tokens

Understand AI Tokens

# Understanding AI Tokens

In the world of Large Language Models (LLMs), **tokens** are the fundamental building blocks for processing and understanding text.

Think of tokens as small chunks, each typically representing 3-4 characters. A 100-word passage generally breaks down into approximately **125–135 tokens**.

When working with AI models, you'll encounter two types:

-   **Input tokens**: The prompts you send to the AI.
-   **Output tokens**: The AI’s generated response.

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
-   **Anthropic**: Requires **Tier 4 or higher** (≥400,000 TPM)
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

### Personal API Keys

-   Can reduce data credit costs (you only pay Actions, not Data Credits)
-   Requires **meeting provider-specific tier requirements**
-   You manage your own API billing directly with the provider

**Note:** When using a personal API key, price breakdowns won't appear in the Clay UI. You'll need to monitor your usage and upgrade tiers manually.
