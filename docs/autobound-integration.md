---
title: Autobound integration
source_url: https://university.clay.com/docs/autobound-integration
last_synced: 2026-04-26T01:39:41.943Z
upstream_hash: cbb5a98a53e5bf3071ad5fa7c1783a1c66a16c13f7efbb12ec139d1319d44fdc
---

# Autobound integration

Automates personalized email creation and insight generation

Autobound automates personalized email creation and insight generation, improving outreach efficiency by tailoring content to each contact's unique profile and company data.

With this integration, you can create targeted outreach, generate personalized content, and gather comprehensive company insights based on data analysis.

## **Enriching data with Autobound**

1.  While in a Clay table, click `Add enrichment` and search for `Autobound`.
2.  Under `Integrations`, select one of the Autobound options.
3.  In the modal, you will be asked to `Select Autobound account`.
    -   If you have your own account, click `+ Add account` and go through authentication. Otherwise, use the Clay provided key.

### `Action` Generate personalized content

Use this action to create highly personalized outreach by leveraging 300+ data points about both sender and recipient, including news, growth trends, social media, and podcast mentions.

**Inputs**

-   **User Identity** (at least one required):
    -   User LinkedIn URL: Identifies sender for relevant insights
    -   User email address: Alternative sender identification
    -   User company URL: Explicitly sets sender's company
-   **Contact Identity** (at least one required):
    -   Contact LinkedIn URL: Identifies prospect and their company
    -   Contact email address: Alternative prospect identification
    -   Contact company URL: Identifies company when other identifiers unavailable
-   **Content type:**
    -   Email
    -   Email opener
    -   Call script
    -   LinkedIn connection request
    -   SMS text
    -   Email sequence (2 steps, 10.5 credits)
    -   Email sequence (3 steps, 14 credits)
    -   Email sequence (4 steps, 17.5 credits)
-   **Writing style:** Basho, Challenger sale, Clever poet, C-suite pitch, Data-driven, Why you why now, or Custom
-   **Value proposition:** Format example: "Most \[personas\] struggle with \[pain point\]. We help achieve \[benefit\] by \[unique approach\]"
-   **Additional context:** Freeform guidance like opportunity notes or past conversations

**Output**

-   Emails: Subject line and message body
-   Email sequences: Multiple email messages with subject lines
-   Other content types: Appropriately formatted content

### `Action` Generate people and company insights

Use this action to create personalized insights for outreach by leveraging LinkedIn and email data to streamline research and power personalized content creation.

**Inputs**

-   **User LinkedIn URL or User email address (Required):** Used to identify the seller for generating relevant relationship insights.
-   **Contact LinkedIn URL or Contact email address (Required):** Used to identify the prospect and their company.
-   **Insight subtypes (Optional):** Specify up to 5 types of insights you want to focus on.

### `Action` Generate company insights

Use this action to gather company-level intelligence to enhance lead engagement and conversion strategies.

**Inputs**

-   **Contact company URL (Required):** Used to resolve the prospect's company domain.
-   **Optional Identification Fields (at least one required):**
-   **User LinkedIn URL:** Used to identify the seller for returning relevant insights, including relationship insights between companies.
-   **User email address:** Alternative way to identify the seller.
-   **User company URL:** Used to identify the seller's company.
-   **Insight subtypes (Optional):** Specify up to 5 specific insight types:
    -   Company business model
    -   Employee breakdown and growth (by department & over time)
    -   HR Specific: Employee breakdown and growth
    -   Finance Specific: Employee breakdown and growth
    -   Market trends
    -   Prospect's case study
    -   Prospect's customers
    -   Prospect's investors
    -   Competitor's earnings call
    -   Names of prospect's competitors
    -   Prospect's competitor is your customer
    -   Company is earning less and profits are shrinking
    -   Company's earnings and operational efficiency are too low

**Output**

-   Funding rounds
-   Hiring trends
-   Competitor moves
-   10-K filings
-   Earnings calls
-   35+ news event types

### **Run settings**

-   **Auto-update**
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))
