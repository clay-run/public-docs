---
title: Writing AI prompts in Clay
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

## Adding examples to your prompt

For tasks that require a specific voice, format, or creative style — such as cold email opening lines, personalized icebreakers, or one-line summaries — **adding examples dramatically improves output consistency**. Examples show the model exactly what "good" looks like instead of leaving it to interpret your intent from instructions alone.

Add an `## Examples` section at the bottom of your prompt with two or three representative outputs:

```
**OUTPUT**
Write one opening sentence. Lowercase. 15–25 words. No punctuation at end.

## Examples

Good output: built a taco bell express inside a hospital, which is a move only someone running three concepts could pull off
Good output: running a ghost kitchen out of the back of a bar is something most operators wouldn't attempt

Bad output (too generic): you've built something impressive in the restaurant space
Bad output (uses a question): have you considered how your expansion strategy could benefit from outside capital?
```

**Why this works:**

-   Positive examples anchor the model to your exact tone and format
-   Negative (bad output) examples act as guardrails — showing the model what to avoid is more reliable than describing constraints in words alone
-   A fallback example for sparse data gives the model a concrete template when input signals are thin, instead of forcing it to improvise

**Input data quality matters too.** Prompt structure cannot compensate for missing or generic enrichment data. If the column your prompt references (like a news snippet, bio, or research field) is frequently empty or generic, output will be vague regardless of prompt quality. Before troubleshooting the prompt, verify the upstream enrichment is returning substantive data for your rows.

You can also add examples through the Clay UI without editing the prompt text directly: in the **Configure** tab of any Use AI column, click `Examples` → `Add examples`. See [Use AI](https://www.clay.com/university/lesson/use-ai-integration-overview) for details.

## Using the AI help tool

1.  While configuring the "Use AI" enrichment, click `Generate with prompt`**.**
2.  Enter your desired outcome in the `Task description` field, and the tool will generate a tailored prompt to help you achieve it.
3.  Verify that the dynamic prompt inputs are correctly linked to the appropriate columns.
    -   This step is crucial when you have multiple columns connected to the same endpoint (e.g., company domain).
4.  Preview your results by clicking on any enriched cell to view the generated details.
