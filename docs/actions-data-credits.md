---
title: Actions & Data Credits
description: Learn about credits, the virtual currency system used for running
  actions in Clay.
last_synced: 2026-05-11T17:47:40.000Z
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
-   CRM imports and lookup operations (reading data from your CRM into Clay, including **Lookup Record** actions like `Salesforce > Lookup Record`).
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

**Upgrade your action capacity tier** in `Settings` → `Plan & billing`.

Actions cannot be purchased as one-time top-ups because they represent fixed platform capacity tied to your action tier.

## Understanding Data Credits

### What are Data Credits?

Clay connects to 150+ data and AI providers. When you purchase data from these providers through Clay's marketplace, you spend Data Credits.

**Think of Data Credits as:**

-   API call credits for data enrichments or AI use.
-   A currency for buying data from the marketplace.
-   The "fuel" that powers enrichments (when not using your own keys).

### Using your own API keys

If you already subscribe to data providers (ZoomInfo, Apollo, Clearbit, etc.) or AI providers (Anthropic, Claude, ChatGPT), connecting your API keys to Clay will eliminate the **Data Credit** cost. Note that an Action will still be consumed.

When you use your own external API key in Clay, the AI usage and costs are billed directly by that external provider — not through Clay credits. Clay does not track the dollar amounts charged by the provider — to see how much you've spent with Anthropic, OpenAI, or another provider, go directly to your console or dashboard in that provider's platform. What Clay does show is how many **Actions** and Data Credits your keys consumed: go to **Settings → Usage → Integrations tab** and expand any integration to see a breakdown by individual API key (Clay-managed or personal).

#### Clay-managed providers vs. accounts you must bring

Not all providers in Clay's marketplace can be accessed via Clay Data Credits. There are two types:

-   **Clay-managed key**: Clay holds a shared key for the provider, so you can run enrichments directly using Data Credits—no personal subscription required. When setting up these enrichments, you'll see a **"Clay provided key"** option in the account selector. You can also connect your own key to avoid spending Data Credits. Examples: SMARTe, BetterContact, FullEnrich, ContactOut.

-   **Bring Your Own Account (BYOA)**: Clay does not hold a managed key for these providers. You must have your own subscription or API credentials—there is no Clay Data Credit option. The account selector shows only **"Add account"** with no Clay-provided fallback. Example: ZoomInfo.

**Tip for mobile number enrichment without a provider subscription:** The built-in **Mobile Phone Waterfall** enrichment routes through multiple Clay-managed providers in sequence using your Data Credits—no individual provider account needed.

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

**1\\. Upgrade your Data Credits tier** (recommended)

-   Go to `Settings` → `Plan & billing`.
-   Select a higher Data Credits tier.
-   No premium charged.

**2\\. One-time top-up**

-   Requires a paid plan — not available on the free plan.
-   Go to `Settings` → `Usage` and click `Add one-time data credits`.
-   Available for emergency needs during your billing cycle.
-   **30% premium** applies (on modern plans; **50% premium** on legacy plans).
-   Subject to the 2× rollover cap: at renewal, your total balance cannot exceed 2× your monthly credit limit, and any credits above that cap — including purchased top-ups — are dropped.

### Data Credits for AI

