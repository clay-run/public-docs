---
title: Lead-to-account matching for Salesforce
description: Connect Salesforce leads with their corresponding Salesforce accounts.
last_synced: 2026-04-26T01:40:13.950Z
---

# Lead-to-account matching for Salesforce

Connect Salesforce leads with their corresponding Salesforce accounts.

Clay offers powerful lead-to-account matching capabilities that help you efficiently connect Salesforce leads with their corresponding Salesforce accounts. Here's everything you need to know about implementing this in your workflow.

### Three methods for Salesforce lead matching

Clay provides [three distinct approaches](https://www.clay.com/university/guide/salesforce-integration-overview#enriching-data-with-salesforce) for Salesforce lead-to-account matching, ranging from simple to advanced:

1.  **Plain lookup record:** Best for scenarios with unique identifiers like LinkedIn profiles or Salesforce account IDs. This is the simplest and most straightforward method for Salesforce integration.
2.  **Lookup record +** [**Clay formulas**](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101)**:** More flexible approach that allows you to pull multiple Salesforce records and implement custom selection logic to choose the best match — see **Handling multiple results** below for step-by-step instructions.
3.  **Lookup records via SOQL**: The most sophisticated method, offering precise matching capabilities and advanced acceptance criteria for complex Salesforce use cases.

For more information on SFDC actions in Clay, consult our [CRM Enrichment course.](https://www.clay.com/university/lesson/clay-x-salesforce-actions-crm-enrichment)

### Handling multiple results with Lookup record + formulas

When a Lookup Record column shows **"N records found"** — meaning Salesforce matched more than one record for your search input — you can use a formula column and a Use AI column to automatically select the best match:

1.  **Add a formula column to slim down the results.** Reference the Lookup Record column in a formula to extract the key fields from each returned record (such as Name, Id, and Website) into a compact, readable format. Keeping the output concise makes the AI step faster and cheaper.

2.  **Add a Use AI column to identify the best match.** In the prompt, include the formula output alongside context from the current row — such as the contact's email address, company domain, or company name — then instruct the AI to return the Salesforce record Id of the best-matching entry. For example: *"These Salesforce accounts matched: /Formula Column. The contact's company domain is /Company Domain. Return the Salesforce Account Id of the best match."*

3.  **Add a run condition to the AI column so it only fires on rows with multiple matches.** Open the AI column → **Run settings** → **Only run if**, and enter a condition such as `/Lookup Record contains "records found"`. This evaluates to true only when multiple records were returned — a single Salesforce match shows the record name directly, not the phrase "records found" — so rows with one match or no match are skipped, saving AI credits.

**Tip:** For scenarios requiring exact filtering on multiple specific fields at once (for example, website domain AND country code), use [**Lookup records via SOQL**](salesforce-integration-overview.md) instead — it gives full query control without an AI disambiguation step.

### Additional Salesforce features

-   **Lead-to-contact conversion:** Leverage **`Convert lead`** action for seamless Salesforce lead management.
-   **Assignment rules:** Utilize round robin and weighted round robin actions for automated Salesforce lead assignment.
