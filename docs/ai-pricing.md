---
title: How AI is priced
source_url: https://university.clay.com/docs/ai-pricing
last_synced: 2026-04-26T01:39:39.981Z
upstream_hash: 7ebe8e16c1a2999794bf438260edf30b5b22077fbb031ad16a2441e29ab946dc
---

# How AI is priced

This guide explains how each works, which models they apply to, and how credits are calculated.

_Clay uses two pricing structures for AI models—fixed and variable—so you pay based on actual usage. This guide explains how each works, which models they apply to, and how credits are calculated._

## **Two pricing structures**

**Fixed AI pricing** charges a flat number of data credits per task. It applies to 80% of models in Clay, including all of Clay's own models (Neon, Helium, Argon). The cost is exact and known before you run.

**Variable AI pricing** charges data credits based on the actual cost of each run, with **0% markup**. It applies to 20% of models—the most advanced reasoning models available in Clay, typically used for sophisticated web-research tasks with multi-step reasoning—where the underlying compute cost can vary significantly from one prompt to the next. You'll see the exact cost per row in your Clay table once the run is completed. Rather than setting a flat rate high enough to cover the most expensive use cases—which would overcharge most users—variable pricing ensures each task is priced according to what it actually costs to run. This blended model of fixed and variable pricing results in customers paying less overall for AI in Clay.

You can always see which pricing structure applies when selecting a model in the product.**‍**

## **Select model pricing reference**

| Provider | Model | Content Generation | Web Research |
| --- | --- | --- | --- |
| Clay | Helium | — | 1 |
| Argon | — | 3 |
| OpenAI | GPT-4o | 1 | variable |
| GPT-4.1 | 1 | variable |
| GPT-5.1 | 2 | variable |
| GPT-5 Mini | 0.4 | 1 |
| GPT-5 Nano | 0.2 | 0.5 |
| o3 | 5 | variable |
| Anthropic | Claude 4.5 Haiku | 1 | variable |
| Claude 4.5 Sonnet | 1.5 | variable |
| Claude 4.6 Opus | 7.5 | variable |
| Gemini | 2.5 Pro | 3 | variable |
| 2.5 Flash | 0.5 | 1 |
| 2.5 Flash Lite | 0.5 | 1 |

_Costs are in data credits._

## **How variable pricing works**

**_Data credit formula:_** _Credit Charge = Actual LLM Cost ($) ÷ Workspace Cost Per Credit ($)_

The actual LLM cost is the cost charged by the AI provider of the model you've selected. Clay applies 0% markup on variable AI pricing for the most sophisticated reasoning models. Your cost per credit (CPC) is determined by your subscription plan.

**What happens during a run**

1.  **Withhold.** Clay withholds an estimated number of data credits upfront—based on the 75th percentile of past runs for that model—multiplied by the number of rows.
2.  **Execute.** The model processes your task.
3.  **Calculate.** Clay calculates the actual LLM cost for each row.
4.  **Reconcile.** The withheld amount is compared to the actual cost. Any surplus is refunded; any additional cost is deducted. You only pay for what was used.

Every AI prompt counts as **one action**. The variable component affects only the data credit cost of that action.

**Balance protection**

If your data credit balance reaches zero during a run, processing stops. You will never be charged beyond your available balance. Rows that haven't started will not run, and results from completed rows are retained.

## **Fixed vs. variable: a comparison**

The example below details a fixed vs variable AI model being run on 100 rows in Clay. The fixed rate model is priced at 1 credit per row. The variable rate model withholds 1 credit per row as an estimate, but after running the realized cost is only 0.8 credits.

|  | Fixed Pricing | Variable Pricing |
| --- | --- | --- |
| Starting balance | 100 credits | 100 credits |
| Start of run | Charges 100 credits | Withholds 100 credits |
| End of run | — | Refunds 20 credits |
| Ending balance | 0 credits | 20 credits |

In this scenario, the variable model's withholding mechanism protects both the customer and Clay from unexpected cost overruns—while returning unused credits at the end.

## **Using your own API keys**

You can always use your own API keys instead of Clay data credits. That said, many customers prefer Clay's built-in AI for two reasons:

-   **Model selection.** Clay gives you access to a broader set of models than any single provider.
-   **Speed.** Actual usage data shows that AI tasks run through Clay's APIs run up to 2× faster than tasks run through customers' own API keys because Clay has negotiated significantly higher rate limits than most customers have independently.

## **FAQs**

**How do I know if a model uses fixed or variable pricing?**

The product displays the pricing type when you select a model. Fixed-price models show a flat credit cost (e.g., `3/row`), while variable-price models show an estimate (e.g., ~2) with a note that the final charge depends on actual usage.

**Will I always know what a task will cost before I run it?**

For fixed-price models, yes—the cost shown is exact. For variable-price models, you'll see an estimate upfront. The final cost may differ, but credits are withheld before the run starts so there are no surprises to your balance.

**Could a variable-priced task cost significantly more than the estimate?**

In most cases, the final cost will be at or below the estimate. Complex, multi-step tasks can cost more, but these are a small minority of runs. Most customers pay less under variable pricing than they would under a flat rate for the same model.

Customers who are configuring complex, multi-step web research tasks may wish to run their prompt on 10 or 50 rows so they are able to see the credit charge for each row before running the prompt across their full table.

**What happens if I run out of data credits mid-run?**

Processing stops when your balance reaches zero. You won't be charged beyond your available credits. Rows that haven't started will not run; rows that completed successfully retain their results.

**Why not just use fixed pricing for everything?**

Advanced reasoning models have high cost variability from task to task. A fixed rate would need to be high enough to cover the most expensive use cases—overcharging the majority of users on simpler work. Variable pricing ensures every task is priced according to its actual cost.

**Does Clay charge a markup on variable AI pricing?**

No. Clay charges 0% markup on variable AI pricing for reasoning models. You pay exactly what Clay pays the AI provider, making this the most fair and customer-friendly pricing possible.
