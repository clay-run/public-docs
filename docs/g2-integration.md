---
title: G2 integration
description: Find G2 products, pull their ratings, features, reviews, and competitors, and build lists of companies showing G2 buyer intent.
last_synced: 2026-10-01T22:59:47.105Z
---

# G2 integration

Find software products on G2, pull their ratings, features, reviews, and competitors, and build lists of companies researching the categories you compete in.

G2 is a software marketplace where buyers research, compare, and review business software. With this integration, you can build tables of companies showing buyer intent on G2, then enrich any product with the ratings, features, reviews, and competitor list behind its G2 profile.

## **Creating a table with G2**

1.  In a workbook, click `+ Add` at the bottom.
2.  Search for `G2` and select from the results.
3.  In the modal, you will be asked to `Select G2 account`.
    -   If you haven't already connected your G2 account, click `+ Add account` and enter your G2 API key.

**Note:** `Find companies with G2 Buyer Intent` reads the intent data G2 collects for the products your own company owns, so it runs on a G2 API key you connect yourself rather than the Clay-provided key. Add your key under `+ Add account` before setting that source up.

### `Source` Find companies with G2 Market Signals

Build a list of companies researching the G2 categories you choose, with one row per company.

**Inputs**

Required:

-   **Categories:** The G2 software categories to watch. Any company researching one of them shows up in the results.

Optional:

-   **Start date:** The start of the date range to check for signals, in `YYYY-MM-DD` form. Defaults to today.
-   **End date:** The end of the date range to check for signals. Defaults to today.
-   **Maximum results:** How many signals to pull, from 1 to 25,000. Defaults to 1,000. Several signals for the same company collapse into that company's one row, so you usually end up with fewer rows than signals.

**Outputs**

The source creates the following columns:

-   **Company name:** The name of the company behind the signal.
-   **Company domain:** The company's website domain.
-   **Category:** The G2 category the company was researching.
-   **Category ID:** That category's G2 ID, which you can pass to other G2 actions.
-   **Signal start date:** The start of the period the signal covers.
-   **Signal end date:** The end of the period the signal covers.

### `Source` Find companies with G2 Buyer Intent

Build a list of the companies researching your own G2 products, with the activity and visitor counts behind that research.

**Inputs**

Required:

-   **Product IDs or slugs:** One or more G2 product IDs or slugs to pull intent for, such as `hubspot-sales-hub`. Run the `Find products` enrichment first if you need to look one up.
-   **Group by:** How to group the activity into rows. Pick at least one; `Company name` and `Company domain` are selected by default, which gives one row per company. The options cover:
    -   Company details: name, domain, ID, industry, employees, country, state, and city.
    -   Product, category, and vendor: the name, slug, and ID of each.
    -   Compared products: the left and right product in a G2 comparison, by name, slug, and ID.
    -   Time buckets: `Day`, `Week`, `Month`, or `Time`.
    -   Visitor details: ID, country, state, and city.
    -   Signal details: `Signal type` and `Provider`.
-   **Metrics:** The aggregated numbers to return for each group. Pick at least one of `Total activity`, `Visitor count`, `Company count`, and `Last seen at`. Defaults to `Total activity`.

Optional:

-   **Company name contains:** Only return companies whose name contains this text.
-   **Start date:** Only return activity on or after this day, in `YYYY-MM-DD` form.
-   **End date:** Only return activity on or before this day.
-   **Sort by:** The field to sort on. It has to be one of the group-by fields or metrics you selected. Defaults to `Total activity`.
-   **Sort direction:** `Highest first` or `Lowest first`. Defaults to `Highest first`.
-   **Maximum results:** How many rows to return, from 1 to 25,000. Defaults to 1,000.

**Outputs**

The source creates one column for each group-by field and metric you selected, so the columns follow your configuration rather than a fixed list. Adding `Day`, `Week`, or `Month` to `Group by` adds a period column to each company's row.

## **Enriching data with G2**

1.  While in a Clay table, click `Add enrichment` and search for `G2`.
2.  Under `Integrations`, select one of the G2 actions.
3.  In the modal, you will be asked to `Select G2 account`.

**Note:** `Find product competitors`, `Get product ratings`, `Get product features`, and `Get product reviews` each start from a G2 product ID or slug. If a company domain or a product name is all you have, run `Find products` first and map its `Slug` or `Product ID` output into the next action.

### `Action` Find products

Search G2's product catalog by domain, keyword, product name, vendor, slug, or product ID.

