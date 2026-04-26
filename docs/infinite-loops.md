---
title: Infinite loops
source_url: https://university.clay.com/docs/infinite-loops
last_synced: 2026-04-26T01:40:10.668Z
upstream_hash: cd123ac215921f7005c0ac84029e02aed39323bc3818ec07cf7a28aef37f391c
---

# Infinite loops

Learn about infinite loops and how to prevent/fix them.

An **infinite loop** occurs when a workflow or automation continuously triggers itself without stopping, creating a cycle that can consume credits, slow down your workspace, and disrupt your work.

An infinite loop happens when the output of an action becomes the input that triggers the same action again, creating a never-ending cycle. In workflow automation, this typically occurs when:

-   Action A triggers Action B
-   Action B's result triggers Action A again
-   The cycle repeats indefinitely

**Warning:** Infinite loops can rapidly consume credits and may require intervention to stop. Always test workflows carefully before deploying them at scale.

## Why infinite loops occur in Clay

Infinite loops in Clay typically happen in these scenarios:

**1\. Webhook-triggered table updates**

When a table sends data to a webhook, and that webhook writes back to the same table, creating a continuous loop.

**2\. Cross-table circular references**

When Table A enriches data and writes to Table B, and Table B's automation writes back to Table A, triggering the cycle again.

**3\. Auto-enrichment recursion**

When an enrichment column triggers based on a field that the enrichment itself updates, causing it to re-run continuously.

**4\. API integrations with bidirectional sync**

When Clay sends data to an external system, and that system has a webhook configured to send updates back to Clay, which then triggers another send.

## Common Clay examples

### Example 1: Webhook loop

**The scenario:** A table triggers a webhook on new rows, which sends data back to Clay via API, creating or updating rows and retriggering the webhook.

**The loop:**

1.  New row → Webhook fires
2.  External system processes → Sends to Clay
3.  Clay receives data → Row added/updated
4.  **Repeat step 1**

**How to fix it:**

-   Use a status column (e.g., "Not Sent", "Sent", "Completed")
-   Only trigger webhook when status is "Not Sent"
-   Update status to "Sent" immediately after webhook fires
-   Configure external system to NOT write back to the triggering table

### Example 2: Cross-table enrichment loop

**The scenario:** Table A enriches contacts and writes to Table B. Table B enriches company data and writes back to Table A, creating a cycle.

**The loop:**

1.  Table A enriches → Writes to Table B
2.  Table B processes → Enriches → Updates Table A
3.  Table A update triggers enrichment → Writes to Table B
4.  **Repeat step 2**

**How to fix it:**

-   Design unidirectional data flow (no circular references)
-   Use conditional logic to only run enrichments when fields are empty
-   Implement a "processed" flag to prevent re-triggering

### Example 3: Auto-run enrichment on its own output

**The scenario:** An enrichment column auto-runs when a field changes, but the enrichment updates that same field, causing continuous re-runs.

**The loop:**

1.  Field X updates → Enrichment runs
2.  Enrichment modifies Field X (or trigger field)
3.  Field change detected → Enrichment runs again
4.  **Repeat step 2**

**How to fix it:**

-   Set enrichments to manual or specific triggers only
-   Use a separate trigger field that the enrichment doesn't update
-   Add conditional logic: "Only run if \[processed field\] is empty"

### How to identify an infinite loop

**Signs you're in a loop:**

-   Credits depleting rapidly without clear cause
-   Tables continuously showing "running" enrichments
-   Duplicate rows appearing repeatedly
-   Same enrichment columns running multiple times on the same row
-   Webhook logs showing repeated calls in quick succession

**Diagnostic steps:**

1.  **Check your table activity** – Look for patterns of repeated enrichments on the same rows
2.  **Review webhook configurations** – Identify any bidirectional webhook setups
3.  **Examine column dependencies** – Map out which columns trigger which enrichments
4.  **Check external integrations** – Review if external systems are writing back to Clay

## How to fix and prevent infinite loops

### Immediate fixes:

1.  **Pause or disable the triggering automation** – Turn off auto-run on suspect enrichment columns
2.  **Stop webhook deliveries** – Temporarily disable webhook integrations
3.  **Use filters to break the cycle** – Add conditions that prevent re-triggering
4.  **Archive or delete problem rows** – If specific rows are looping, remove them

## Prevention strategies:

-   **Use status/flag columns**
    -   Create a column that tracks whether a row has been processed. Only trigger actions on unprocessed rows.

`IF(Status = "Not Processed", [run enrichment], [skip])   `

-   **Implement one-way data flows**
    -   Design your workflow so data flows in a single direction. Avoid circular references between tables.

`Source → Table A → Table B → Destination   (No writes back from B to A)   `

-   **Add conditional triggers**
    -   Only run enrichments when specific conditions are met, not on every change.

`Auto-run when: Company Name is not empty AND Enriched is empty   `

-   **Use manual run for sensitive operations**
    -   For enrichments that could create loops, disable auto-run and trigger them manually or via API.
-   **Separate trigger fields from output fields**
    -   Don't let an enrichment modify the field that triggers it.
-   **Test with small batches first**
    -   When setting up new automations, test with 5-10 rows before scaling up.

### Best practices for loop-free workflows

1.  **Map your workflow before building** – Diagram how data flows through your tables and integrations
2.  **Use clear naming conventions** – Label status columns consistently (e.g., "Enrichment\_Complete", "Webhook\_Sent")
3.  **Set up monitoring** – Regularly check credit usage and enrichment run counts
4.  **Document trigger conditions** – Keep notes on what triggers each automation
5.  **Leverage pass-through patterns** – For high-volume data that doesn't need storage, use auto-delete to prevent accumulation

### Getting help

If you're experiencing an infinite loop that you can't resolve:

1.  Pause all automations in the affected table(s).
2.  Document the loop pattern (which columns/webhooks are involved).
3.  Reach out to Clay support with details about your workflow structure.

The support team can help identify the root cause and suggest architectural changes to prevent future loops.
