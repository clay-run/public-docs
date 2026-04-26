---
title: AI in Clay
source_url: https://university.clay.com/docs/ai-in-clay
description: A comprehensive guide to how Clay uses AI across its features.
last_synced: 2026-04-26T01:39:39.278Z
upstream_hash: ab5a2532485680f80f2914a032bb5c46561638991f78f21d5ec6d399949698fa
---

# AI in Clay

A comprehensive guide to how Clay uses AI across its features.

A comprehensive guide to how Clay uses AI across its features, with a focus on data privacy, security, and responsible AI practices.

**Your data is never used for AI model training.** Clay has contractual agreements with all AI providers (OpenAI, Anthropic, Google, and others) that strictly prohibit using customer data to train their models.

## Core AI principles

Clay is committed to transparent and responsible AI use. Here's what you need to know:

-   **No training on your data**: Customer data is never used to train Clay's AI models or those of our AI providers.
-   **Enterprise-grade security**: Industry-standard encryption for data at rest and in transit, with SOC 2 Type II and ISO 27001 compliance.
-   **You control your data**: As a data processor, Clay only uses your data to provide services to you.
-   **Transparent partnerships**: Full list of AI subprocessors available at [trust.clay.com](http://trust.clay.com).

## AI features in Clay

### Email sequencer

**What it does**: Email Sequencer is Clay's built-in email outreach tool that lets you run email campaigns directly from your tables, using AI to create personalized messaging at scale.

[View Email Sequencer documentation →](https://www.clay.com/university/guide/email-sequencer)

**How AI is used**:

-   AI generates email copy based on your business context and prospect information.
-   AI snippets within messages automatically create personalized content using lead data.
-   Content generation happens in real-time when you create campaigns.

**Data privacy**:

-   Your campaign data and prospect information are processed only to generate your email content.
-   No data is retained by AI providers after processing.
-   Data is not used to train models or shared with other Clay customers.
-   You can optionally use your own API keys with supported providers.

### Message drafting

**What it does**: AI-powered message drafting within Clay tables helps you create personalized outreach messages for individual prospects.

[View Email sequencer documentation →](https://www.clay.com/university/guide/email-sequencer)

**How AI is used**:

-   AI reads context from your table columns (company info, prospect details, etc.).
-   Generates tailored messages based on your prompts and business context.
-   Uses your "My Business Context" settings to maintain brand voice.

**Data privacy**:

-   Only the specific table data you select is sent to AI models.
-   Messages are generated on-demand and data is not retained post-processing.
-   No training occurs on your messaging or prospect data.
-   Access is controlled by Clay's role-based permissions.

### Use AI action

**What it does**: A powerful table action that gives you access to AI for web research, content generation, and image generation.

[View Use AI documentation →](https://www.clay.com/university/guide/use-ai-integration-overview)

**How AI is used**:

-   **Web research**: AI searches and synthesizes information from the web.
-   **Content generation**: Transforms unstructured text (like call transcripts) into structured data.
-   **Image generation**: Creates images based on text prompts.

**Model options**:

-   Access to models from OpenAI, Anthropic, Google, and other leading AI providers.
-   Option to bring your own API keys for supported providers.
-   MCP (Model Context Protocol) server support when using your own keys.
-   Different models offer different capabilities (document upload, specialized research, etc.).

**Data privacy**:

-   Data from your table rows is only sent to AI when you explicitly run the action.
-   You control which columns are included as context.
-   Contractual agreements prohibit training on customer data.

### Claygents

**What it does**: Build repeatable AI agents for web research and prospecting that can navigate websites, extract information, and make decisions.

[View Claygent builder documentation →](https://www.clay.com/university/guide/claygent-playground)

**How AI is used**:

-   AI agents follow your instructions to research prospects, companies, or topics.
-   Navigate web pages and extract specific information.
-   Make intelligent decisions about which sources to consult.

**Data privacy**:

-   Claygents process data row-by-row as they run.
-   Research results are stored in your table, under your control.
-   No customer data used for training agent capabilities.

### Sculptor

**What it does**: A chat interface for Clay that helps with table building, debugging, and analysis using conversational AI.

[View Sculptor documentation →](https://www.clay.com/university/guide/sculptor)

**How AI is used**:

-   Reads your "My Business Context" to understand your goals.
-   Accesses information in your current table to provide relevant help.
-   Suggests formulas, identifies issues, and helps analyze data.

**Data privacy**:

-   Only accesses the specific table you're working in.
-   Uses table metadata and visible data to provide context-aware assistance.
-   Chat history and table context are not used for training.
-   Data is processed transiently to provide real-time assistance.

### Formula generator

**What it does**: AI-powered tool that helps you create Clay formulas using natural language.

**How AI is used**:

-   Converts your natural language description into working formulas.
-   Understands Clay's formula syntax and functions.
-   Suggests appropriate formulas based on your use case.

**Data privacy**:

-   Only your formula description and relevant table schema are sent to AI.
-   Actual row data is not transmitted.
-   Generated formulas are not used to train models.
-   Processing is instantaneous with no data retention.

### API generator

**What it does**: Helps you build HTTP API requests using AI, making it easier to connect to external services.

[View HTTP API documentation →](https://www.clay.com/university/guide/http-api-integration-overview)

**How AI is used**:

-   Generates API request configurations based on your description.
-   Understands common API patterns and authentication methods.
-   Suggests appropriate parameters and headers.

**Data privacy**:

-   Only your API description is sent to AI models.
-   API keys and credentials are never sent to AI providers.
-   Generated configurations are not used for training.

### Debug with AI

**What it does**: When errors occur in Clay, AI helps diagnose and suggest fixes using error logs and Clay documentation.

**How AI is used**:

-   Analyzes error messages and logs.
-   References Clay's documentation to suggest solutions.
-   Provides step-by-step troubleshooting guidance.

**Data privacy**:

-   Only error logs and relevant system information are sent to AI.
-   Personal data in your tables is not included in debug requests.
-   Error analysis is done in real-time with no retention.
-   Debug data is not used to train models.

### Find companies with natural language

**What it does**: An import feature that lets you describe your ideal customer profile (ICP) and searches Clay's database of 50M+ companies.

**How AI is used**:

-   Interprets your natural language ICP description.
-   Converts your criteria into database queries.
-   Ranks and filters companies based on fit.

**Data privacy**:

-   Only your ICP description is processed by AI.
-   Search results come from Clay's company database, not your data.
-   Your search criteria are not shared with other customers.
-   No training occurs on your ICP descriptions.

## Data Security and Compliance

### Encryption

-   **At rest**: All customer data is encrypted using industry-standard encryption.
-   **In transit**: TLS 1.2/1.3 encryption for all data transmission.
-   **Access controls**: Role-based permissions control who can access your data.

### Compliance Certifications

-   **SOC 2 Type II**: Active certification for security and privacy controls.
-   **ISO 27001**: Compliance with international information security standards.
-   **GDPR**: Full compliance with European data protection regulations.
-   **CCPA**: Compliance with California Consumer Privacy Act.

### Third-Party AI Providers

Clay partners with leading AI providers, all of whom have contractual obligations to:

-   **Never train models on customer data.**
-   **Maintain security certifications** (SOC 2, ISO 27001).
-   **Comply with data protection regulations.**

Our current AI subprocessors include:

-   [OpenAI](https://trust.openai.com/)
-   [Anthropic](https://trust.anthropic.com/)
-   [Google](https://support.google.com/gemini/answer/13594961?hl=en) (Gemini models).
-   Other leading AI providers.

Full subprocessor list: [trust.clay.com](http://trust.clay.com)

### Data Processing

-   **Data location**: Customer data is primarily processed in the United States (AWS US-East).
-   **Data controller vs. processor**: Clay acts as a data processor; you remain the data controller.
-   **Data deletion**: You can delete your data at any time; workspace deletion removes all data after 30 days.
-   **Data access**: Only you and authorized users in your workspace can access your data.

## Your Rights and Controls

### What you control:

-   **Which AI features you use**: All AI features are opt-in through your actions.
-   **What data AI sees**: You choose which table columns to include in AI requests.
-   **API keys**: Option to bring your own API keys for supported providers.
-   **Data deletion**: Delete individual records, tables, or entire workspaces at any time.
-   **Access permissions**: Control who in your organization can use AI features.

### What Clay guarantees:

-   Your data will never be used to train AI models.
-   Your data will not be shared with other Clay customers.
-   All AI subprocessors have contractual prohibitions against unauthorized use.
-   Industry-standard security and encryption protect your data.

## Available AI Models

Clay provides access to a wide range of AI models from multiple providers. Below is a complete list of available models:

| Provider | Models |
| --- | --- |
| Clay | HeliumNeonArgonXenonRadonClay ConductorClay Navigator |
| OpenAI | GPT 4o, 4.1, 4o MiniGPT 4.1 Mini, 4.1 NanoGPT 5, 5.1, 5 Mini, 5 Nanoo1, o1 Pro, o1 Minio3, o3 Mini, o3 Deep Researcho4 MiniDALL·E 3 (Standard, HD)GPT Image 1 (Low, Medium, High) |
| Anthropic | Claude 3 HaikuClaude 3.5 HaikuClaude 3.7 SonnetClaude 4 SonnetClaude 4 OpusClaude 4.5 SonnetClaude 4.5 HaikuClaude 4.5 OpusClaude 4.6 Opus |
| Gemini | 2.0 Flash, Flash Lite2.5 Flash, Flash Lite2.5 Pro, 3 ProImagen 3.0, 3.0 Fast |
| xAI | Grok 4Grok 4.1 Fast Reasoning |
| DeepSeek | DeepSeek R1DeepSeek V3.2 |
| Mistral | Mistral Medium 3Mistral Large 2.1Mistral Large 3Magistral MediumDevstral 2 |
| BlackForestLabs | Flux 1 SchnellFlux 1 Dev |
| Playground | Playground V2Playground V2.5 |
| Segmind | SSD 1B |
| Stability | Stable Diffusion XL 1024 |

Questions?

For more information about Clay's security and privacy practices:

-   **Trust Center**: [trust.clay.com](http://trust.clay.com)
-   **Privacy Policy**: [privacy.clay.com](http://privacy.clay.com)
-   **Security inquiries**: [security@clay.com](mailto:security@clay.com)
-   **Compliance documentation**: Available upon request through your account team.

Clay is committed to transparent and responsible AI use. If you have specific questions about how AI works with your data, please reach out to our support team.
