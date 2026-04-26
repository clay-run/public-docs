---
title: Dappradar integration overview
source_url: https://university.clay.com/docs/dappradar-integration-overview
description: Blockchain dapp store providing data and analytics for NFT, DeFi,
  and gaming exploration.
last_synced: 2026-04-26T01:39:50.701Z
upstream_hash: cd40989c1f312e0729974bfea6703797bdc54e220ff4f142e69dbccd842cd121
---

# Dappradar integration overview

Blockchain dapp store providing data and analytics for NFT, DeFi, and gaming exploration.

## DappRadar overview

DappRadar is a platform that provides comprehensive data and metrics for decentralized applications (Dapps) and NFT collections across multiple blockchains.

You can use the DappRadar integration to:

-   Find the top Decentralized Applications or NFT collections
-   Get NFT Collection Data and Metrics
-   Get Decentralized Application Data and Metrics

All DappRadar actions in Clay use a Clay-managed account and utilize your Clay credits.

## Using DappRadar data as a source

Import DappRadar data into a new existing table to find top Dapps or NFT collections across 50+ blockchains, filtering by blockchain, category, or metrics like transactions and volume.

Note that the limit on this search is 10,000 results and Clay will only import the first 10,000 results.

**Step 1:** Specify if you want to search for NFT collections or Dapps

### **Optional Steps**

**Step 2:** Specify Blockchain

To filter data by a specific blockchain, select the desired chain from the dropdown.

**Step 3:** Select Metric to Sort By

In the **Metric to Sort By** dropdown, choose a metric (e.g., Average Price, Traders, Volume, Sales, Market Cap, or Floor Price) to prioritize your data.

**Step 4:** Set Time Range and Limit

Specify a time range for the data, with options from 15 minutes to 30 days. The default is **24 hours**.

## Available DappRadar Actions

Within your Clay table, you’re able to run the following DappRadar-supported actions:

-   Get NFT Collection Data and Metrics
-   Get Decentralized Application Data and Metrics

### `Action` Get NFT Collection Data and Metrics

Get data and metrics from a single DappRadar NFT collection. This will find the blockchains the collection is on, as well as metrics -- sales, volume, traders, floor price -- during a specified time period, as well as percentage change in these metrics.

**Step 1:** Specify search parameters.

Enter the **Collection ID** from the NFT object.

Choose a **Timeframe** for metrics like transactions and balance. The default is 24 hours.

Select a specific **Blockchain**, or leave it blank to include all chains.

**Step 2:** Configure run settings.

By default, new rows within your Clay table will automatically run a DappRadar action. Learn more about auto-update in [this brief guide](https://docs.clay.com/en/articles/9642165-auto-update-and-auto-dedupe-table).

To run enrichment only under specific conditions, use formulas that trigger the column when the formula is true. Learn more about AI formulas in [this Clay University lesson](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101).

**Step 3:** Run your enrichment to Get NFT Collection Data within DappRadar.

### `Action` Get Decentralized Application Data and Metrics

Get data and metrics from a single DappRadar dapp. This will find social links, dapp category, and description for a dapp. It will also find the metrics such as transactions, UAW, and balance, as well as percentage changes over a specified time period.

**Step 1:** Specify search parameters.

Provide the **Dapp ID** from the DappRadar page, such as [Uniswap V3 About Page](https://dappradar.com/multichain/exchanges/uniswap-v3/about).

Set a **Timeframe** for metrics like transactions and balance. If no timeframe is specified, the default is 24 hours.

Enter the **Name** of the Dapp and provide its **Website URL**.

Include the **Smart Contract** address if applicable.

Specify a **Blockchain** for data filtering, or leave it blank to include all associated chains.

**Step 2:** Configure run settings.

By default, new rows within your Clay table will automatically run a DappRadar action. Learn more about auto-update in [this brief guide](https://docs.clay.com/en/articles/9642165-auto-update-and-auto-dedupe-table).

To run enrichment only under specific conditions, use formulas that trigger the column when the formula is true. Learn more about AI formulas in [this Clay University lesson](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101).

**Step 3:** Run your enrichment to Get Decentralized Application Data within DappRadar.
