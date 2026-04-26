---
title: Actions & Data Credits
source_url: https://university.clay.com/docs/actions-data-credits
last_synced: 2026-04-26T01:39:38.626Z
upstream_hash: cd12f235935b9ccb524e8f8b4c5bc296d4e2cbc26ce34181c2bc90f2ff35b528
---

# Actions & Data Credits

Learn about credits, the virtual currency system used for running actions in Clay.

Clay uses two separate metrics to track your usage: **Actions** and **Data Credits**.

-   **Actions** measure the orchestration you do in Clay: enriching data, running AI research, and sending data to other tools. Each Action costs a few tenths of a penny.
-   **Data Credits** are used to buy data or AI from 3rd party vendors in Clay's data marketplace—costs vary by data type. Each Data Credit costs a few pennies.

This separation gives you transparency and control—you know exactly what you're paying for.

## Quick comparison

|  | Actions | Data credits |
| --- | --- | --- |
| What it measures | Platform usage capacity | Data marketplace purchases |
| Cost per enrichment | Always 1 action | Varies (0.5–10+ credits based on data type) |
| How to get more | Upgrade action capacity tier | Upgrade tier OR purchase one-time top-up |
| Rollover | No | Yes (up to 2× monthly limit) |

## How Actions and Data Credits work together

| Activity | Actions | Data credits |
| --- | --- | --- |
| Sourcing accounts and contacts | No | Yes (unless accessing free data or using your own API keys) |
| Importing 1st party data into Clay | No | No |
| Enriching accounts and contacts with net-new data (including signals) | 1 per enrichment | Yes (unless accessing free data or using your own API keys) |
| Transforming data within Clay | No | No |
| Using AI | 1 per AI run | Yes (unless using your own API keys) |
| Exporting and executing GTM tasks | 1 per record | No |

## Understanding Actions

### What are Actions?

