---
title: Kernel integration
description: Resolve company records to legal entities, map corporate hierarchies, and enrich firmographics using Kernel's entity resolution platform.
last_synced: 2026-09-22T15:04:40.621Z
---

# Kernel integration

Resolve a company record to the one real entity behind it, map its corporate structure, and pull firmographics for every entity in the group with Kernel.

Kernel is an entity resolution and company data provider. It works out which real company a messy record actually refers to, maps how that company sits inside its corporate group, and returns firmographics for each entity in the group. Clay resells Kernel, so you can run it as an enrichment on any table once your workspace has Kernel enabled.

Kernel's data is grounded in legal entities rather than domains, and that difference shows up in your results. Resolved entities, their hierarchies, and their firmographics all arrive with a confidence level and a written explanation attached, so you can see how Kernel reached an answer before you act on it.

**Note:** Kernel is available to workspaces with Kernel enabled, on the Enterprise plan, and needs a Kernel subscription of your own. Your Clay rep can get you set up.**Cost per run:**`Resolve company entity` — 5 data credits + 1 action credit`Resolve company hierarchy` — 10 data credits + 1 action credit`Enrich company firmographics` — 7.5 data credits + 1 action creditRuns that come back with no data are **refunded**.

## KERN IDs

Every entity Kernel resolves gets a KERN ID — a persistent identifier for one corporate entity, resolved from the name, website, email domain, and address you provide.

KERN IDs aren't anchored to domains. Several distinct entities often share one website: a regional arm, a business unit, and the group brand can all sit on the same domain, and a domain-keyed match collapses them into a single record. Kernel gives each one its own KERN ID, which is what lets a corporate hierarchy hold its shape instead of flattening.

Two things make the identifier worth storing:

-   **It's the input to everything else.** The `Resolve company hierarchy` and `Enrich company firmographics` actions each take a `KERN ID` and nothing else.
-   **It survives rebrands and domain migrations.** Written back to your CRM or warehouse, it gives you a crosswalk between the systems that hold the same accounts.

## Enriching data with Kernel

Kernel's three actions run in sequence. The `Resolve company entity` action comes first and returns a `KERN ID`; `Resolve company hierarchy` and `Enrich company firmographics` each take that `KERN ID` as their only input, so neither one can run until the first has returned.

1.  While in a Clay table, click `Add enrichment` and search for `Kernel`.
2.  Select `Resolve company entity`.
3.  In the modal, `Select Kernel account`, or click `+ Add account` and paste your `Kernel API Key`.
4.  Under `Company identifiers`, map at least one field from your table. Mapping more of them improves the match.
5.  Once that column returns a `KERN ID`, add `Resolve company hierarchy` or `Enrich company firmographics` as a new enrichment and map the `KERN ID` column into it.

Every Kernel action returns a set of job fields alongside its data: `Kernel job ID`, `Kernel job status`, `Kernel job created at`, and `Kernel job completed at`. Kernel does its work in the background and posts each result back to Clay when it's ready, so these tell you when a given row finished.

### `Action` Resolve company entity

Match a company record to the one real entity it refers to, and return that entity's KERN ID.

**Inputs**

Required:

-   **Company identifiers:** At least one of the fields in this group. Each one is optional on its own, and filling in more of them improves the match.
    -   **Legal name:** The registered legal name, for example `Stripe, Inc.`
    -   **Trading name:** The brand or trading name, for example `Stripe`.
    -   **Website:** The company's website.
    -   **Company professional URL:** The company's page on its professional network.
    -   **Street address**, **City**, **State**, **Postal code**, and **Country:** The company's address. `Country` takes either a country name or a two-letter country code.
    -   **Email:** An email address at the company. Only the domain is used for matching.

Optional:

-   **Your record ID:** Your own identifier for the record, such as a Clay row ID or a Salesforce account ID.
-   **Match to professional profile:** When enabled, Kernel also tries to match the resolved entity to the company's page on its professional network.

**Outputs**

-   **KERN ID:** The resolved entity's identifier, and the input to the other two Kernel actions.
-   **Identity type:** The kind of identity Kernel matched the record to, such as a legal entity.
-   **Identity resolution confidence** and **Identity resolution reasoning:** `HIGH`, `MEDIUM`, or `LOW`, plus a written explanation of how Kernel reached the match.
-   **Legal info:** The registered entity — its `Legal name`, `Trading name`, `Website`, and `Country`, with `Legal info confidence` and `Legal info reasoning`.
-   **Trading info:** The same company as it goes to market — its `Trading name`, `Website`, and `Country`, with its own confidence and reasoning. A registered identity and a market-facing one are often different, and Kernel returns both rather than picking one.
-   **Entity classification:** `Entity classification type`, such as `Company`, and `Entity classification subtype`, such as `Operating`, with reasoning.
-   **Company registration number:** The entity's registration number, where Kernel has one on record.

