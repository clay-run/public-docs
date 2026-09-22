---
title: Account hierarchies
description: Use the Enrich account hierarchies action to map parent companies and subsidiaries for any company in a Clay table.
last_synced: 2026-09-22T05:31:35.889Z
---

# Account hierarchies

Map the parent companies and subsidiaries around any company in your table with the Enrich account hierarchies action.

Large accounts rarely arrive in your data as a single company. They show up as business units, regional entities, and brands that all belong to the same parent, and nothing in the record says so.

The `Enrich account hierarchies` action maps that structure around a company you already have, returning every parent above it and every subsidiary below it. With the structure in a column, you can roll activity up to the account you actually sell to, route a new lead to the rep who owns the parent, or expand from one business unit into the rest of the group.

**Note:** Account hierarchies are in beta. Introductory pricing is 2 data credits + 1 action credit per run, or 4 credits on legacy plans, until Dec 1, 2026 — after that date it becomes 3 data credits + 1 action credit, or 5 credits on legacy plans. Runs that find no hierarchy data are refunded.

**Tip:** Use the Clay company ID whenever you have one. Names and domains change when a company rebrands or migrates, so a lookup keyed on them can miss the hierarchy or match the wrong company — a Clay company ID never changes. The action returns one for every company in the result, so you can chain one lookup straight into the next.  

## Enriching data with account hierarchies

1.  While in a Clay table, click `Add enrichment` and search for `Enrich account hierarchies`.
2.  Under `Company identifiers`, map the column that holds your `Clay company ID (recommended)`. If you don't have one, leave that field empty and fill in at least one field under `Other company identifiers` instead.
3.  Under `Hierarchy data`, choose what to return — set `Parent companies`, `Subsidiaries`, or both. A run needs at least one of the two.

### `Action` Enrich account hierarchies

Find parent companies and subsidiaries for a company, using a Clay company ID or other company details.

**Inputs**

Required:

-   **Clay company ID (recommended):** The company's numeric Clay company ID, for example `111521557`. When it's filled in, every field under `Other company identifiers` is ignored. (Required if no other company identifier is provided.)
-   **LinkedIn URL:** The company's page on LinkedIn. (Required if no Clay company ID, `Company domain`, or `Company name` is provided.)
-   **Company domain:** The company's domain, for example `clay.com`. (Required if no Clay company ID, LinkedIn URL, or `Company name` is provided.)
-   **Company name:** The company's name, for example `Clay`. (Required if no Clay company ID, LinkedIn URL, or `Company domain` is provided.)
-   **Hierarchy data:** A run needs at least one of the two settings below.
    -   **Parent companies:** How far up the hierarchy to look. `All parent companies` returns every available level above the company, `Immediate parents` returns one level above, and `Ultimate parent` returns the top of the hierarchy. Defaults to `All parent companies`.
    -   **Subsidiaries:** How far down the hierarchy to look. `All subsidiaries` returns every available level below the company, and `Immediate subsidiaries` returns one level below. Defaults to `All subsidiaries`.

Optional:

-   **Company headquarters location:** The company's headquarters location. Adding it improves matching.
-   **Limit:** The maximum number of companies to return for each hierarchy type you selected, so a run with both selected can return up to this many parents and this many subsidiaries. Defaults to 500, with a maximum of 10,000.

**Outputs**

-   **Resolved input company:** The company Clay matched your input to, with its `Clay company ID`, `Name`, `Domain`, and company profile URL. Read this first when a result looks off — it tells you which company was actually looked up.
-   **Parent companies:** The parents returned for your `Parent companies` setting, ordered from the top of the hierarchy down. Each row carries:
    -   **Level:** The company's absolute position in the hierarchy, where `1` is the ultimate parent.
    -   **Distance from input company:** How many steps separate that company from the one you looked up.
    -   **Clay company ID, Name, Domain, and company profile URL:** The same identifiers as the resolved input company, so you can chain another lookup or enrichment off any row.
-   **Subsidiaries:** The subsidiaries returned for your `Subsidiaries` setting, with the same fields as `Parent companies` plus one more:
    -   **Immediate parent Clay company ID:** The Clay company ID of that subsidiary's direct parent, which lets you rebuild the shape of the tree instead of just a flat list.
-   **Result status** and **Status message:** Whether the lookup found hierarchy data, matched the company but found no relationships, or couldn't match the company at all. `Status message` spells the outcome out in a readable sentence.

### Run settings

-   **Auto-update:** Recommended when new accounts land in the table continuously, so each one gets its hierarchy looked up without you rerunning the column by hand.
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))

## Coverage

Account hierarchies are built from Clay's own company dataset, so a company has to be in that dataset to show up in a result. Coverage is strongest where that data is densest.

-   **Geography and segment:** The action covers the US operating and brand universe, plus the Global 2000 — the list of the world's largest public companies. Non-US companies are mapped less consistently.
-   **Company size:** Results are most reliable for companies with 50 or more employees. Startups and recently-acquired businesses are less consistently mapped.
-   **Relationship types:** Every relationship comes back as either a parent or a subsidiary. The data doesn't characterize what kind of relationship it is, so a holding company and an operating parent look the same in a result.
-   **Where hierarchy data appears:** Hierarchy data is available in this action and in Search, Clay's list-building surface for companies and people. It isn't available in the classic filter experience or in the `Find lookalikes` search mode.

## FAQs

### How is this different from the `Get Company Hierarchy` managed function?

They answer the same question in two different ways. This action is deterministic: it resolves your input to a company in Clay's dataset and returns the relationships recorded there, so the same input gives you the same result every time, with identifiers on every row that you can enrich or join on.

The `Get Company Hierarchy` managed function — one of the ready-made workflows Clay builds and maintains — does AI research instead. It starts from a company name and domain, researches the hierarchy, and returns it with the reasoning attached.

Reach for the action when you need structured, repeatable relationships across a large list, especially if you plan to act on the rows at scale. Reach for the managed function when this action comes up empty for a company, or when you want a described hierarchy with its reasoning rather than rows you can join on. The [managed functions doc](https://university.clay.com/docs/managed-functions) covers how to run one.

### Can I filter a search by where a company sits in a hierarchy?

Yes. Add the `Hierarchy status` filter to a Companies search in Search, and set it to `Ultimate parent`, `Subsidiary`, or both.

That's a different job from this action. The filter narrows which companies come back in a search, so you can build a list of just the parent entities you sell into. The action maps the structure around companies you already have. The [Search doc](https://university.clay.com/docs/search) covers the filter in more detail.

### Why did my lookup return a company but no parents or subsidiaries?

Clay matched your input to a company but has no hierarchy recorded for it. Most often that's because the company genuinely stands alone, or because it sits outside the coverage described above.

`Result status` and `Status message` tell you which of those happened, and they're worth reading before you conclude a company is independent — a lookup that couldn't match the company at all is a different outcome from one that matched a company with no relationships.

If it's a matching problem rather than a coverage one, a more specific identifier usually fixes it. A Clay company ID resolves the company exactly, and `Company headquarters location` gives Clay more to match on.