**Inputs**

Required — provide at least one of these:

-   **Company domain:** The vendor's website domain, such as `salesforce.com`. This matches products whose G2 detail page URL contains the domain, which is the most practical lookup when a company domain is all you have.
-   **Search query:** Full-text search across product names and descriptions, such as `email marketing`.
-   **Product name:** A product name to match, such as `hubspot`. This is a partial match unless you turn on `Use exact match`.
-   **Vendor name:** The vendor or company behind the product, such as `HubSpot`.
-   **Product slugs:** One or more exact G2 slugs, such as `salesforce-sales-cloud`. Best when you already know the product.
-   **Product IDs:** One or more G2 product IDs, useful for batch lookups from a list you already have.

Optional:

-   **Use exact match:** Requires `Product name` to match exactly. Off by default, so partial matches come back.
-   **Categories:** Scope results to one or more G2 software categories.
-   **Star rating:** Only return products rated `1 star` through `5 stars`, as selected.
-   **Minimum review count:** Only return products with at least this many reviews, which screens out products with little review activity.
-   **Maximum results:** How many products to return, from 1 to 100. Defaults to 10.

**Outputs**

-   **Products found:** How many products matched.
-   **Product names:** The matched product names in one comma-separated cell.
-   **Products:** The full result list. Each product carries:
    -   **Product ID:** The product's G2 ID.
    -   **Product name:** The product's name on G2.
    -   **Slug:** The product's G2 slug.
    -   **Domain:** The product's domain.
    -   **Vendor website:** The vendor's own site for the product.
    -   **G2 URL:** The product's G2 profile.
    -   **Star rating:** The product's average star rating.
    -   **Review count:** How many reviews the product has.
    -   **Description:** The product's detailed description on G2.
    -   **Write review URL:** The link G2 uses to collect a new review for the product.
    -   **Image URL:** The product's logo image.

### `Action` Find product competitors

Find the products G2 lists as competitors to a product you specify.

**Inputs**

Required:

-   **Product ID or slug:** The G2 product ID or slug to find competitors for, such as `hubspot-sales-hub`.

Optional:

-   **Category:** Narrow competitors to a single G2 category, which helps when a product is listed in several.
-   **Maximum results:** How many competitors to return, from 1 to 50. Defaults to 10.

**Outputs**

-   **Competitors found:** How many competitors came back.
-   **Competitor names:** The competitor names in one comma-separated cell.
-   **Competitors:** The full list. Each competitor carries the same fields as a `Find products` result — product ID, name, slug, domain, vendor website, G2 URL, star rating, review count, description, write review URL, and image URL.

### `Action` Get product ratings

Get a product's G2 scores across the seven rating categories G2 tracks.

**Inputs**

Required:

-   **Product ID or slug:** The G2 product ID or slug to get ratings for.

Optional:

-   **Rating categories:** Which categories to return — `Ease of use`, `Quality of support`, `Ease of setup`, `Meets requirements`, `Ease of doing business with`, `Moving in the right direction`, and `Ease of admin`. All seven come back if you leave this empty.

**Outputs**

-   **Ratings found:** How many rating categories returned a score.
-   **Ratings:** One score per category you requested, alongside the G2 product ID the scores belong to.

### `Action` Get product features

List the features G2 tracks for a product, with each feature's rating and verification status.

**Inputs**

Required:

-   **Product ID or slug:** The G2 product ID or slug to get features for.

Optional:

-   **Category:** Filter features to a single G2 category, which helps for products listed in several.
-   **Functionality:** Filter by functionality type, such as `native` for natively supported features only.
-   **Verified only:** Return `Verified only` or `Unverified only` features.
-   **Created after:** Only return features created after this date.
-   **Created before:** Only return features created before this date.
-   **Updated after:** Only return features last updated after this date.
-   **Updated before:** Only return features last updated before this date.
-   **Maximum results:** How many features to return, from 1 to 100. Defaults to 25.

**Outputs**

-   **Features found:** How many features came back.
-   **Feature names:** The feature names in one comma-separated cell.
-   **Features:** The full list. Each feature carries:
    -   **Feature:** The feature's name.
    -   **Section:** The section of the product profile the feature sits under.
    -   **Description:** What the feature does.
    -   **Rating:** How reviewers rated the feature.
    -   **Review count:** How many reviews rated it.
    -   **Functionality:** How the product supports the feature.
    -   **Verified:** Whether G2 has verified the feature.
    -   **Available:** Whether the feature is available in the product.
    -   **Created at:** When the feature was added.
    -   **Updated at:** When the feature was last updated.

