---
title: AI column behaves strangely when generating content (wrong Use case)
description: Why a Use AI column set to Web research (Claygent) misbehaves on content tasks like drafting emails, and how switching to Create or modify content fixes it.
---

# AI column behaves strangely when generating content (wrong Use case)

A common reason a **Use AI** column "performs strangely" — wandering off-topic, returning odd results, or failing to finish — is that the **Use case** is set to **Web research (Claygent)** when the task is actually content generation, such as drafting a personalized email.

This is a configuration issue, not a problem with the AI or your prompt. Switching the Use case to **Create or modify content** resolves it.

## The short version

The **Use case** dropdown at the top of the **Configure** tab tells the column *how* to work, not just what to do:

-   **Web research (Claygent)** is built to browse the web as part of its process. It will attempt to scrape and analyze websites.
-   **Create or modify content** works only from your prompt and your table's data. It does **not** access the web.

If you're generating content (like emails) but left the Use case on **Web research (Claygent)**, the column tries to research the web anyway — which produces erratic output or an incomplete run. For content tasks, use **Create or modify content**.

## Why this happens

The two use cases run fundamentally different procedures.

**Web research (Claygent)** is designed to go out and scrape and analyze websites as part of answering. So when you point it at a writing task, it still tries to do web research — even when you don't need it. This happens whether or not you explicitly ask it to visit a page:

-   If a **domain or URL is present in the inputs** (for example, a `{{Domain}}` reference in your prompt), Claygent will try to visit it.
-   If your prompt **doesn't clearly direct that research**, the web step just layers confusing, irrelevant work on top of the writing task.

Either way, the result is a column that behaves strangely, goes off-topic, or can't complete the task cleanly — because it's spending effort on web research instead of simply writing what you asked for.

**Create or modify content** doesn't have this problem. It never touches the web — it writes directly from the prompt and the column values you provide, which is exactly what email and content generation need. That's why the same prompt works cleanly under this use case.

## How to resolve it

1.  Open the AI column and go to the **Configure** tab.
2.  At the top, open the **Use case** dropdown.
3.  Select **Create or modify content**.
4.  Re-run the affected rows.

To test the change before committing to a full re-run, select a few rows, right-click, and choose **Run [N] rows** to validate the output first.

## Choosing the right Use case

Use this rule of thumb:

| Your task | Use case |
| --- | --- |
| Draft, rewrite, summarize, classify, or clean data you already have | **Create or modify content** |
| Genuinely need the AI to read a website to answer | **Web research (Claygent)** |
| Generate images from text | **Image generation** |

**Note:** If a **Create or modify content** column needs website content, don't switch to Web research just for that — instead, add a **Scrape Website** column to pull the page text into a table column, then reference that column in your prompt with `/`. For multi-page or multi-step browsing, a dedicated **Claygent** agent column is the more reliable option. See [Use AI](use-ai-integration-overview.md) for details on each use case and model.

## Related

-   [Use AI](use-ai-integration-overview.md) — full overview of use cases, models, prompts, and outputs.
