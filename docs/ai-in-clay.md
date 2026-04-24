---
title: AI in Clay
source_url: https://university.clay.com/docs/ai-in-clay
---

# AI in Clay

A comprehensive guide to how Clay uses AI across its features, with a focus on data privacy, security, and responsible AI practices.

## Core AI Principles

Clay is committed to transparent and responsible AI use:

- **No training on your data**: Customer data is never used to train Clay's AI models or those of AI providers.
- **Enterprise-grade security**: Industry-standard encryption for data at rest and in transit, with SOC 2 Type II and ISO 27001 compliance.
- **You control your data**: As a data processor, Clay only uses your data to provide services to you.
- **Transparent partnerships**: Full list of AI subprocessors available at trust.clay.com.

## AI Features in Clay

### Email Sequencer

Built-in email outreach tool that runs campaigns directly from tables using AI for personalized messaging at scale.

**How AI is used:**
- Generates email copy based on business context and prospect information
- AI snippets create personalized content using lead data
- Content generation happens in real-time when creating campaigns

**Data privacy:**
- Campaign data and prospect information processed only to generate email content
- No data retained by AI providers after processing
- Data not used to train models or shared with other customers
- Option to use your own API keys with supported providers

### Message Drafting

AI-powered message drafting helps create personalized outreach messages for individual prospects.

**How AI is used:**
- Reads context from table columns (company info, prospect details, etc.)
- Generates tailored messages based on prompts and business context
- Uses "My Business Context" settings to maintain brand voice

**Data privacy:**
- Only selected table data is sent to AI models
- Messages generated on-demand with no post-processing retention
- No training occurs on messaging or prospect data
- Access controlled by role-based permissions

### Use AI Action

Powerful table action providing access to AI for web research, content generation, and image generation.

**How AI is used:**
- **Web research**: Searches and synthesizes information from the web
- **Content generation**: Transforms unstructured text into structured data
- **Image generation**: Creates images based on text prompts

**Model options:**
- Access to models from OpenAI, Anthropic, Google, and other providers
- Option to bring your own API keys for supported providers
- MCP (Model Context Protocol) server support when using your own keys
- Different models offer different capabilities

**Data privacy:**
- Data from table rows sent to AI only when explicitly running the action
- Control which columns are included as context
- Contractual agreements prohibit training on customer data

### Claygents

Build repeatable AI agents for web research and prospecting that navigate websites, extract information, and make decisions.

**How AI is used:**
- AI agents follow instructions to research prospects, companies, or topics
- Navigate web pages and extract specific information
- Make intelligent decisions about which sources to consult

**Data privacy:**
- Process data row-by-row as they run
- Research results stored in your table under your control
- No customer data used for training agent capabilities

### Sculptor

Chat interface for Clay helping with table building, debugging, and analysis.

**How AI is used:**
- Reads "My Business Context" to understand your goals
- Accesses information in current table for relevant help
- Suggests formulas, identifies issues, and analyzes data

**Data privacy:**
- Only accesses the specific table you're working in
- Uses table metadata and visible data for context-aware assistance
- Chat history and table context not used for training
- Data processed transiently for real-time assistance

### Formula Generator

AI-powered tool that creates Clay formulas using natural language.

**How AI is used:**
- Converts natural language description into working formulas
- Understands Clay's formula syntax and functions
- Suggests appropriate formulas based on use case

**Data privacy:**
- Only formula description and relevant table schema sent to AI
- Actual row data not transmitted
- Generated formulas not used to train models
- Processing is instantaneous with no data retention

### API Generator

Helps build HTTP API requests using AI for easier external service connections.

**How AI is used:**
- Generates API request configurations based on descriptions
- Understands common API patterns and authentication methods
- Suggests appropriate parameters and headers

**Data privacy:**
- Only API description sent to AI models
- API keys and credentials never sent to AI providers
- Generated configurations not used for training

### Debug with AI

When errors occur, AI helps diagnose and suggest fixes using error logs and Clay documentation.

**How AI is used:**
- Analyzes error messages and logs
- References Clay's documentation to suggest solutions
- Provides step-by-step troubleshooting guidance