Actions measure when you use Clay to either enrich accounts/contacts with net-new data (e.g., enrichments from Clay's data marketplace, AI web research, signals) or execute GTM work (e.g., send emails, sync to CRM, export ads audiences, write copy with AI). Each record enriched or exported counts as 1 Action—regardless of data source or provider.

### What consumes Actions?

Features that use an Action:

-   Each enrichment from any provider (e.g., "Find email via Hunter").
-   Using your own API keys (still counts as platform usage).
-   AI uses
-   Signals
-   Executing GTM work: sending emails, posting to Slack, generating Notion briefs.
    -   **Clay sequencer**: 1 Action per lead added to campaign (not per email sent).
    -   **External sequencer**: 1 Action per record exported to the external sequencer.
-   CRM exports and syncs (Salesforce, HubSpot, etc.).
-   Data warehouse exports and syncs.
-   HTTP API calls.
-   Ads audience exports (e.g., LinkedIn, Facebook).

**Features that don't use an Action:**

-   Sourcing lists of accounts or contacts (e.g., Find People returns 100 contacts).
-   CRM imports (bringing data into Clay from your CRM).
-   Data warehouse imports (bringing data into Clay from your warehouse).
-   Webhook imports.
-   Clay formulas and filters.
-   Manual data entry.
-   Using formulas for scoring and normalization.
-   Sculptor.
-   Creating audiences (only the export counts).

### How many Actions do I need?

Your Actions capacity is determined by your plan tier. Plan tiers are designed so 90% of customers do not hit the limit of their Actions capacity.

| Plan | Actions/month | Best for |
| --- | --- | --- |
| Launch | 15,000 | Enriching ~10,000 records/year |
| Growth | 40,000 | Enriching ~50,000 records/year |
| Enterprise | 100,000+ | Enriching millions of records/year |

### How to get more Actions

**Upgrade your plan tier** in `Settings` → `Plans & billing`.

Actions cannot be purchased as one-time top-ups because they represent fixed platform capacity tied to your plan's tier.

## Understanding Data Credits

### What are Data Credits?

Clay connects to 150+ data and AI providers. When you purchase data from these providers through Clay's marketplace, you spend Data Credits.

**Think of Data Credits as:**

-   API call credits for data enrichments or AI use.
-   A currency for buying data from the marketplace.
-   The "fuel" that powers enrichments (when not using your own keys).

### Using your own API keys

If you already subscribe to data providers (ZoomInfo, Apollo, Clearbit, etc.) or AI providers (Anthropic, Claude, ChatGPT), connecting your API keys to Clay will eliminate the **Data Credit** cost. Note that an Action will still be consumed.

When you use your own external API key in Clay, the AI usage and costs are billed directly by that external provider — not through Clay credits. To track your API spending, you'll need to check your console or dashboard in that AI provider's platform. Clay will only show the Actions used (our orchestration layer), but not the AI token costs themselves.

### How many Data Credits do I need?

Each fully enriched record typically costs **6–20 Data Credits**, depending on:

-   The data types you enrich (emails are cheap, phone numbers are expensive).
-   How many of your own API keys you use.
-   Whether you're using waterfalls with multiple providers.

‍**General guidelines:**

| Plan | Data Credits/month | Best for |
| --- | --- | --- |
| Launch | 2,500–10,000 | ~1,000 records/month |
| Growth | 6,000–100,000 | 1,000–10,000 records/month |
| Enterprise | 100,000+ | 10,000+ records/month |

**Note:** The more API keys you connect, the fewer Data Credits you'll need.

### Example: Data Credits in practice

**Scenario:** You want to enrich 100 contacts with LinkedIn profiles and emails.

**Using Clay's data marketplace:**

1.  Find 100 people (Clay database) → **0 Data Credits**
2.  Enrich LinkedIn profiles → **50 Data Credits** (0.5 per profile)
3.  Find emails (90% success) → **45 Data Credits** (0.5 per email × 90)
4.  Validate emails (90% success) → **0 Data Credits** (select validator providers are free in Clay under new pricing)

**Total Data Credits consumed:** 95

**Using your own email API key for steps 3–4:**

-   Total Data Credits consumed: **50** (just the LinkedIn enrichments)
-   **You saved 45 Data Credits** by using your own key

### How to get more Data Credits

Two options:

**1\. Upgrade your Data Credits tier** (recommended)

-   Go to `Settings` → `Plans & billing`.
-   Select a higher Data Credits tier.
-   No premium charged.

**2\. One-time top-up**

-   Available for emergency needs during your billing cycle.
-   **30% premium** applies.
-   Subject to rollover limits.

### Data Credits for AI

Data Credit pricing varies for AI models in [Use AI](https://www.clay.com/university/guide/use-ai-integration-overview), with rates determined by which model you select. Find out more in [AI pricing](https://university.clay.com/docs/ai-pricing) doc.

-   Data Credit costs are based on prompt and token usage.
-   You can control spending by setting custom budgets for each run.

## Action and Data Credit usage

To see detailed Data Credit consumption across your workspace, workbooks, and tables, visit the **credit usage** dashboard:

1.  Click your account name in the corner
2.  Go to `Settings` → `Credit usage`.

For a complete guide on tracking and analyzing your Data Credit spend, see [this doc](https://www.clay.com/university/guide/credit-usage).

### Workbook credit limits (Enterprise only)

_This feature is for users on the Enterprise Plan._

Admins can set **Data Credit spend limits** for individual workbooks to control and monitor Data Credit usage at the workbook level.

**How to enable workbook credit limits:**

1.  Open your workbook. In the settings panel, under `Credit spend limit`, click `Manage`.
2.  Toggle `Enabled credit spend limit` and add a number to `Workbook limit`.
3.  Click `Save changes`.

Once enabled, all Actions run within that workbook will contribute to the workbook's Data Credit spend. When the limit is reached, you'll see an error message preventing further Actions from running.

**Note:** Only workspace admins can modify workbook Data Credit limits. Editors and Viewers cannot manage Data Credit limits, even if they have editing access to the workbook.

## Rollover Data Credits

### Actions: No rollover

Actions represent your fixed monthly capacity. Unused Actions expire at the end of each billing cycle.

**Why no rollover?** Each plan tier is designed with sufficient capacity for typical use cases at that level. If you consistently hit limits, upgrade to the next tier.

### Data Credits: Yes, with limits

If you are on a **monthly plan**, unused Data Credits will roll over and accumulate in your account. The maximum accumulation is capped at **2× your plan's monthly credit limit**.

-   For example, if your plan includes 50,000 credits per month, your maximum balance would be 100,000.
-   If you cancel or downgrade, you can use any excess Data Credits until your current billing cycle ends. After the billing cycle ends, your balance will be reduced to the **Data Credit rollover limit** of your new plan.

If you are on an **annual plan**, you are eligible for a **15% Data Credit rollover** of unused Data Credits, provided you renew on the same or a higher-tier plan.

_Note: Your rollover and renewal happen on the same day and at the same time you originally subscribed (this timestamp is now shown in your billing details). Processing may take a few hours after that timestamp, so there can be a delay before you see Data Credits updated._

## Managing your plan and credits

You can adjust your Clay plan, Actions, and Data Credits at any time to match your usage needs. For complete details on plan features, pricing, and billing management, see [Plans & billing](https://www.notion.so/Plans-billing-1537e66eb014807e86a3e586aeb7c164?pvs=21).

### Upgrade your plan or add more credits

If you need ongoing increases in capacity:

1.  Go to `Settings` → `Plans & Billing`.
2.  Click `Change plan` to upgrade your plan tier, or adjust your Actions and Data Credits limits.
3.  Select the higher tier or credit amount that fits your needs.
4.  Click `Upgrade` to confirm.

Your new plan or credit limits will activate immediately, and any applicable charges will be applied to your billing cycle.

### Purchase one-time Data Credit top-ups

For emergency Data Credit needs during your billing cycle (not available for Actions):

1.  Go to `Settings` → `Usage`.
2.  Click `Add one-time data credits`.
3.  Select the amount you need (subject to rollover limits).
4.  Confirm your purchase.

**Note:** One-time top-ups have a **30% premium** and are subject to Data Credit rollover limits. For regular needs, upgrading your Data Credits tier is more cost-effective.

### Downgrade or cancel your plan

To downgrade your Clay workspace plan:

1.  Click your profile picture in the top-right corner and select `Settings`.
2.  Navigate to `Plans & billing` and click `Change plan`.
3.  Choose the plan you'd like to downgrade to and confirm your selection.

**If you downgrade:**

-   Your account remains active on a lower-tier or free plan.
-   All of your data—including tables, flows, and configurations—stays intact.
-   You'll have limited access to features based on your new plan's capabilities.
-   You can upgrade again at any time to restore full access.

**If you cancel fully:**

-   After a full cancellation, your workspace transitions to a free plan temporarily.
-   Your data remains stored, but long-term retention isn't guaranteed after extended inactivity.
-   To ensure your data is preserved, we recommend downgrading instead of fully canceling.

**During your current billing cycle:**

-   Your Data Credit balance remains until the cycle ends.
-   You can use excess Data Credits.

**After your billing cycle ends:**

-   Your balance is capped at 2× the new plan's monthly Data Credit limit.
-   Your data remains intact.
-   Features are limited to the new plan's capabilities.

## Cost optimization tips

### Use your own API keys

Connect your existing data provider keys (ZoomInfo, Apollo, Clearbit, etc.) to save 50–80% on Data Credits while still consuming 1 Action per enrichment.

### Filter before enriching

Narrow down your dataset to only relevant records before running enrichments to avoid wasting Actions and Data Credits on data you won't use.

### Use conditional logic

Set up enrichments to run only when a field is empty, data is outdated, or a confidence score is low to avoid re-enriching data you already have.

### Test on small batches first

Run new workflows on 10–20 records to validate results before scaling to avoid wasting Data Credits on failed experiments.

## FAQs

### What's the difference between Actions and Data Credits?

Actions measure platform work (what you do). Data Credits measure data purchases (what you buy). Every enrichment typically consumes both—1 Action for the platform work, plus variable Data Credits for the data itself.

### Why do Data Credits cost different amounts?

Unlike Actions (always 1 per enrichment), Data Credits reflect the real-world value of each data point. You'll see the exact cost displayed next to each enrichment option in the product.

### Why do I pay Actions even when using my own API key?

Actions represent the platform orchestration Clay performs—ingesting, storing, and routing your data. Even with your own API keys, Clay is doing work to integrate that data into your workflows.

### What happens if I run out of Data Credits but not Actions?

You can either:

1.  Upgrade your Data Credits tier (no premium).
2.  Purchase a one-time top-up (30% premium).

You don't need to change your Actions tier.

### What happens if I run out of Actions but not Data Credits?

You must upgrade to a higher plan tier. Actions cannot be topped up separately because they're tied to your plan's capacity and features.

### Why can't I top up Actions?

Actions represent fixed platform capacity tied to your plan tier's features and limits. To get more Actions, you must upgrade to a higher plan tier. Data Credits, however, are consumption-based and can be purchased as one-time top-ups or by upgrading your Data Credits tier.

### Do unused Data Credits or Actions roll over?

Actions reset each billing cycle and don't roll over, since they reflect the platform capacity your plan includes. Each plan includes enough Actions to cover 90% of customer usage, and if you need more, you can increase your Action tier.

Data Credits work more like a currency and do roll over. On Launch and Growth plans, unused credits can accumulate up to 2x your monthly credit amount (e.g., a 10,000 credit plan can bank up to 20,000 total). Enterprise customers can roll over up to 15% of their prior year's purchased credits, provided they renew at an equal or higher commitment.

### How do I estimate costs before running an enrichment?

The enrichment panel shows costs before you run:

-   Actions: Always 1 per result.
-   Data Credits: Displayed next to each enrichment option.

For complex workflows, run a small test batch (10–50 records) to understand full costs.

### What happens to my Data Credits if I get invalid data?

If a provider refunds us due to invalid data, we'll refund those Data Credits back to you.

### How long does it take for Data Credits to renew?

When your plan renews, Data Credits may take 1–2 hours to appear due to transaction processing times. This is based on your original billing timestamp.

### Why are Data Credits being deducted unexpectedly?

Common causes:

-   **Actions stopped midway:** Already-sent requests still consume Data Credits.
-   `Auto-Update` enabled: Automatic refreshes trigger enrichments.
-   **AI columns:** Every row processed incurs a cost.
-   **Duplicate enrichments:** Re-running columns triggers new usage.

**Prevention tips:**

-   Turn off `Auto-Update` when not needed.
-   Pause AI columns that aren't providing value.
-   Check table settings before re-running enrichments.

### What happens when I downgrade my plan?

**During your current billing cycle:**

-   Your Data Credit balance remains until the cycle ends.
-   You can use excess Data Credits.

**After your billing cycle ends:**

-   Your balance is capped at 2× the new plan's monthly Data Credit limit.
-   Your data remains intact.
-   Features are limited to the new plan's capabilities.

### **I have a trial, when do the Data Credits expire?**

Data Credits expire when your trial ends or when a free workspace refreshes at the end of the monthly cycle. Only 100 Data Credits will be rolled over.

### Does CSV export consume an Action?

No. Exporting data to CSV does not consume an Action or any Data Credits. CSV export is a simple data download operation and does not count as platform usage or GTM execution.
