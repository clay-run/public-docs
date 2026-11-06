---
title: Definitive Healthcare integration
description: Find US hospitals and enrich them with executives, physicians, networks, payor mix, technology, and financial metrics from Definitive Healthcare.
last_synced: 2026-11-02T16:00:21.641Z
---

# Definitive Healthcare integration

Find US hospitals in Clay and enrich them with executives, physicians, networks, payor mix, technology, and financial metrics.

Definitive Healthcare is a commercial intelligence provider for the US healthcare market, covering hospitals, the networks they belong to, and the executives and physicians affiliated with them. With this integration, you can build hospital lists in Clay and enrich them with firmographics, affiliations, installed technology, payor mix, financial and clinical metrics, and contact details for named executives and physicians.

**Note:** These actions run on a Clay-managed account, so you don't need your own Definitive Healthcare subscription to use them. If you have one, connect your own API key instead — it costs fewer credits per record, and the data you get back matches the entitlements on your account.

## Creating a table with Definitive Healthcare

1.  In a workbook, click `+ Add` at the bottom.
2.  Search for `Definitive Healthcare` and select `Find hospitals` from the results.
3.  In the modal, you will be asked to `Select Definitive Healthcare account`.
    -   To use your own Definitive Healthcare subscription rather than the Clay-managed account, click `+ Add account` and enter your API key. Clay saves it as a `Definitive Healthcare API Key` connection and reuses it for every Definitive Healthcare action. ([Learn more about managing integration accounts](https://university.clay.com/docs/managing-integration-accounts))

### `Source` Find hospitals

Imports the US hospitals that match your search, each with its `Definitive ID` alongside its firmographics.

**Inputs**

-   **Filters to apply:** Your search. Click `Add filter` for each condition you want, then set its `Filter field`, `Condition`, and `Value`.
-   **Max hospitals to import** (optional): How many hospitals land in your table, up to 500.

`Filter field` covers 32 hospital attributes:

-   **Identity:** `Hospital name`, `Website`, `Hospital Definitive ID`, `Medicare provider number`, `Primary NPI`, `Tax ID`, `340B facility ID`, `Phone number`
-   **Location:** `City`, `State`, `ZIP code`, `County`, `Street address`, `Core-based statistical area (CBSA) code`, `Latitude`, `Longitude`
-   **Classification:** `Facility type`, `Hospital type`, `Operating status`, `Ownership`, `Trauma center level`, `Pediatric trauma center level`, `Health system integration level`
-   **Network:** `Network name`, `Parent network name`, `Network ID`, `Parent network ID`
-   **Market and payor:** `Medicare payor mix`, `Medicaid payor mix`, `Self-pay payor mix`, `Medicare administrative contract`, `Market concentration index`

`Condition` only offers the comparisons that fit the field you picked:

-   **Fields with a set list of values** — `Facility type`, `Hospital type`, `Operating status`, `Ownership`, `Trauma center level`, `Pediatric trauma center level`, `Health system integration level`, and `State` — offer `Is any of`, `Is none of`, and `Has a value`.
-   **Number fields**, such as the payor mix shares, `Market concentration index`, and the ID and coordinate fields, add `Greater than`, `Less than`, `Greater than or equal to`, and `Less than or equal to`.
-   **Text fields**, such as `Hospital name`, `City`, and `Network name`, add `Contains`, `Starts with`, and `Ends with`.

Reach for `Has a value` when you only care that a field is populated — it's the one condition that takes no `Value`.

`Is any of` and `Is none of` both accept several entries at once. The fields with a set list give you a picker to choose from; the rest take values you type in or pull from a column in your table.

**Note:** The three payor mix fields take a decimal rather than a percentage. Enter `0.32` to filter for a 32% share.

## Enriching data with Definitive Healthcare

1.  While in a Clay table, click `Add enrichment` and search for `Definitive Healthcare`.
2.  Under `Integrations`, select one of the Definitive Healthcare actions.
3.  In the modal, you will be asked to `Select Definitive Healthcare account`.

Every action identifies a hospital by its `Hospital Definitive ID`, except `Get hospital ID`, which finds that ID from a hospital name or website.

The actions that return a list of records page their results. `Max results` sets the page size — up to 1,000 records, and 25 if you leave it alone — while `Page` picks which page to fetch. Each of those actions returns a `Total pages` output, so you can see how many pages your filters produced before working through them.

### `Action` Get hospital ID

Looks up a hospital's Definitive ID from its name or its website.

**Inputs**

Required:

-   **Hospital name:** The hospital's name (Required if `Hospital website` is not provided).
-   **Hospital website:** The hospital's website (Required if `Hospital name` is not provided).

**Outputs**

The matching hospitals, each with facility name, Definitive ID, Medicare provider number, primary NPI and the full NPI list, firm type, website, company status, and a link to its Definitive Healthcare profile.

### `Action` Enrich hospital basic info

Returns firmographics for a hospital.

**Inputs**

Required:

-   **Hospital Definitive ID:** The hospital's numeric identifier in Definitive Healthcare.

**Outputs**

Hospital type, address, core-based statistical area code, phone, trauma center and pediatric trauma center level, health system integration level, 340B facility ID, tax ID, Medicare administrative contract, market concentration index, and physician counts.

### `Action` Enrich hospital parent network

Returns the network a hospital belongs to.

**Inputs**

Required:

-   **Hospital Definitive ID:** The hospital's numeric identifier in Definitive Healthcare.

**Outputs**

The network and parent network, each by ID and name.

### `Action` Enrich hospital's network affiliations

Returns the facilities affiliated with a hospital.

**Inputs**

Required:

-   **Hospital Definitive ID:** The hospital's numeric identifier in Definitive Healthcare.

Optional:

-   **Facility name:** Narrows results to affiliated facilities whose name matches.
-   **Facility type:** Select one or more facility types. Leave it blank to include every type.
-   **Sub-network name:** Narrows results to one sub-network.
-   **Max results:** Caps how many affiliations come back per page.

**Outputs**

Each affiliated facility's name, Definitive ID, firm type, address, and sub-network.

### `Action` Enrich hospital payor mix

Returns a hospital's payor mix.

**Inputs**

Required:

-   **Hospital Definitive ID:** The hospital's numeric identifier in Definitive Healthcare.

**Outputs**

The Medicaid, Medicare, and self-pay shares.

### `Action` Enrich hospital medical school affiliations

Returns the medical schools a hospital is affiliated with.

**Inputs**

Required:

-   **Hospital Definitive ID:** The hospital's numeric identifier in Definitive Healthcare.

**Outputs**

The affiliated medical schools.

### `Action` Enrich hospital technologies

Returns the technology a hospital currently runs.

**Inputs**

Required:

-   **Hospital Definitive ID:** The hospital's numeric identifier in Definitive Healthcare.

Optional:

-   **Technology:** Select one or more technologies. The dropdown groups them by category, so you can narrow to a category before picking. Leave it blank to include every technology.
-   **Vendor:** Select one or more vendors. Leave it blank to include every vendor.
-   **Max results:** Caps how many records come back per page.

**Outputs**

Each record's category, technology, vendor, product, vendor status, implementation year, and units installed.

### `Action` Enrich hospital financial and clinical metrics

Returns financial and clinical metrics for a hospital, such as licensed beds and average length of stay.

**Inputs**

Required:

-   **Hospital Definitive ID:** The hospital's numeric identifier in Definitive Healthcare.

Optional:

-   **Metrics:** Select one or more metrics to return. Leave it blank to include every metric.
-   **Max results:** Caps how many metrics come back per page.

**Outputs**

Each metric's name, description, and numeric value.

### `Action` Find hospital executives

Returns the executives at a hospital.

**Inputs**

Required:

-   **Hospital Definitive ID:** The hospital's numeric identifier in Definitive Healthcare.

Optional:

-   **First name:** Narrows results to executives with a matching first name.
-   **Last name:** Narrows results to executives with a matching last name.
-   **Department:** Select one or more departments. Leave it blank to include every department.
-   **Position level:** Select one or more position levels. Leave it blank to include every position level.
-   **Title:** Narrows results to a matching title.
-   **Only physician leaders:** Turn on to return only physician leaders. Turn off to include all executives.
-   **Max results:** Caps how many executives come back per page.
-   **Include email:** Adds each executive's work email. Costs extra per email found.
-   **Include phone number:** Adds each executive's direct dial. Costs extra per phone number found.

**Outputs**

Each executive's name, credentials, gender, department, position level, standardized title, title, location phone, professional profile URL, executive NPI, and physician flags.

### `Action` Find hospital physicians

Returns the physicians affiliated with a hospital.

**Inputs**

Required:

-   **Hospital Definitive ID:** The hospital's numeric identifier in Definitive Healthcare.

Optional:

-   **Primary practice state:** Narrows results to one state, selected from a picker.
-   **Primary practice city:** Narrows results to one city.
-   **Primary specialty:** Select one or more specialties. Leave it blank to include every specialty.
-   **Role:** Narrows results to roles containing the text you enter, so `Nurse` also matches `Nurse Practitioner`.
-   **Max results:** Caps how many physicians come back per page.
-   **Include Medicare data and secondary affiliations:** Adds each physician's Medicare activity and secondary affiliations. Costs extra per physician enriched.

**Outputs**

Each physician's NPI, name, credentials, role, gender, primary practice city and state, practice phone, primary specialty, and primary hospital affiliation.

### `Action` Enrich hospital physicians

Adds Medicare activity and secondary affiliations to a hospital's affiliated physicians.

**Inputs**

Required:

-   **Hospital Definitive ID:** The hospital's numeric identifier in Definitive Healthcare.
-   **NPI:** The physician's National Provider Identifier (Required if a first and last name are not provided).
-   **First name** and **Last name:** The physician's name (Required if `NPI` is not provided).

Optional:

-   **Primary practice state:** Narrows results to one state, selected from a picker.
-   **Primary practice city:** Narrows results to one city.
-   **Primary specialty:** Select one or more specialties. Leave it blank to include every specialty.
-   **Role:** Narrows results to roles containing the text you enter, so `Nurse` also matches `Nurse Practitioner`.
-   **Max results:** Caps how many physicians come back per page.

**Outputs**

Each physician's secondary affiliations and Medicare activity, including Medicare payments, charges, unique patients, and number of procedures.

### Run settings

-   **Auto-update:** Useful while hospitals are still being added to the table, so each new row is enriched as it arrives.
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))