**Data privacy:**
- Only error logs and system information sent to AI
- Personal data in tables not included in debug requests
- Error analysis done in real-time with no retention
- Debug data not used to train models

### Find Companies with Natural Language

Import feature allowing you to describe your ideal customer profile (ICP) and search Clay's database of 50M+ companies.

**How AI is used:**
- Interprets natural language ICP descriptions
- Converts criteria into database queries
- Ranks and filters companies based on fit

**Data privacy:**
- Only ICP description processed by AI
- Search results from Clay's company database, not your data
- Search criteria not shared with other customers
- No training occurs on ICP descriptions

## Data Security and Compliance

### Encryption

- **At rest**: Industry-standard encryption for all customer data
- **In transit**: TLS 1.2/1.3 encryption for all data transmission
- **Access controls**: Role-based permissions control data access

### Compliance Certifications

- **SOC 2 Type II**: Active certification for security and privacy controls
- **ISO 27001**: Compliance with international information security standards
- **GDPR**: Full compliance with European data protection regulations
- **CCPA**: Compliance with California Consumer Privacy Act

### Third-Party AI Providers

Clay partners with leading AI providers with contractual obligations to:

- Never train models on customer data
- Maintain security certifications (SOC 2, ISO 27001)
- Comply with data protection regulations

Current AI subprocessors include:

- OpenAI
- Anthropic
- Google (Gemini models)
- Other leading AI providers

Full subprocessor list: trust.clay.com

### Data Processing

- **Data location**: Primarily processed in the United States (AWS US-East)
- **Data controller vs. processor**: Clay acts as a data processor; you remain the data controller
- **Data deletion**: Delete data at any time; workspace deletion removes all data after 30 days
- **Data access**: Only you and authorized workspace users can access your data

## Your Rights and Controls

### What You Control

- **Which AI features you use**: All AI features are opt-in through actions
- **What data AI sees**: Choose which table columns to include in AI requests
- **API keys**: Option to bring your own API keys for supported providers
- **Data deletion**: Delete individual records, tables, or entire workspaces at any time
- **Access permissions**: Control who in your organization can use AI features

### What Clay Guarantees

- "Your data will never be used to train AI models"
- Your data will not be shared with other Clay customers
- All AI subprocessors have contractual prohibitions against unauthorized use
- Industry-standard security and encryption protect your data

## Available AI Models

| Provider | Models |
|----------|--------|
| Clay | Helium, Neon, Argon, Xenon, Radon, Clay Conductor, Clay Navigator |
| OpenAI | GPT 4o, 4.1, 4o Mini; GPT 4.1 Mini, 4.1 Nano; GPT 5, 5.1, 5 Mini, 5 Nano; o1, o1 Pro, o1 Mini; o3, o3 Mini, o3 Deep Research; o4 Mini; DALL·E 3 (Standard, HD); GPT Image 1 (Low, Medium, High) |
| Anthropic | Claude 3 Haiku, Claude 3.5 Haiku, Claude 3.7 Sonnet, Claude 4 Sonnet, Claude 4 Opus, Claude 4.5 Sonnet, Claude 4.5 Haiku, Claude 4.5 Opus, Claude 4.6 Opus |
| Gemini | 2.0 Flash, Flash Lite; 2.5 Flash, Flash Lite; 2.5 Pro, 3 Pro; Imagen 3.0, 3.0 Fast |
| xAI | Grok 4, Grok 4.1 Fast Reasoning |
| DeepSeek | DeepSeek R1, DeepSeek V3.2 |
| Mistral | Mistral Medium 3, Mistral Large 2.1, Mistral Large 3, Magistral Medium, Devstral 2 |
| BlackForestLabs | Flux 1 Schnell, Flux 1 Dev |
| Playground | Playground V2, Playground V2.5 |
| Segmind | SSD 1B |
| Stability | Stable Diffusion XL 1024 |

## Questions?

For more information about Clay's security and privacy practices:

- **Trust Center**: trust.clay.com
- **Privacy Policy**: privacy.clay.com
- **Security inquiries**: security@clay.com
- **Compliance documentation**: Available upon request through your account team