Data Credit pricing varies for AI models in [Use AI](https://www.clay.com/university/guide/use-ai-integration-overview), with rates determined by which model you select. Find out more in [AI pricing](https://university.clay.com/docs/ai-pricing) doc.

-   Data Credit costs are based on prompt and token usage.
-   You can control spending by setting custom budgets for each run.

## Action and Data Credit usage

To see detailed Data Credit consumption across your workspace, workbooks, and tables, visit the **credit usage** dashboard:

1.  Click your account name in the corner
2.  Go to `Settings` → `Usage`.

For a complete guide on tracking and analyzing your Data Credit spend, see [this doc](https://www.clay.com/university/guide/credit-usage).

### Workbook credit limits (Enterprise only)

_This feature is for users on the Enterprise Plan._

Admins can set **Data Credit spend limits** for individual workbooks to control and monitor Data Credit usage at the workbook level. Admins can also set a **workspace default limit** — a credit cap that every new workbook automatically inherits upon creation — from `Settings` → `Usage` → `Workbook limits` tab.

**How to enable workbook credit limits:**

1.  Open your workbook. In the settings panel, under `Credit spend limit`, click `Manage`.
2.  Toggle `Enabled credit spend limit` and add a number to `Workbook limit`.
3.  Click `Save changes`.

Once enabled, all Actions run within that workbook will contribute to the workbook's Data Credit spend. When the limit is reached, you'll see an error message preventing further Actions from running.

**Note:** Only workspace admins can modify workbook Data Credit limits. Editors and Viewers cannot manage Data Credit limits, even if they have editing access to the workbook.

For complete documentation on credit spend limits—including default workspace limits, notifications, and behavior when limits are reached—see the [Credit spend limits FAQ](https://university.clay.com/docs/credit-spend-limits-faq).

### Credit budgets (Enterprise, open beta)

_Credit budgets are currently in open beta for Enterprise Plan workspaces._

Credit budgets let admins create named spending pools and assign them to users or groups, so each team or cost center's Data Credit usage is tracked and governed independently. Unlike workbook credit limits—which cap a single workbook's spend—a budget spans multiple workbooks and users, making it well-suited for team- or department-level cost allocation.

**How to access:** `Settings` → `Budgets`.

**How credit budgets work:**

1.  An admin creates a named budget (e.g., "Marketing") and sets a Data Credit limit for it.
2.  The admin grants budget access to user groups or individual members.
3.  Users assign their workbooks to a budget. Any Data Credits consumed by those workbooks count against the assigned budget's limit.

When a budget's limit is reached, credit-consuming actions are blocked for all workbooks assigned to that budget. Workbooks remain fully editable, but enrichment runs cannot start until an admin increases the limit or resets the budget.

**Key behaviors:**

-   **Data Credits only.** Budgets track Data Credit spend only, not Actions.
-   **Spending caps, not reserved credits.** The sum of all budget limits can exceed your total workspace credit balance—you don't need to divide your full credit pool upfront.
-   **No automatic reset.** Budget balances count down continuously; an admin must manually reset them.
-   **Independent from workbook limits.** If a workbook has both a workbook credit limit and a budget assigned, credits count against each independently.
-   **Homepage filter.** Filter your workbooks by budget from the Clay homepage to see spend by team or initiative.
-   **Bulk assignment.** Admins can assign multiple workbooks to a budget at once.
-   **Email alerts.** Receive email notifications when a budget's usage approaches or reaches its limit.

## Rollover Data Credits

### Actions: No rollover

Actions represent your fixed monthly capacity. Unused Actions expire at the end of each billing cycle.

**Why no rollover?** Each plan tier is designed with sufficient capacity for typical use cases at that level. If you consistently hit limits, upgrade to the next tier.

### Data Credits: Yes, with limits

If you are on a **monthly plan**, unused Data Credits will roll over and accumulate in your account. The maximum accumulation is capped at **2× your plan's monthly credit limit**. This cap is enforced at every renewal: when new monthly credits are added, your **total balance** (existing credits + new credits) cannot exceed 2× your monthly limit. Any credits that would push you over the cap are dropped.

-   For example, if your plan includes 50,000 credits per month, your maximum balance is 100,000. If you already have 82,000 credits when your plan renews, your balance becomes 100,000 — not 132,000. The 32,000 excess is dropped.
-   If you cancel or downgrade, you can use any excess Data Credits until your current billing cycle ends. After the billing cycle ends, your balance will be reduced to the **Data Credit rollover limit** of your new plan.

If you are on an **annual plan**, you are eligible for a **15% Data Credit rollover** of unused Data Credits, provided you renew on the same or a higher-tier plan.

_Note: Your rollover and renewal happen on the same day and at the same time you originally subscribed (this timestamp is now shown in your billing details). Credits are updated via a payment-processor webhook and typically appear within a few minutes of that timestamp._

## Managing your plan and credits

You can adjust your Clay plan, Actions, and Data Credits at any time to match your usage needs. For complete details on plan features, pricing, and billing management, see [Plans & billing](https://www.notion.so/Plans-billing-1537e66eb014807e86a3e586aeb7c164?pvs=21).

### Upgrade your plan or add more credits

If you need ongoing increases in capacity:

1.  Go to `Settings` → `Plan & billing`.
2.  Click `Upgrade` (on a free plan) or `Switch plan` (on a paid plan) to upgrade your plan tier, or adjust your Actions and Data Credits limits.
3.  Select the higher tier or credit amount that fits your needs.
4.  Click `Upgrade` to confirm.

Your new plan or credit limits will activate immediately, and any applicable charges will be applied to your billing cycle.

### Purchase one-time Data Credit top-ups

One-time top-ups are only available on paid plans. If you are on the free plan, you cannot purchase additional Data Credits — upgrade to a paid plan to access this feature.

For emergency Data Credit needs during your billing cycle (not available for Actions):

1.  Go to `Settings` → `Usage`.
2.  Click `Add one-time data credits`.
3.  Select the amount you need (subject to rollover limits).
4.  Confirm your purchase.

Credits are added to your balance immediately upon purchase. Top-ups do not change your plan or billing cycle — your existing subscription and renewal date are unaffected.

**Note:** One-time top-ups have a **30% premium** on modern plans (**50% premium** on legacy plans). Top-up credits are subject to the 2× rollover cap: at your next renewal, your total balance cannot exceed 2× your monthly credit limit, and any credits above that cap are dropped — including credits you purchased. For example, on a plan with 2,500 credits/month, your maximum balance at renewal is 5,000; if you buy a 15,000-credit top-up and don't spend it all before renewal, only up to 5,000 credits carry over. Check your current balance and upcoming renewal date before purchasing a large top-up. For regular needs, upgrading your Data Credits tier is more cost-effective.

### Downgrade or cancel your plan

To downgrade your Clay workspace plan:

1.  Click your profile picture in the top-right corner and select `Settings`.
2.  Navigate to `Plan & billing` and click `Switch plan` (or `Upgrade` if you're currently on a free plan).
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
-   Your Data Credit balance is capped at 200 credits (the free plan's rollover limit) at the end of your billing cycle — any credits above 200 are forfeited.

_**Note:** The credit balance icon in the top-right corner of your workspace shows a projected rollover amount. If you have scheduled a **downgrade to another paid plan**, the projection already reflects the pending plan's credits. However, if you have scheduled a **cancellation** (which moves your workspace to the Free plan), the projected amount does not account for the Free plan's 200-credit rollover cap — your actual balance after your billing cycle ends will be capped at 200 credits, regardless of the amount shown in the credit balance display._

**During your current billing cycle:**

-   Your Data Credit balance remains until the cycle ends.
-   You can use excess Data Credits.

**After your billing cycle ends:**

-   Your monthly Actions and Data Credit allocation resets to the new plan's level.
-   Your balance is capped at 2× the new plan's monthly Data Credit limit.
-   Your data remains intact.
-   Features are limited to the new plan's capabilities.

**Downgrading to the free plan:** The free plan includes only 100 Data Credits per month (rollover cap: 200 credits). Credits at or below 200 carry over; any credits above 200 are forfeited at the end of your billing cycle. If you have a large credit balance, spend it down before your cycle ends or contact support before downgrading to explore your options.

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

### Why do I see lower enrichment prices in my account but I'm still being charged the old rate?

If you see an in-product pricing summary comparing old and new enrichment costs (for example, ZeroBounce Validate Email showing 1 → 0.1 credits), those reduced rates apply to modern plans (Launch, Growth, or Enterprise) only. Customers on legacy plans continue to pay the original credit costs. To start benefiting from the lower data credit prices, go to `Settings` → `Plan & billing` and switch to a current plan. See [Legacy plans](./legacy-plans.md) for a full comparison of what changes when you migrate.

### Why do I pay Actions even when using my own API key?

Actions represent the platform orchestration Clay performs—ingesting, storing, and routing your data. Even with your own API keys, Clay is doing work to integrate that data into your workflows.

### What happens if I run out of Data Credits but not Actions?

You can either:

1.  Upgrade your Data Credits tier (no premium).
2.  Purchase a one-time top-up (30% premium on modern plans; 50% on legacy plans).

You don't need to change your Actions tier.

### What happens if I run out of Actions but not Data Credits?

You must upgrade to a higher action tier. Actions cannot be topped up separately because they're tied to your action tier's capacity.

If your billing cycle resets soon, waiting is also an option — your full Actions allotment replenishes automatically at your next renewal. You can check your exact renewal date in `Settings` → `Plan & billing`.

### Why can't I top up Actions?

Actions represent fixed platform capacity tied to your action tier. To get more Actions, you must upgrade to a higher action tier. Data Credits, however, are consumption-based and can be purchased as one-time top-ups or by upgrading your Data Credits tier.

### Do unused Data Credits or Actions roll over?

Actions reset each billing cycle and don't roll over, since they reflect the platform capacity your plan includes. Each plan includes enough Actions to cover 90% of customer usage, and if you need more, you can increase your Action tier.

Data Credits work more like a currency and do roll over. On Launch and Growth plans, unused credits can accumulate up to 2x your monthly credit amount (e.g., a 10,000 credit plan can bank up to 20,000 total). Enterprise customers can roll over up to 15% of their prior year's purchased credits, provided they renew at an equal or higher commitment.

**Trial plans:** Trial Data Credits are handled differently — see the [*I have a trial, when do the Data Credits expire?*](#i-have-a-trial-when-do-the-data-credits-expire) section below for details.

### Why do I see a warning that credits are "over the rollover limit" when my current balance is below the 2× cap?

The warning appears when your current balance is already high enough that adding your next monthly renewal would push the total over the 2× rollover cap — not because you are over it right now.

When your plan renews, your credit balance is capped at 2× your monthly allotment. If your current balance plus the credits you will receive at renewal would exceed that cap, you will see a warning showing how many credits are projected to fall above the cap at renewal.

**Example:** On a 10,000 credits/month plan (2× cap = 20,000), if your current balance is 17,150 credits, adding 10,000 at renewal would reach 27,150 — 7,150 above the cap. The warning shows: *"7,150 credits are over the rollover limit. Use them by [renewal date] or they will expire."* At renewal, your balance is set to 20,000.

No credits are affected before your renewal date — you can use them freely until then. To preserve more credits, spend down your balance before the renewal date shown in the warning.

### How do I estimate what my workflow will cost?

**Before purchasing a plan:** Use the [Clay Pricing Calculator](https://www.clay.com/credits-calculator) to scope out how many Actions and Data Credits your workflow is likely to consume.

**Once you have an account:** The enrichment panel shows costs before you run:

-   Actions: Always 1 per result.
-   Data Credits: Displayed next to each enrichment option.

For complex workflows, run a small test batch (10–50 records) to understand full costs.

### What happens to my Data Credits if I get invalid data?

It depends on whether the data provider refunds Clay. If the provider refunds Clay due to invalid data, those credits are passed back to your account. However, if the provider returned any data — even data that turns out to be invalid — credits are still charged because Clay incurs a cost for any data that was returned.

### How do I request a Data Credit refund?

Use the in-app chat (the icon in the bottom-right corner of the Clay interface) to contact support and start a refund request. Include the workbook, table, and column details where the issue occurred to help the support team investigate.

**Accidental enrichments:** If you ran an enrichment by mistake, the support team typically issues a one-time 50% Data Credit refund per account as standard policy. To avoid accidental enrichments, turn off `Auto-run` in column settings when you're not actively running enrichments, and test new workflows on a small batch first.

Note that credits are not refunded for enrichments where the system operated as intended — for example, an email validation that returns "invalid" is a valid result, not an error. The exception is AI columns (see below).

### Are Data Credits charged when a provider finds no result?

It depends on the provider's billing model. Some providers charge Clay only when data is successfully found, so credits are refunded if no result is returned. Others charge Clay for the API call regardless of whether data is found, so credits are deducted either way. You can see the exact credit cost for each enrichment in the enrichment panel before running.

### What happens to credits if an enriched email fails validation or turns out to be undeliverable?

Credits are charged when a provider returns a result — including email addresses that later fail a validation step or turn out to be undeliverable. There is no automatic credit refund when a returned email fails validation or bounces after sending; credits are deducted at the point the provider returns data, regardless of what happens to that address downstream.

For system errors (such as a timeout or infrastructure failure during enrichment), credits are automatically refunded.

**To limit credit spend on invalid emails:** Add an email validation step immediately after your waterfall enrichment. This won't recover credits already spent on the waterfall lookup, but it lets you filter out invalid addresses before running further enrichments — preventing additional credit spend on contacts with unusable email addresses. See [Waterfalls](building-a-data-waterfall.md) for how to configure validation in your waterfall workflow.

### Can I request a credit refund for poor AI column results?

AI columns complete with a success status even when the output quality is low or the column returns empty content, so no automatic credit refund fires for poor results. If an AI column produced consistently poor output due to a prompt misconfiguration or unexpected model behavior, you can contact [Clay support](https://app.clay.com) to request a review — a one-time credit exception may be granted at Clay's discretion. This is not an automated policy and is not guaranteed for future requests on the same column.

To minimize the risk of this situation: use the **Generate** button in the prompt cell to test your prompt on a single row before running at scale, and write clear, specific instructions with example inputs and outputs.

### How can I see when my credits will next renew?

There are two ways to check your credit renewal date:

-   **Credits button** — Click the **Credits** button in the top bar of your Clay workspace. The popover that opens shows your upcoming renewal date.
-   **Settings** (workspace admins only) — Navigate to `Settings` → `Plan & billing` to view your plan renewal date.

### How long does it take for Data Credits to renew?

When your plan renews, Data Credits are updated via a payment-processor webhook and typically appear within a few minutes of your renewal timestamp. If credits haven't updated shortly after the renewal time shown in your billing settings, wait a few minutes and refresh the page.

### Why are Data Credits being deducted unexpectedly?

Common causes:

-   **Actions stopped midway:** Already-sent requests still consume Data Credits.
-   `Auto-run` enabled: Automatic refreshes trigger enrichments.
-   **AI columns:** Every row processed incurs a cost.
-   **Duplicate enrichments:** Re-running columns triggers new usage.

**Prevention tips:**

-   Turn off `Auto-run` when not needed.
-   Pause AI columns that aren't providing value.
-   Check table settings before re-running enrichments.

### What happens when I downgrade or cancel my plan?

**During your current billing cycle:**

-   Your Data Credit balance remains until the cycle ends.
-   You can use excess Data Credits.

**After your billing cycle ends:**

-   Your monthly Actions and Data Credit allocation resets to the new plan's level.
-   Your balance is capped at 2× the new plan's monthly Data Credit limit.
-   Your data remains intact.
-   Features are limited to the new plan's capabilities.

**Downgrading to the free plan:** The free plan includes only 100 Data Credits per month (rollover cap: 200 credits). Credits at or below 200 carry over; any credits above 200 are forfeited at the end of your billing cycle. If you have a large credit balance, spend it down before your cycle ends or contact support before downgrading to explore your options.

_**Note:** The credit balance icon in the top-right corner of your workspace shows a projected rollover amount. If you have scheduled a **downgrade to another paid plan**, the projection already reflects the pending plan's credits. However, if you have scheduled a **cancellation** (which moves your workspace to the Free plan), the projected amount does not account for the Free plan's 200-credit rollover cap — your actual balance after your billing cycle ends will be capped at 200 credits, regardless of the amount shown in the credit balance display._

### Can Data Credits be restored after an unexpected loss?

In some situations, Clay's support team can manually restore Data Credits that were unexpectedly lost. Credit restoration is discretionary, handled case-by-case, and is not guaranteed. The following scenarios are worth contacting support about:

-   **Accidental usage**: If credits were consumed unintentionally (for example, by a run you did not mean to trigger), support may grant a one-time exception.
-   **Reactivating a paid plan after a lapse**: If you let a subscription lapse and then reactivate a paid plan, credits forfeited during the lapse may be eligible for restoration. Contact support after reactivating to request a review.
-   **Missing rollover credits after a plan upgrade**: If credits you expected to carry over are missing after upgrading your plan, contact support — this can be verified and manually corrected.

**What support cannot restore:**

-   Credits dropped above the 2× rollover cap — the system enforces this cap at renewal and cannot retroactively recover credits removed by it.
-   Credits forfeited when downgrading to the free plan above the 200-credit rollover cap.

To request a review, contact [Clay support](https://www.clay.com/contact) with details about your plan, when the credits were lost, and the reason.

### **I have a trial, when do the Data Credits expire?**

Unused trial Data Credits do not roll over. What happens to them depends on whether you convert to a paid plan:

-   **If you convert to a paid plan:** Your trial Data Credits do not carry over to the paid plan. At conversion, your balance is set to the Data Credits included with your new paid plan.
-   **If your trial ends without converting:** Your workspace moves to the Free plan, which includes 100 Data Credits per month with a rollover cap of 200 credits. Any trial balance above that cap is forfeited at your first monthly renewal on the Free plan.

To get the most out of your trial credits, use them before your trial ends.

### Does CSV export consume an Action?

No. Exporting data to CSV does not consume an Action or any Data Credits. CSV export is a simple data download operation and does not count as platform usage or GTM execution.

### Does Salesforce Lookup Record consume an Action credit?

No. **Lookup Record** operations — such as `Salesforce > Lookup Record` — read data from your CRM into Clay and are treated as CRM imports. They do not consume Action credits. This holds even when the lookup returns **No Records Found**.

Only CRM **write** operations consume Actions: Create Record, Update Record, Upsert Object, and other actions that push data from Clay to your CRM.

### Does enriching the same person in two separate tables charge me credits twice?

Yes. Clay charges **1 Action** (and the associated Data Credits) per enrichment row run, regardless of whether that person has been enriched in another table. There is no cross-table deduplication — each row runs independently. If the same contact appears in two tables and you run an enrichment such as Enrich Person in both, you will be charged for each run separately.

**To avoid double-charging on overlapping lists:** Merge your lists into a single table first and use the **Dedupe** feature (click a text, email, or URL column header → **Dedupe**) to remove duplicate entries based on a unique identifier such as a profile URL or email address. Enriching the merged, deduplicated table ensures each person is processed and charged only once.