## FAQs

### Why doesn't someone I can see in Definitive Healthcare come back in Clay?

Clay leaves out people who have asked not to be contacted. If an executive's professional profile URL, work email, direct dial, or location phone matches an opt-out record, the whole executive is left out of the results rather than returned with blank fields.

`Find hospital physicians` works the same way on a physician's practice phone. The hospital itself is unaffected either way.

### Do I need to run `Get hospital ID` before every enrichment?

Only once per hospital. Run it into its own column, then point every other action at that column.

If your hospitals came from the `Find hospitals` source, the ID is already there in the `Definitive ID` column, so you can skip the lookup entirely.

### How do I keep an action from returning more records than I need?

The actions that return a list of records charge on each record they return, so `Max results` is your main control — it sets how many come back per page, up to 1,000, and defaults to 25. `Find hospitals` works per run instead, capping at 500 hospitals.

The `Include email`, `Include phone number`, and `Include Medicare data and secondary affiliations` toggles each cost extra per record they enrich, so leave them off when you only need the roster. You aren't charged when an action finds no data, so a filter that matches nothing costs you nothing.

### Can I search hospitals by network without knowing the network's ID?

Yes. `Find hospitals` accepts `Network name` and `Parent network name` alongside `Network ID` and `Parent network ID`, so you can build a list for a health system by name.

To go the other direction and map a hospital you already have to its system, use `Enrich hospital parent network`.
