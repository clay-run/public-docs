---
title: Credit refunds
description: Learn when Clay refunds Actions and Data Credits, and which actions refund when a provider returns no data.
last_synced: 2026-11-02T19:32:08.158Z
---

# Credit refunds

Learn when Clay refunds Actions and Data Credits, and which actions refund when a provider returns no data.

Learn when Clay refunds Actions and Data Credits, and which actions refund when a provider returns no data.

Clay charges for an enrichment per record, at the point a data provider charges us for the API call behind it. When a provider can't deliver valid data and refunds Clay, Clay refunds that record's charge back to you.

Actions and Data Credits are the two usage metrics Clay bills against, and a refund returns both. For what each one measures, see [Actions & data credits](https://university.clay.com/docs/actions-data-credits).

## How refunds work

Refunds are automatic, so there's nothing to request. Clay settles the refund as part of the run itself, which means the credits are back on your balance once the run finishes.

A refund returns everything that run was charged: the Data Credits for the provider call and the Action for the record. It also comes off the spend counted against workbook and budget credit limits, so a refunded run frees that allowance up again.

## Run outcomes that refund

Every run finishes with a status, and that status decides whether the credits come back.

| Run status | Credits refunded |
| --- | --- |
| Success | No — the provider returned data. |
| No data | Only for the actions listed below. |
| Blocked data | Yes. |
| Preview run | Yes. |
| Error | Yes, in most cases. |
| Timed out | Yes. |
| Invalid input | Yes. |
| Missing input | Yes. |
| Some inputs missing | Yes. |
| Missing authentication | Yes. |
| Invalid credentials | Yes. |
| Run condition not met | Yes. |
| Retried but failed | Yes. |
| Rate limit wait time exceeded | Yes. |
| Run Stopped | Yes. |
| Action disabled | Yes. |
| Empty response | No. |

**Note:** A run that is still in flight — `Running...`, `Queued...`, or `Awaiting callback...` — hasn't been settled yet, so there's nothing to refund until it lands on a final status.

## Actions that refund when no data is returned

Many actions charge whether or not the provider finds a match, because the provider charges Clay either way. The actions below are the exceptions: when one of them comes back with `No data`, the provider refunds Clay and Clay refunds you.

They're grouped by the kind of data each one returns.

### AI and text generation

| Provider | Action |
| --- | --- |
| Anthropic | Generate text with Claude |
| Artificial Intelligence | Extract B2B customers from domain |
| ElevenLabs | Text to speech |
| Lavender | Rate your emails |

### Email and phone verification

| Provider | Action |
| --- | --- |
| Findymail | Verify email |
| Hunter | Verify email |
| Icypeas | Verify email |
| Kitt | Verify email |
| Openmart | Enrich and verify email (SMB) |
| Openmart | Enrich and verify phone (SMB) |
| Snov.io | Verify email |
| SureConnect | Verify phone number |
| Trestle | Verify contact |
| Trestle | Verify phone number |

**Note:** A verification result of `invalid` is a real answer, so it's charged. Credits come back only when the provider can't reach a verdict at all.

### Email finding

| Provider | Action |
| --- | --- |
| Actovia | Find contact email |
| Aviato | Find hashed personal email |
| Aviato | Find personal email |
| BetterContact | Find work email |
| Bytemine | Find hashed personal email |
| ContactLevel | Find hashed emails |
| ContactOut | Find personal email from professional profile |
| Datagma | Find work email |
| Dropcontact | Find work email |
| Enrich CRM | Find work email |
| Enrow | Find work email |
| Findymail | Find work email |
| Findymail | Find work email from profile URL |
| Firmable | Find work email |
| Forager | Find personal email |
| FullEnrich | Find work email |
| Hunter | Find emails by company |
| Hunter | Find work email |
| Icypeas | Find emails for domain |
| Icypeas | Find work email |
| Kitt | Find work email |
| LeadMagic | Find personal email |
| LeadMagic | Find work email |
| Limadata | Find hashed emails |
| Limadata | Find personal email from GitHub profile |
| Lunar.io | Find work email |
| MixRank | Find hashed personal email |
| MixRank | Find personal email |
| People Data Labs | Find personal email |
| Pipecorn | Find work email |
| Prospeo | Find work email |
| Pubrio (APAC) | Find email (APAC) |
| SMARTe | Find work email |
| Snov.io | Find email |
| Snov.io | Find emails for domain |
| Surfe | Find email |
| Vector | Find hashed emails |
| Versium | Get hashed emails & phones for ad targeting |
| Wiza | Find hashed personal email |
| Wiza | Find personal email |
| Wiza | Find work email |
| Zeliq | Find email |

### Phone finding

| Provider | Action |
| --- | --- |
| Actovia | Find contact phone |
| BetterContact | Find mobile phone |
| ContactOut | Find mobile number from professional profile |
| Datagma | Find mobile number |
| Datagma | Find mobile number from full name |
| Enrow | Find mobile phone number |
| Findymail | Find mobile phone |
| Firmable | Find mobile phone |
| Forager | Find mobile phone number |
| FullEnrich | Find mobile phone |
| LeadMagic | Find mobile number |
| Lunar.io | Find mobile phone |
| Pipecorn | Find mobile phone |
| Prospeo | Find mobile number |
| Pubrio (APAC) | Find phone number (APAC) |
| SMARTe | Find company phone number |
| SMARTe | Find mobile number |
| Surfe | Find mobile phone number |
| upcell | Find mobile number |
| Weekday (India) | Find phone number (India) |
| Wiza | Find phone number |
| Zeliq | Find phone number |

### People and contact enrichment

| Provider | Action |
| --- | --- |
| Actovia | Find property contacts |
| Aviato | Find professional profile |
| Bytemine | Find contact info |
| Champify | Find professional profile URL |
| Clay Enrichments | Find mobile number & professional URLs |
| Clearbit | Enrich person & company |
| Companies, People, Jobs | Enrich person |
| Companies, People, Jobs | Find & enrich person from Google Search |
| Companies, People, Jobs | Find contacts at company |
| Companies, People, Jobs | Find people lookalikes |
| ContactOut | Find professional URL from personal email |
| Crunchbase | Enrich a person's basic profile |
| Datagma | Enrich person |
| Datagma | Find employees at company |
| Datagma | Find professional profile |
| Dropcontact | Enrich person |
| Enigma | Find a person's company affiliations |
| Enrich CRM | Enrich contact |
| Enrich CRM | Reverse email lookup |
| Forager | Enrich person |
| Forager | Find professional profile |
| Forager | Find professional profile from phone number |
| GovSpend | Enrich person |
| GovSpend | Find people |
| Icypeas | Enrich profile |
| Icypeas | Find people at company |
| Icypeas | Find professional profile |
| Leadfeeder | Enrich contact |
| Leadfeeder | Find people at company |
| LeadMagic | Find professional profile |
| Limadata | Find personal email from professional profile |
| Limadata | Find professional profile from email |
| Limadata | Find professional profile from work details |
| LiveData | Find professional profile |
| Lusha | Find people lookalikes |
| Minerva | Enrich person wealth & income |
| Minerva | Find professional profile |
| MixRank | Enrich person from email |
| NBS (Japan) | Get key contacts (Japan) |
| Openmart | Find people at company (SMB) |
| People Data Labs | Enrich person |
| Prospeo | Find people at company |
| Pubrio (APAC) | Enrich personal profile (APAC) |
| Pubrio (APAC) | Find people at company |
| Pursuit | Enrich a public sector contact |
| RB2B | Professional URL to hashed emails |
| RB2B | Professional URL to personal email |
| Reverse Contact | Enrich professional profile |
| Reverse Contact | Find professional profile |
| SMARTe | Enrich contact |
| SMARTe | Find person's company domain |
| SMARTe | Find professional profile from name and company |
| SMARTe | Find professional profile from work email |
| Snov.io | Enrich person from email |
| Snov.io | Enrich person from professional profile URL |
| Surfe | Find people at company |
| Surfe | Find professional profile |
| The Org | Get a person's manager |
| The Swarm | Find warm intros to company |
| Wiza | Find professional profile |

### Company intel

| Provider | Action |
| --- | --- |
| Actovia | Enrich owner holdings value |
| Actovia | Enrich owner holdings value (historical) |
| Actovia | Enrich owner portfolio summary |
| Actovia | Enrich property details |
| Actovia | Enrich property value |
| Actovia | Enrich property value (historical) |
| Actovia | Find owner's properties |
| Aviato | Enrich private company financial data |
| Aviato | Find private company acquisitions |
| Aviato | Find private company legal compliance data |
| Beauhurst (UK & Germany) | Enrich company (UK & Germany) |
| Beauhurst (UK & Germany) | Find company corporate structure (UK & Germany) |
| Beauhurst (UK & Germany) | Find company funding (UK & Germany) |
| Brandfetch | Get logo and brand data |
| CB Insights | Assess commercial maturity |
| CB Insights | Classify company industry |
| CB Insights | Enrich company acquisitions |
| CB Insights | Enrich company funding activity |
| CB Insights | Enrich corporate hierarchy |
| CB Insights | Find company competitors |
| CB Insights | Find company partnerships |
| CB Insights | Get company revenue |
| CB Insights | Get company total funding |
| CB Insights | Get company valuation |
| CB Insights | Get public identifiers |
| Champify | Find company professional profile |
| Clearbit | Enrich company |
| Clearbit | Enrich IP address |
| Companies, People, Jobs | Enrich account hierarchies |
| Companies, People, Jobs | Enrich company |
| Companies, People, Jobs | Find active job openings |
| Companies, People, Jobs | Find company lookalikes |
| Companies, People, Jobs | Find employee headcount by country |
| Companies, People, Jobs | Find employee headcount by criteria |
| Company URL Finder | Find domain from company name |
| Crunchbase | Enrich a company's categories & industry profile |
| Crunchbase | Enrich a company's competitors |
| Crunchbase | Enrich a company's growth & heat scores |
| Crunchbase | Enrich a company's press references |
| Crunchbase | Enrich a principal's investor stats |
| Crunchbase | Enrich company's acquisitions |
| Crunchbase | Enrich company's basic information |
| Crunchbase | Enrich company's financials |
| Crunchbase | Enrich company's investors |
| Crunchbase | Enrich company's latest funding round |
| Crunchbase | Enrich investment fund's details |
| Crunchbase | Find a principal's investment activity |
| Datagma | Enrich company |
| dealroom.co | Get company investors |
| dealroom.co | Get company valuation |
| dealroom.co | Get fundraising data for company |
| dealroom.co | Get investor's funds |
| dealroom.co | Get investor's investments |
| Enigma | Get 12-month average transaction count |
| Enigma | Get 12-month average transaction size |
| Enigma | Get 12-month card growth rate |
| Enigma | Get 12-month card revenue |
| Enigma | Get 3-month card growth rate |
| Enigma | Get operating location addresses |
| Enigma | Get operating location count |
| Enigma | Resolve company identity |
| Enrich CRM | Enrich company firmographics |
| Enrich CRM | Enrich company latest funding |
| Enrich CRM | Enrich company with French SIRENE |
| Enrich CRM | Find French SIREN number |
| Explorium | Enrich company ratings and employee sentiment |
| Explorium | Enrich public company business challenges |
| Explorium | Enrich public company competitive landscape |
| Explorium | Enrich public company strategic insights |
| GovSpend | Enrich agency |
| GovSpend | Enrich agency's aggregated bid activity |
| GovSpend | Enrich employee count by criteria |
| GovSpend | Find bids and RFPs |
| GovSpend | Get bid document details |
| Harmonic.ai | Get fundraising data for company |
| HG Insights | Enrich company |
| HG Insights | Find company corporate structure |
| HG Insights | Find company domain |
| Icypeas | Enrich company |
| Icypeas | Find company professional profile |
| Intellizence | Enrich company with latest fundraising data |
| Intellizence | Enrich company with latest news data |
| Intellizence | Find news for companies |
| Kernel | Enrich company firmographics |
| Kernel | Resolve company entity |
| Kernel | Resolve company hierarchy |
| Leadfeeder | Enrich company |
| LeadMagic | Enrich company |
| LeadMagic | Find active job openings |
| Lusha | Find company lookalikes |
| Magellan Data | Enrich PE portfolio companies |
| Magellan Data | Find corporate family |
| Magellan Data | Find parent company |
| Magellan Data | Find PE owner |
| NBS (Japan) | Enrich company details (Japan) |
| NBS (Japan) | Find companies (Japan) |
| NBS (Japan) | Get company departments (Japan) |
| NBS (Japan) | Get group affiliated companies (Japan) |
| NBS (Japan) | Get marketing tags (Japan) |
| Openmart | Find businesses (SMB) |
| Owler | Enrich company |
| People Data Labs | Enrich company |
| People Data Labs | Enrich company detailed employee trends |
| People Data Labs | Enrich company job post insights |
| People Data Labs | Enrich IP address |
| People Data Labs | Get employee count by criteria |
| Pubrio (APAC) | Enrich company |
| Pubrio (APAC) | Find open jobs at company |
| Pursuit | Enrich a public sector account |
| Pursuit | Find public sector signals |
| Pursuit | Find public sector signals for an account |
| Pursuit | Search public sector accounts |
| Reverse Contact | Enrich company profile |
| Reverse Contact | Find company professional profile |
| SMARTe | Enrich company |
| SMARTe | Find company address |
| SMARTe | Find company domain |
| SMARTe | Find company employee count |
| SMARTe | Find company founding year |
| SMARTe | Find company industry |
| SMARTe | Find company name |
| SMARTe | Find company professional profile URL |
| SMARTe | Find company revenue |
| SMARTe | Find parent and global parent companies |
| SMARTe | Find parent company |
| Snov.io | Find company domain |
| Spade | Enrich company's payment processing insights |
| Store Leads | Enrich company |
| Surfe | Enrich company |
| The Org | Find company org chart |
| TheirStack | Find jobs |
| Vainu (Nordic) | Enrich company assets |
| Vainu (Nordic) | Enrich company earnings |
| Vainu (Nordic) | Enrich company equity & liabilities |
| Vainu (Nordic) | Enrich company revenue |
| Vainu (Nordic) | Enrich company salary costs |
| Vainu (Nordic) | Enrich employee count |
| Vainu (Nordic) | Enrich industry, location and founding date |
| Versium | IP to domain lookup |

### Buying intent and signals

| Provider | Action |
| --- | --- |
| Bombora | Find companies with buying intent |
| Bombora | Find company topic intent |
| Bombora | Find company topic intent by geo |
| Clay | Find companies with topic intent |
| Clay | Find people with topic intent |
| Delivr | Find companies with buying intent |
| Delivr | Find company topic intent |
| Delivr | Find people with buying intent |
| Delivr | Find person topic intent |
| G2 | Find companies with G2 Market Signals |
| Intentsify | Find companies with buying intent |
| Intentsify | Find company topic intent |
| Intentsify | Find company topic intent by geo |
| Intentsify | Find company topic intent by persona |
| Intentsify | Find people with buying intent |
| Intentsify | Find person topic intent |
| Lusha | Find company headcount growth signal |
| Lusha | Find company IT spend signal |
| Lusha | Find company jobs growth by department signal |
| Lusha | Find company jobs growth by location signal |
| Lusha | Find company jobs growth signal |
| Lusha | Find company news signal |
| Lusha | Find company website traffic signal |
| Lusha | Find person signals |
| TrustRadius | Enrich company with buying intent from TrustRadius |

### Technology and products

| Provider | Action |
| --- | --- |
| BuiltWith | Enrich website technologies |
| BuyerCaddy | Compare company tech stack |
| BuyerCaddy | Enrich company technologies |
| BuyerCaddy | Find alternative or complementary technology products |
| BuyerCaddy | Verify technology usage |
| CB Insights | Classify company technology |
| Enigma | Get payment technologies |
| Enrich CRM | Enrich website technologies |
| Forager | Enrich website technologies & traffic |
| G2 | Find product competitors |
| G2 | Find products |
| G2 | Get product features |
| G2 | Get product ratings |
| G2 | Get product reviews |
| HG Insights | Enrich website technologies |
| HG Insights | Verify technology usage |
| Openmart | Find tech stack (SMB) |
| Pubrio (APAC) | Enrich company technologies |
| Similarweb | Find website technologies |
| SMARTe | Enrich company technologies |
| Spade | Enrich payment & delivery technologies |
| Sumble | Enrich company technologies |

### Advertising and website analytics

| Provider | Action |
| --- | --- |
| Adbeat | Find ad media mix and spend for company |
| Adbeat | Find companies spending the most on an ad publisher |
| Adbeat | Find cumulative ad spend for a company |
| Adbeat | Find lookalike companies based on advertising data |
| Adbeat | Find top ad networks used by a company |
| Adbeat | Find top ad publishers used by a company |
| Adbeat | Find top ads published by a company |
| Adbeat | Find top advertising geographies for a company |
| Adbeat | Find top YouTube channels a company is advertising on |
| Adyntel | Check for Google ads |
| Adyntel | Check for Meta ads |
| Adyntel | Check for professional social media ads |
| Aviato | Find private company social metrics |
| Aviato | Find private company web traffic |
| Enrich CRM | Enrich monthly website traffic |
| Explorium | Enrich company social media metrics |
| Foreplay | Discover brands by ads |
| Foreplay | Get ad details |
| Foreplay | Get brands by domain |
| Foreplay | Search and filter ads |
| Foreplay | Search brands by name |
| SE Ranking | Get AI search visibility |
| SE Ranking | Get organic competitors |
| SE Ranking | Get traffic and ad spend |
| Semrush | Get company social media engagement |
| Semrush | Get company top pages |
| Semrush | Get company traffic sources |
| Semrush | Get company website traffic's geographic distribution |
| Semrush | Get competitors in paid search |
| Semrush | Get traffic analytics |
| Similarweb | Get global website traffic rank |
| Similarweb | Get monthly website visits |
| Similarweb | Get website average visit duration |
| Similarweb | Get website bounce rate |
| Similarweb | Get website pages per visit |

### Social media and creators

| Provider | Action |
| --- | --- |
| Influencers.club | Enrich creator details |
| Influencers.club | Find all social profiles from one |
| Influencers.club | Find creator personal email |
| Influencers.club | Find creator phone number |
| Influencers.club | Find lookalike creator profiles |
| Influencers.club | Find social profiles by creator email |
| Modash | Enrich influencer details |
| Modash | Find audience overlap between two creators |
| Modash | Find creator personal email |
| Modash | Find influencer contacts |
| Modash | Find lookalike creator profiles |
| Modash | Find social profiles by creator email |
| Professional Posts | Enrich professional post |
| Professional Posts | Get a person's professional post comments |
| Professional Posts | Get a person's professional post reactions |
| Professional Posts | Get a person's professional posts and shares |
| Professional Posts | Get comments on a professional post |
| Professional Posts | Get reactions on a professional post |
| Professional Posts | Get shares on a professional post |
| Trigify | Enrich professional profile |
| Trigify | Find prospects engaging with professional posts |
| Upfluence | Enrich influencer details |
| Upfluence | Find creator personal email |
| Upfluence | Find social profiles by creator email |
| Upriver | Find products |
| Upriver | Find sponsors |
| Upriver | Find sponsorships |
| Upriver | Get audience personas |
| Upriver | Get brand details |
| Upriver | Get product details |
| YouTube | Enrich YouTube channel |
| YouTube | Enrich YouTube video |
| YouTube | Extract YouTube video transcript |

### Utilities

| Provider | Action |
| --- | --- |
| Aviato | Normalize location |
| Clay | Get page screenshot |
| Clay Scrapers | Find data from page (beta) |
| Enrich CRM | Get homepage content |
| GitHub | Find forks on GitHub |

## Checking whether a run was refunded

Open a cell to see its details. The cost line reads `Charged:` followed by the amount, with `(Refunded)` beside it when those credits went back.

## FAQs

### Why wasn't a run that errored refunded?

Nearly every error refunds, but a couple of outcomes don't. If a provider replies with something Clay can't read as a result, or an export run can't find the destination it was pointed at, the run keeps its charge.

Those two show up as `Error` in the table above, which is why that row says "in most cases" rather than "yes". If a run looks like it should have been refunded and wasn't, reach out to Clay support with the table and column.

### Does using my own API key change what gets refunded?

With your own key connected, the provider bills you directly and Clay charges no Data Credits, so there are none to refund. The Action for the record is still charged, and still refunded on any outcome in the table above.

### Can a run be refunded only in part?

Yes. Some actions price on what comes back, so the charge is settled when the run completes rather than when it starts. Where the final cost lands below what was taken upfront, Clay returns the difference instead of the whole amount.

### Is a run refunded if it stops because a credit limit was reached?

Yes. Hitting a workbook, budget, workflow, or per-user credit limit stops the run before you get a result, so anything already taken for it comes back.
