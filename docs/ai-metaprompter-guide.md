---
title: Writing AI prompts in Clay
source_url: https://university.clay.com/docs/ai-metaprompter-guide
description: Create high-quality AI prompts in Clay so you can easily accomplish your goals.
last_synced: 2026-04-26T01:39:39.607Z
---

# Writing AI prompts in Clay

Create high-quality AI prompts in Clay so you can easily accomplish your goals.

For more information on how to use the **Use AI** feature, please visit [this doc](https://www.clay.com/university/lesson/use-ai-integration-overview).

Writing effective AI prompts in Clay requires understanding and practice. **Clay's AI capabilities allow you to extract, analyze, and enrich data by crafting clear, specific instructions**.

Whether you're using natural language prompts or the AI help tool, the key is to be precise about your desired outcome, data sources, and format requirements.

## Prompt structure

A reliable prompt format follows five sections: **CONTEXT**, **OBJECTIVE**, **STEPS**, **INPUTS**, and **OUTPUT**. Structuring your prompts this way helps the model understand what it's working with before it tries to produce a result.

```
**CONTEXT**
You are an AI that categorizes sales contacts based on their job function. You are given a person's LinkedIn profile URL.

**OBJECTIVE**
Visit the profile URL and identify the person's current or most recent job. Categorize them as one of: "customer success", "data or finance", or "inapplicable".

**STEPS**
1. Visit {{Profile URL}}
2. Find their current or most recent role
3. Map the role to the closest category
4. Return only the category

**INPUTS**
Profile URL: {{Profile URL}}

**OUTPUT**
Return only one of the following as a plain string: customer success, data or finance, inapplicable
```

### Reference columns throughout the prompt — not just in the inputs list

A common mistake is to list column references only at the bottom of the prompt in the **INPUTS** section, without using them in the **CONTEXT**, **OBJECTIVE**, or **STEPS** sections. When the model doesn't see how an input connects to the task it's performing, it may not use that data reliably — especially for rows where the values are less predictable.

Instead, weave your column references into each section where they're relevant:

-   **Good:** `Your job is to evaluate {{Company Name}}, a company in the {{Industry}} space with {{Employee Count}} employees.`
-   **Less effective:** Having the column reference appear only at the bottom as a bare list entry.

### Describe each input before referencing it

When listing inputs, don't just name the column — describe what it represents and what values it can have. This gives the model enough context to handle edge cases and blank values correctly.

-   **Good:** `Signal indicating no dedicated HR leader on file: {{Signal (No Top HR)}}. Possible values: "Trigger to Call" or blank (treat blank as not applicable).`
-   **Less effective:** `{{Signal (No Top HR)}}: "Trigger to Call" or blank`

The format `Description of what this is: {{Column Reference}}` consistently outperforms bare column references.

### Using the AI help tool

1.  While configuring the "Use AI" enrichment, click `Generate with prompt`**.**
2.  Enter your desired outcome in the `Task description` field, and the tool will generate a tailored prompt to help you achieve it.
3.  Verify that the dynamic prompt inputs are correctly linked to the appropriate columns.
    -   This step is crucial when you have multiple columns connected to the same endpoint (e.g., company domain).
4.  Preview your results by clicking on any enriched cell to view the generated details.