### `Action` Resolve company hierarchy

Find the parents above a resolved entity, and whether it is a regional arm of a larger group.

**Inputs**

Required:

-   **KERN ID:** The KERN ID of a resolved entity. Map the column your `Resolve company entity` enrichment wrote it to.

**Outputs**

| Output | What it returns |
| --- | --- |
| Parent | The entity that directly owns this one. |
| Top parent | The entity at the top of the ownership chain. This can be a pure holding company with no commercial activity of its own. |
| Top operating parent | The highest entity in the chain that actually operates, holding companies excluded. This is usually the level where buying power sits, and the one to anchor an account on. |
| Regional subsidiary | Whether this entity is a regional arm of a larger group, with its Regional subsidiary scope and reasoning. |

Each of the three parent outputs carries the same set of fields for that company, prefixed with the parent's name — `Parent legal name`, `Top parent legal name`, and so on. Alongside the names you get that parent's own `KERN ID`, website, country, entity category and subcategory, confidence, and reasoning. The entity category is where a holding company is distinguished from an operating one.

Because every parent carries its own KERN ID, you can chain another Kernel action straight off one — walking a level further up the hierarchy, or enriching the operating parent you plan to build the account on.

### `Action` Enrich company firmographics

Add operating status, addresses, headcount, and revenue to a resolved entity.

**Inputs**

Required:

-   **KERN ID:** The KERN ID of a resolved entity. Map the column your `Resolve company entity` enrichment wrote it to.

**Outputs**

-   **Operational status:** Whether the entity is still trading, with reasoning.
-   **Location:** Two addresses — `Operating address` and `Registered address` — each with street, city, state, country, and postal code. Companies are often registered somewhere other than where they work.
-   **Headcount:** `Headcount` and `Entity headcount` for this entity, `Consolidated headcount` for its whole hierarchy, each with confidence and reasoning.
-   **Revenue:** Revenue in USD and in the company's local currency, at both the entity and the consolidated level, with `Revenue currency`, `Revenue source`, confidence, and reasoning.

The entity and consolidated figures answer different questions. A consolidated number covers the whole hierarchy, so it tells you the size of the group you are selling into. An entity number covers this company alone, which is how you tell one regional subsidiary's revenue from another's.

Segmenting on the wrong one is how a large multi-entity account ends up looking small, or one subsidiary ends up looking like the entire group.

### Run settings

-   **Auto-update:** Recommended when new accounts land in the table continuously, so each one gets resolved without you rerunning the column by hand.
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))

## Coverage

Kernel's coverage is global, and it reaches past the companies that usually appear in a company dataset.

-   **Geography and segment:** US accounts, alongside SMB, public sector, and non-US markets.
-   **Entity types:** Brands and establishments resolve, not only registered legal entities — so a company that never shows up in a registered-entity dataset can still get a KERN ID.
-   **Companies Kernel hasn't seen before:** When Kernel holds no stored match for a record, it resolves the entity live rather than returning nothing.

## FAQs

### Should I use Kernel or Clay's account hierarchies?

They are separate products that answer the hierarchy question in different ways, and holding a Kernel subscription doesn't change how Clay's own action behaves.

Clay's `Enrich account hierarchies` action runs on Clay's company dataset and needs no extra subscription. It is the quicker path for US companies and the world's largest public companies, and it returns parents and subsidiaries as rows with Clay company IDs on them that you can enrich straight away. The account hierarchies doc covers it.

Reach for Kernel when the input records are ambiguous — a missing website, a website shared across several entities, or a name that doesn't match its domain. It is also the one to use when you need the legal structure rather than just the operating one, a global operating parent to anchor an account on, or coverage beyond the US.

### What does an empty hierarchy or firmographics result mean?

Three outcomes look similar in the column and mean different things:

-   **Kernel couldn't find the KERN ID.** The run finishes without data rather than erroring.
-   **There is nothing above the company.** A `Resolve company hierarchy` run that comes back with no parent means Kernel resolved the entity and found it standalone. That's an answer, not a miss.
-   **No KERN ID on the row.** Neither of these two actions can run without one, and the run fails asking you to resolve the company entity first.
