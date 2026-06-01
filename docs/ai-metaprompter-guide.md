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
You are an AI that categorizes sales contacts based on their job function.
You will be given a LinkedIn profile URL to visit.

**OBJECTIVE**
Visit the profile URL and identify the person's current or most recent job.
Categorize them as one of: "customer success", "data or finance", or "inapplicable".

**STEPS**
1. Visit the profile URL from the inputs
2. Find their current or most recent role
3. Map the role to the closest category
4. Return only the category

**INPUTS**
Profile URL: {{Profile URL}}

**OUTPUT**
Return only one of the following as a plain string: customer success, data or finance, inapplicable
```

### Keep `{{variable}}` references in the INPUTS section only

**The `{{variable}}` syntax must appear only in the INPUTS section — never duplicated in CONTEXT, OBJECTIVE, or STEPS.** Clay substitutes the column value at run time, and if the same variable appears in multiple sections, the column's full content is injected multiple times. For columns with large values (like transcripts, scraped pages, or long text), this significantly increases token cost and can hit limits.

Instead, *describe* your inputs by name in the earlier sections, and reserve `{{variable}}` references exclusively for the INPUTS block:

-   **Good:** `You will be given a company name and three HR signal values.` _(in CONTEXT)_ ... `Company name: {{Company Name}}` _(in INPUTS)_
-   **Incorrect:** `Evaluate {{Company Name}} — a company with signals {{Signal (No Top HR)}}...` _(in CONTEXT, where `{{}}` causes values to be injected twice)_

### Describe each input before referencing it

When listing inputs in the INPUTS section, don't just name the column — describe what it represents and what values it can have. This gives the model enough context to handle edge cases and blank values correctly.

-   **Good:** `Signal indicating no dedicated HR leader on file: {{Signal (No Top HR)}}. Possible values: "Trigger to Call" or blank (treat blank as not applicable).`
-   **Less effective:** `{{Signal (No Top HR)}}: "Trigger to Call" or blank`

The format `Description of what this is: {{Column Reference}}` consistently outperforms bare column references in the INPUTS section.

## Generating varied, personalized content

If AI-generated messages across your table look too similar to each other, the fix is usually in the prompt structure — not the data.

**Use guidelines instead of strict templates.** Providing many full email examples in your prompt anchors the model to those examples' structure and phrasing. It copies the format rather than personalizing for each lead. Instead, describe the *style and voice* you want in plain language: `"conversational, direct, no fluff, 3 sentences max"`. This gives the model room to personalize based on each row's unique data.

**Keep examples to 1–2 at most.** If you want to illustrate tone, include one or two short examples — enough to convey the voice, not so many that the model treats them as rigid templates. You can add examples in the **Configure** tab → **Examples** section of a Use AI column.

**Feed in more lead-specific data.** Varied output comes from varied input. The more distinct data per row — job title, a recent LinkedIn post, a specific company news item, an identified pain point — the more each generated message will differ. If every row has the same inputs, the outputs will converge regardless of the prompt.

**Split the message across multiple AI columns.** Rather than generating an entire email in one prompt, use separate AI columns for each section: one for the opening line, one for the value proposition, one for the call to action. Each focused prompt produces sharper, more targeted results. Combine the outputs into a final column using a formula, which costs 0 credits.

## Using the AI help tool

1.  While configuring the "Use AI" enrichment, click `Generate with prompt`**.**
2.  Enter your desired outcome in the `Task description` field, and the tool will generate a tailored prompt to help you achieve it.
3.  Verify that the dynamic prompt inputs are correctly linked to the appropriate columns.
    -   This step is crucial when you have multiple columns connected to the same endpoint (e.g., company domain).
4.  Preview your results by clicking on any enriched cell to view the generated details.
