# Guide to Creating White Whales Pools

## Introduction

This guide outlines the detailed process of creating liquidity pools within White Whale's ecosystem, ensuring a comprehensive and accurate setup. By following these steps, you can create and manage pools effectively also ensuring you are following our evolving standard to get pools listed quickly.

## 1. Preparation and Initial Setup

### Initial Contact and Gathering Information

- **Collect Essential Token Details:** Including name, symbol, logo, and decimals.
- **For pools not paired against WHALE,** collect the same info for both tokens.

### Register Native Assets

**Contract Message for Adding Native Token Decimals:**

```json
{
  "add_native_token_decimals": {
    "denom": "<denom_path>",
    "decimals": <number_of_decimals>
  }
}
```
- **Documentation:** [Add Native Token Decimals](https://docs.whitewhale.money/white-whale-docs/liquidity-hub/overview-1/terraswap-factory#add-native-token-decimals)

## 2. Smart Contract Creation and Liquidity Addition

### Determine Token Ratios and Specify Deployment Chain

- **Choose the blockchain for deployment** and **establish the liquidity distribution ratio.**

### Order of Assets

- Decide the order based on the token type (stablecoin or non-stablecoin).

### Set Initial Liquidity and Use CLI for Pool Creation

**Contract Message for Creating a Pool:**

```json
{
  "create_pair": {
    "asset_infos": [
      {
        "native_token": {
          "denom": "<first_token_denom>"
        }
      },
      {
        "native_token": {
          "denom": "<second_token_denom>"
        }
      }
    ],
    "pool_fees": {
      "protocol_fee": {
        "share": "0.001"
      },
      "swap_fee": {
        "share": "0.002"
      },
      "burn_fee": {
        "share": "0.0"
      }
    },
    "pair_type": "constant_product",
    "token_factory_lp": true
  }
}
```
- **Documentation:** [Create Pair](https://docs.whitewhale.money/white-whale-docs/liquidity-hub/overview-1/terraswap-factory#create-pair)

### Add Initial Liquidity

**Before adding a swap route,** ensure initial liquidity is provided.

- **Initial Liquidity Documentation:** [Adding Initial Liquidity](https://docs.whitewhale.money/white-whale-docs/liquidity-hub/overview-1)

## 3. Setting Up Incentives and Frontend Integration

### Incentives Setup

**Contract Message for Creating Incentives:**

```json
{
  "create_incentive": {
    "lp_asset": {
      "native_token": {
        "denom": "<lp_token_denom>"
      }
    }
  }
}
```
- **Documentation:** [Create Incentive](https://docs.whitewhale.money/white-whale-docs/liquidity-hub/overview-1/incentive-factory#create-incentive)

### Frontend Setup

- **Configure GUI,** document the pool, and list it in the frontend `pools_list`.

## 4. Asset Listing, Indexing, and Testing

### Ensure Token and LP Asset Listing

- **Verify that tokens and LP are listed** in the asset directory.

### Indexing with Enigma and Coinhall

- **Provide details to Enigma and Coinhall** for indexing.

### Integration with Coingecko API

- **Have Enigma add the pool information** to the Coingecko API.

### Testing Pool Functionality

- **Verify creation, setup, and perform tests** for swaps and liquidity provision.

## 5. Submit Pool for Listing on Analytical Platforms

- **Coingecko API Submission:** Enhance discoverability by listing the pool on analytical platforms.

## Conclusion

By following this guide and utilizing the provided contract messages, you can ensure the accurate creation, documentation, and operation of liquidity pools.