### `Action` Get product reviews

Pull G2 reviews for a product, either as the standard written review or as a market intelligence view of the same reviews.

**Inputs**

Required:

-   **Product ID or slug:** The G2 product ID or slug to get reviews for.

Optional:

-   **Return market intelligence data:** Swaps the standard review fields for market intelligence fields — pricing, contract length, ROI timeframe, implementation cost, switching reasons, feature ratings, and reviewer firmographics. Off by default.
-   **Company segment:** Only return reviews from `Small Business (50 or fewer emp.)`, `Mid-Market (51-1000 emp.)`, or `Enterprise ( >1000 emp.)` reviewers, as selected.
-   **Region:** Only return reviews from reviewers in `North America`, `Europe`, `Asia`, `Middle East`, or `ANZ`.
-   **Reviewer role:** Only return reviews from reviewers whose role is `User`, `Administrator`, `Executive Sponsor`, `Internal Consultant`, or `Consultant`.
-   **NPS star rating:** Only return reviews with the ratings you select, from 1 to 5. G2 derives this rating from the reviewer's 0-to-10 NPS score, so it works like a star rating rather than an NPS score.
-   **NPS score:** Only return reviews with the scores you select, from 0 to 10. Pick 9 and 10 for promoters, or 0 through 6 for detractors.
-   **Categories:** Only return reviews tied to the G2 categories you select.
-   **Exclude answer text:** Leave out reviews containing this answer text.
-   **Created after:** Only return reviews created after this date.
-   **Created before:** Only return reviews created before this date.
-   **Updated after:** Only return reviews last updated after this date.
-   **Updated before:** Only return reviews last updated before this date.
-   **Maximum results:** How many reviews to return, from 1 to 100. Defaults to 10.

**Outputs**

-   **Reviews found:** How many reviews came back.
-   **Review titles:** The review titles in one comma-separated cell.
-   **Reviews:** The full list. Every review carries **Review ID**, **Title**, **Review URL**, **Product name**, **Country**, **Last updated at**, and **Answers**.
    -   **Answers:** The reviewer's written responses — `What they like best`, `What they dislike`, `Benefits realized`, `Recommendations to others`, `Implementation cost`, and `ROI timeframe` — each with the question G2 asked and the reviewer's answer. Which ones come back depends on the questions that reviewer answered.
    -   Standard reviews also carry **Star rating**, **Published at**, **Submitted at**, **Regions**, **Source**, **Review incentive**, **Verified current user**, **Official response present**, **Comments present**, and **Slug**.
    -   Market intelligence reviews instead carry **Rating**, **Feature ratings**, **Company segment**, **Industry**, **Reviewer company**, **Country code**, **Region**, **Categories**, **Switched from products**, and **Switching reason**.

### Run settings

-   **Auto-update:** Recommended for `Find products` so that new rows added to your table are looked up automatically.
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))

## **FAQs**

### What happens if an action finds no match?

The enrichment actions and `Find companies with G2 Market Signals` refund runs that find no match, so an unmatched domain or a product with no reviews doesn't cost you anything. `Find companies with G2 Buyer Intent` is the exception — a run that returns no activity isn't refunded.

### What's the difference between the two G2 sources?

`Find companies with G2 Market Signals` starts from G2 categories and returns one row per company, with the category and the date range its most recent signal covers. Use it to find accounts already in-market for a category you compete in, whether or not they have looked at your profile.

`Find companies with G2 Buyer Intent` starts from the G2 product IDs you own and returns activity that has been aggregated for you, so you choose how rows are grouped and which numbers come back. Use it to see who is spending time on your own profiles and comparison pages, and how that changes week to week.

### Can I use a different G2 category for each row?

Yes. Click the gear button beside `Categories` or `Category`, switch the input to `Text with tokens`, and map a column holding the G2 category ID you want for that row.

The same works for the other select inputs in these actions, including `Star rating`, `Rating categories`, and `Company segment`. The `Category ID` column that `Find companies with G2 Market Signals` creates is a convenient thing to map in.

### What date formats do the date filters accept?

Anything readable as a date works — `2024-01-01`, `Jan 1 2024`, or a column of timestamps — and Clay converts it into the format G2 expects. If a value can't be read as a date, the run fails and names the field it came from, so you can fix that one input instead of checking the whole table.
