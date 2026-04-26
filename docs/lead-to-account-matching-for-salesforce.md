---
title: Lead-to-account matching for Salesforce
source_url: https://university.clay.com/docs/lead-to-account-matching-for-salesforce
description: Connect Salesforce leads with their corresponding Salesforce accounts.
last_synced: 2026-04-26T01:40:13.950Z
upstream_hash: d86f29130400b2875ff5a02d7dfa65cede6b8f4eb4d75653b6d031a0d3ab374a
---

# Lead-to-account matching for Salesforce

Connect Salesforce leads with their corresponding Salesforce accounts.

Clay offers powerful lead-to-account matching capabilities that help you efficiently connect Salesforce leads with their corresponding Salesforce accounts. Here's everything you need to know about implementing this in your workflow.

### Three methods for Salesforce lead matching

Clay provides [three distinct approaches](https://www.clay.com/university/guide/salesforce-integration-overview#enriching-data-with-salesforce) for Salesforce lead-to-account matching, ranging from simple to advanced:

1.  **Plain lookup record:** Best for scenarios with unique identifiers like LinkedIn profiles or Salesforce account IDs. This is the simplest and most straightforward method for Salesforce integration.
2.  **Lookup record +** [**Clay formulas**](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101)**:** More flexible approach that allows you to pull multiple Salesforce records and implement custom selection logic to choose the best match.
3.  **Lookup records via SOQL**: The most sophisticated method, offering precise matching capabilities and advanced acceptance criteria for complex Salesforce use cases.

For more information on SFDC actions in Clay, consult our [CRM Enrichment course.](https://www.clay.com/university/lesson/clay-x-salesforce-actions-crm-enrichment)

### Additional Salesforce features

-   **Lead-to-contact conversion:** Leverage **`Convert lead`** action for seamless Salesforce lead management.
-   **Assignment rules:** Utilize round robin and weighted round robin actions for automated Salesforce lead assignment.
