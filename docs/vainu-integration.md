---
title: Vainu integration
description: Use Vainu in Clay to enrich Nordic companies with their registry details and the figures from their filed annual accounts.
last_synced: 2026-09-28T16:43:58.127Z
---

# Vainu integration

Use Vainu in Clay to enrich Nordic companies with their registry details and the figures from their filed annual accounts.

Vainu is a company data provider that builds its company records from the Nordic national business registries. With this integration, you can look a company up by domain, name or registry ID, then pull back its registry profile along with the figures from its filed annual accounts — revenue, earnings, employee count, salary costs and balance sheet totals.

## **Enriching data with Vainu**

1.  While in a Clay table, click `Add enrichment` and search for `Vainu`.
2.  Under `Integrations`, select one of the Vainu actions — the integration is listed as `Vainu (Nordic)`.
3.  In the modal, you will be asked to `Select Vainu account`.
    -   If you have your own Vainu account, click `+ Add account` and enter your `Client ID` and `Client secret`, which you create in Vainu under `Settings` → `API Access`. Otherwise, use the Clay provided key.

**Note:** Vainu reads the national business registries of Finland, Sweden, Norway and Denmark, so these actions cover companies registered in one of those four countries. If you connect your own Vainu credentials, the registries you can reach follow your Vainu subscription — Clay checks which ones your credentials cover when you add the account and tells you what it found.

### Inputs

All seven actions take the same inputs: the registry to look in, plus at least one way to identify the company.

Required:

-   **Country:** The national business registry to look the company up in — `Finland (FI)`, `Sweden (SE)`, `Norway (NO)` or `Denmark (DK)`.

Under `Company identifiers`, at least one of:

-   **Company domain:** The company's website domain (e.g., `vainu.com`).
-   **Company name:** The company name as registered.
-   **Business ID:** The company's official registry number, either country-prefixed like `FI25578642` or in the local format like `2557864-2`.

Which identifier you map changes how reliably Vainu lands on the right company:

-   **A domain or a `Business ID` is the surest route.** Both are unique to one company, so the match is unambiguous.
-   **A company name has to match the registered name.** Registries keep the legal form as part of the name and Vainu sets that aside when comparing, so `Volvo AB` still matches the registered `Aktiebolaget Volvo`. A trading name or a shortened name the company never registered won't match, and the cell comes back empty rather than settling for a near-namesake.
-   **A country-prefixed `Business ID` sets its own registry.** Map `FI25578642` while `Country` is set to `Sweden (SE)` and the lookup runs against Finland.
-   **`Country` can vary row by row.** It's a dropdown by default; click the gear button next to it and switch to `Text with tokens` to map a column instead. The mapped value needs to be `FI`, `SE`, `NO` or `DK`.

### Actions

Six of the seven actions read a company's filed financial statements — the annual accounts these registries collect — and report the most recently filed figure. The seventh returns the registry profile.

| Action | What it returns | Outputs |
| --- | --- | --- |
| Enrich industry, location and founding date | The company's registry profile: legal form, industry classification, addresses, founding date, registered status, and company-level contact details. | Legal form, Country, Founded date, Primary industry, Primary industry code, Registered address, Visiting address, Company email, Company phone, Official status, Is active, Website, Domain |
| Enrich employee count | Headcount as reported in the company's filing. | Employee count |
| Enrich company revenue | Revenue — total sales for the accounting period — from the filed income statement. | Revenue, Currency |
| Enrich company earnings | Earnings — the profit or loss left after costs — from the filed income statement. | Earnings, Currency |
| Enrich company salary costs | Wages and salaries as reported in the filed income statement. | Salary costs, Currency |
| Enrich company equity & liabilities | The funding side of the balance sheet: what the owners hold, what the company owes, and the total of the two. | Total equity and liabilities, Equity total, Liabilities total, Currency |
| Enrich company assets | The other side of the balance sheet: what the company owns. | Total assets, Current assets total, Cash and cash equivalents, Inventory, Currency |

Every action also returns `Company name` and `Business ID`, and the six financial actions add `Fiscal period end` so you can see which accounting period a figure came from.

`Legal form` and `Official status` come back in the registry's own language, so a Finnish company reads `Osakeyhtiö` and `Aktiivinen` rather than their English equivalents. `Is active` gives you the same standing as a true/false value if you'd rather filter on that.

Which actions you add depends on what you're using the data for:

-   **Sizing and scoring accounts** — `Enrich employee count` and `Enrich company revenue` carry most of the weight.
-   **Reading financial health** — `Enrich company assets` and `Enrich company equity & liabilities` give you both sides of the balance sheet, and `Enrich company salary costs` shows how much of the cost base goes on people.
-   **Routing and segmenting** — `Enrich industry, location and founding date` gives you the official industry code and registered address to route on.

Each action is its own enrichment column and its own lookup, so add the ones you'll use rather than all seven.

### Run settings

-   **Auto-update:** Useful when new companies keep arriving in the table, so they're enriched as they land instead of waiting for you to re-run the column. Annual accounts are filed once per accounting period, so rows that already have data rarely change in between.
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))

## **FAQs**

### Why do two actions report different accounting periods for the same company?

Because each action reports the most recent period that actually holds its figure. A filing can carry a full income statement but leave the employee count blank, or report a balance sheet total without the breakdown beneath it.

Each action works back through the filings until it finds one carrying the figure it's after, so `Enrich company revenue` and `Enrich employee count` can land on different years for the same company. `Fiscal period end` on each column tells you which period you got.

### Why is `Fiscal period end` empty on some employee counts?

Norway's registry keeps a current headcount record alongside the dated annual filings, and that record isn't tied to an accounting period. When it's the most recent number available, `Enrich employee count` returns it and leaves `Fiscal period end` blank — so an empty period on a Norwegian company means you're looking at the current registry figure rather than a year-old filing.

### What currency are the amounts in?

The currency the company filed in: EUR in Finland, SEK in Sweden, NOK in Norway and DKK in Denmark. Clay passes the amount through without converting it, which is why `Currency` travels alongside every figure. Convert before you compare across countries or total up a mixed list.

### Are expense figures positive or negative?

`Salary costs` always comes back as a positive amount. The registries disagree on this — Finland and Sweden file salary costs as a negative number, Norway and Denmark as a positive one — so Clay reports the cost the same way for all four, which keeps a column of mixed countries comparable.

`Earnings` is passed through exactly as filed, so a negative value there is a real loss for the period.

### Can I pull earlier years instead of just the latest filing?

Yes. Alongside the latest figure, each financial action returns every earlier period it found that figure in, so a company with a decade of filings gives you a decade of revenue. Those earlier periods aren't mapped to columns by default — open the action's output to map the ones you want.

### Some figures filled in and others stayed empty on the same company — why?

Companies file different levels of detail, so how deep the data goes varies from one to the next. On the balance sheet actions in particular, a top-line total can be filed while a sub-total below it is left blank: `Total equity and liabilities` can be populated while `Liabilities total` is empty. The row still ran fine — there simply isn't a filed figure behind that one line.

### Am I charged for rows where Vainu doesn't find anything?

No. When a lookup finishes without a result, Clay refunds the credits for that row. The cell shows `Company not found` when nothing matched your identifiers, or something like `No filed revenue found` when the company matched but hasn't filed that particular figure — so the two cases are easy to tell apart at a glance.
