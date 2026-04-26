---
title: Twain integration
source_url: https://university.clay.com/docs/twain-integration-overview
description: The accurate deep research API for GTM Engineers building agents.
last_synced: 2026-04-26T01:40:49.969Z
upstream_hash: 8cb94f77a7fb733ee515bf6e0eafb19306c780319bf48533c730845bc9c16be3
---

# Twain integration

The accurate deep research API for GTM Engineers building agents.

Twain has developed accurate deep research for GTM agents. GTM Engineering and Growth Teams use Twain for automated outreach campaigns using signal-based personalization. Sales Enablement and RevOps teams to generate real-time account and contact based insights to support SDRs and AEs.

By verifying signals like job changes and company news through a proprietary multi-agent safety net, Twain ensures every sequence is factually accurate and backed by detailed research proof. This allows revenue teams to scale personalized communication while protecting brand reputation and ensuring 100% factual accuracy across all automated workflows.

You can choose between two APIs: one to generate research-backed 1:1 outreach for inbound and outbound workflows and another one to enable sales teams with real-time deep research on account and lead level.

Both APIs have access to deep research and qualification agents. Out of the box, no prompting needed.

## **Enriching data with Twain V3**

1.  While in a Clay table, click `Add enrichment` and search for `Twain V3`.
2.  Under `Integrations`, select one of the Twain V3 options.
    -   If you haven't already connected your Twain V3, click `+ Add account` and go through authentication.

**Important:** Unlike other integrations that allow you to use the "Clay provided" public key, Twain only supports private keys. You must sign up on [twain.ai](http://twain.ai) to get started.

**Learn more:** For more information about Twain, check out this [playlist](\<https://www.youtube.com/playlist?list=PLURB-4aGAMq4jqN9bJ_EmvOAn8_hlPoPB\>).

## **`Action` Generate outreach with deep research**

Automates the creation of AI-personalized sales outreach messages tailored to each prospect.

### **Inputs**

**Required:**

-   `Campaign` - The Twain campaign you want to use for generating sequences. Displays as a dropdown if using a private key, or text input field if using shared account.

**Optional (Prospect Information):**

-   `Prospect LinkedIn URL` - Your prospect's LinkedIn profile URL. Alternatively, add your prospect's work email. One of the two is required. The results will be more granular if you use the LinkedIn profile URL.
-   `Prospect email address` - Your prospect's work email address. Alternatively, add your prospect's LinkedIn profile URL. One of the two is required. The results will be more granular if you use the LinkedIn profile URL.
-   `Prospect name` - The prospect's name.
-   `Prospect company domain` - The prospect's company domain.
-   `Prospect extra info` - Additional information you know about the prospect that's relevant to the sequence (e.g., "Has hired 5 people this year. Made a blog post about GTM engineering.").
-   `Prospect trigger / signal` - Why are you reaching out to this specific prospect right now (e.g., "Posted a job ad on LinkedIn to hire GTM engineers for their team.").

**Optional (Custom Variables):**

Twain supports up to 10 custom variables that can be passed directly from Clay. These variables can be created on the fly - they don't need to pre-exist in Twain. This allows you to pass any unique data points you discover in Clay directly into your Twain campaigns.

For each custom variable (1-10):

-   `Custom Variable Name` - The name of the custom variable.
-   `Custom Variable Value` - The value of the custom variable.
-   `Custom Variable Description` - Description of the custom variable.

### **Run settings**

-   `Auto-update`
-   `Only run if:` The enrichment will only run if conditions are met. ([**Learn more about conditional formulas here!**](https://www.notion.so/2ef7e66eb01480b4871bd7e06cc936df?pvs=21))
