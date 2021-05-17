# CCSwap V1 Subgraph

[CCSwap](https://ccswap.org/) is a decentralized lending AMM compound trading protocol, which is a Dex invested and incubated by CCFOX Labs. In addition to the conventional SWAP function, CCSwap also integrates the features of liquidity mining, token loaning liquidity provision , On-Chain perpetual contract trading, On-Chain options trading, trade mining, multi-chain support, etc.

This subgraph dynamically tracks any pair created by the CCSwap factory. It tracks of the current state of CCSwap contracts, and contains derived stats for things like historical data and USD prices.

- aggregated data across pairs and tokens,
- data on individual pairs and tokens,
- data on transactions
- data on liquidity providers
- historical data on CCSwap, pairs or tokens, aggregated by day

## Running Locally

Make sure to update package.json settings to point to your own graph account.

## Queries

Below are a few ways to show how to query the ccswap-subgraph for data. The queries show most of the information that is queryable, but there are many other filtering options that can be used, just check out the [querying api](https://thegraph.com/docs/graphql-api). These queries can be used locally or in The Graph Explorer playground.

## Key Entity Overviews

#### CCSwapFactory

Contains data across all of CCSwap V1. This entity tracks important things like total liquidity (in ETH and USD, see below), all time volume, transaction count, number of pairs and more.

#### Token

Contains data on a specific token. This token specific data is aggregated across all pairs, and is updated whenever there is a transaction involving that token.

#### Pair

Contains data on a specific pair.

#### Transaction

Every transaction on CCSwap is stored. Each transaction contains an array of mints, burns, and swaps that occured within it.

#### Mint, Burn, Swap

These contain specifc information about a transaction. Things like which pair triggered the transaction, amounts, sender, recipient, and more. Each is linked to a parent Transaction entity.

## Example Queries

### Querying Aggregated CCSwap Data

This query fetches aggredated data from all CCSwap pairs and tokens, to give a view into how much activity is happening within the whole protocol.

```graphql
{
  ccswapFactories(first: 1) {
    pairCount
    totalVolumeUSD
    totalLiquidityUSD
  }
}
```
