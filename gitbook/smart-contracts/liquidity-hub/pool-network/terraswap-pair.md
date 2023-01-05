# 💱 Pair

The pair contract is the pool. Creating a new pool should be done via the pool factory, so that the pool is indexed in the pool registry stored by the factory. A pool can be created with native, ibc or cw20 tokens.

## Constant Product <a href="#constant-product" id="constant-product"></a>

For now, White Whale pools make prices based on a **constant product invariant:**&#x20;

$$
XY=k
$$

Where _**X**_ and _**Y**_ are the reserves for each token in the pool, while _**k**_ is a constant. The product of the number of tokens on each side of the pool should remain constant across trading operations. With _**X**_ being the current balance of the pool's source asset and and _**Y**_ being that of the target asset:

$$
XY=k=(X+∆x
​
 )(Y−∆y
​
 )
$$

To determine the value of the ask asset _**∆y**_ given the trader's offered asset _**∆x**_:

$$
∆y = Y∆x/(X+∆x)
$$

The market price is calculated by dividing the number of pool's target token into the source asset (also called the pool ratio).

The spread between the executed and the expected trade is:

$$
spread= (Y∆x/X) − (Y∆x/ (X+∆x))​
$$

The deeper the pool the smaller the spread.

## Liquidity Provision

A user or bot can provide liquidity by sending a `provide_liquidity` message and withdraw liquidity with `withdraw_liquidity`. Whenever liquidity is deposited into a pool, special tokens known as liquidity (LP) tokens are minted to the provider's address, in proportion to how much liquidity it contributed to the pool. These tokens are a representation of a liquidity provider's contribution to a pool. Whenever a trade occurs, the `swap_fee` percentage, which is a parameter specified by the `PoolFee`, is distributed pro-rata to all LPs in the pool at the moment of the trade. To receive the underlying liquidity back, plus commission fees that were accrued while their liquidity was locked, LPs must burn their liquidity tokens, which is done via `withdraw_liquidity`.

## Fees

There are three types of fees associated to the pools, namely `swap_fee`, `protocol_fee` and `burn_fee`. The `swap_fee` 
remains in the pool, causing a permanent increase in the constant product K. The value of this permanently increased pool goes to all LPs.

The `protocol_fee` goes to the protocol, and it is to be collected by the Fee Collector contract of the Liquidity Hub. 
The protocol revenue is then distributed to WHALE stakers in the form of token buybacks.

The `burn_fee` is a percentage of the tokens that is burned whenever a swap takes place.

## Feature toggle

Pools contain a feature toggle, containing the following properties: `withdrawals_enabled`, `deposits_enabled` and `swaps_enabled`. Those features are \`ON by default, but could be changed via governance. They could be changed in different scenarios, the ones we could envision include for example if a critical bug is found in a given feature, it could be shut down while is being fixed to avoid exploits. Additionally, if for example liquidity is desired to be migrated to another pool, deposits could be disabled to prevent bots or users to deposit liquidity in the pool.

The code for the pair contract can be found [here](https://github.com/White-Whale-Defi-Platform/migaloo-core/tree/main/contracts/liquidity\_hub/pool-network/terraswap\_pair).

***

The following are the messages that can be executed on the pair contract:

## Instantiate

Instantiates the pair.

```json
{
  "asset_infos": [
    {
      "native_token": {
        "denom": "ujuno"
      }
    },
    {
      "token": {
        "contract_addr": "juno1..."
      }
    }
  ],
  "token_code_id": 123,
  "asset_decimals": [
    6,
    6
  ],
  "pool_fees": {
    "protocol_fee": {
      "share": "0.01"
    },
    "swap_fee": {
      "share": "0.02"
    },
    "burn_fee": {
      "share": "0.01"
    }
  },
  "fee_collector_addr": "juno1..."
}
```

| Key                  | Type            | Description                                                                         |
| -------------------- | --------------- | ----------------------------------------------------------------------------------- |
| `asset_infos`        | \[AssetInfo; 2] | Information about the two assets                                                    |
| `token_code_id`      | u64             | Code if for the token contract. Used by the factory to create the LP token contract |
| `asset_decimals`     | \[u8; 2]        | Decimal places for the given assets                                                 |
| `pool_fees`          | PoolFee         | Pool fees for the given pair                                                        |
| `fee_collector_addr` | String          | Fee collector contract address                                                      |

## Migrate

Migrates a pair. This is to be triggered by the owner of the contract, i.e. the pool factory, via the `migrate_pair` message.

```json
{}
```

## ExecuteMsg

### Collect protocol fees

Sends the accrued protocol fees to the Fee Collector. This action can be triggered by anyone.

```json
{
  "collect_protocol_fees": {}
}
```

### Provide liquidity

Provides liquidity to the pool.

{% hint style="warning" %}
Note: in case of providing liquidity with a cw20 token, the message [increase\_allowance](terraswap-token.md#increase-allowance) should be called on the cw20 token contract **before** cw20 tokens can be transferred to the pool.
{% endhint %}


{% tabs %}
{% tab title="Native/IBC token" %}
```json
{
  "provide_liquidity": {
    "assets": [
      {
        "info" : {
          "native_token": {
            "denom": "ujuno"
          }
        },
        "amount": "1000"
      },
      {
        "info" : {
          "native_token": {
            "denom": "ibc/B3504E092456BA618CC28AC671A71FB08C6CA0FD0BE7C8A5B5A3E2DD933CC9E4"
          }
        },
        "amount": "1000"
      }
    ],
    "slippage_tolerance": "0.01",
    "receiver": "receiver_addr"
  }
}
```
{% endtab %}

{% tab title="cw20 token" %}
```json
{
  "provide_liquidity": {
    "assets": [
      {
        "info" : {
          "token": {
            "contract_addr": "juno1..."
          }
        },
        "amount": "1000"
      },
      {
        "info" : {
          "token": {
            "contract_addr": "juno1..."
          }
        },
        "amount": "1000"
      }
    ],
    "slippage_tolerance": "0.01",
    "receiver": "receiver_addr"
  }
}
```
{% endtab %}
{% endtabs %}

| Key                  | Type             | Description                                                                                               |
| -------------------- | ---------------- | --------------------------------------------------------------------------------------------------------- |
| `assets`             | \[Asset; 2]      | Assets to provide liquidity with                                                                          |
| `slippage_tolerance` | Option\<Decimal> | If set, the transaction will suceed if the price in the pool moves less than the given slippage tolerance |
| `receiver`           | Option\<String>  | Receiver address for the LP tokens in case it is different from the sender                                |

### Swap native

Swaps a native token.

```json
{
  "swap": {
    "offer_asset": {
      "amount": "100000",
      "info": {
        "native_token": {
          "denom": "ujuno"
        }
      }
    },
    "belief_price": "0.3524",
    "max_spread": "0.05",
    "to": "to_address"
  }
}
```

| Key            | Type             | Description                                                            |
| -------------- | ---------------- | ---------------------------------------------------------------------- |
| `offer_asset`  | Asset            | Asset to swap                                                          |
| `belief_price` | Option\<Decimal> | Belief price of the asset                                              |
| `max_spread`   | Option\<Decimal> | Max desired spread to perform the swap with                            |
| `to`           | Option\<String>  | Receiver address for ask asset in case it is different from the sender |

### Swap cw20

Swaps a cw20 token. This message is to be sent to the cw20 token contract address.

```json
{
  "send": {
    "contract": "pool_contract_address",
    "amount": "1000",
    "msg": "ewogICJzd2FwIjogewogICAgImJlbGllZl9wcmljZSI6ICIwLjM1MjQiLAogICAgIm1heF9zcHJlYWQiOiAiMC4wNSIsCiAgICAidG8iOiAidG9fYWRkcmVzcyIKICB9Cn0="
  }
}
```

where `ewogICJ...IKICB9Cn0=` is the following message, encoded in base64:

```json
{
  "swap": {
    "belief_price": "0.3524",
    "max_spread": "0.05",
    "to": "to_address"
  }
}
```

Note that `contract_addr` in the swap message is the cw20 token address to be swapped.

| Key            | Type             | Description                                                            |
| -------------- | ---------------- | ---------------------------------------------------------------------- |
| `belief_price` | Option\<Decimal> | Belief price of the asset                                              |
| `max_spread`   | Option\<Decimal> | Max desired spread to perform the swap with                            |
| `to`           | Option\<String>  | Receiver address for ask asset in case it is different from the sender |

### Update config

Updates the configuration of the pool.

```json
{
  "update_config": {
    "owner": "owner",
    "fee_collector_addr": "fee_collector_addr",
    "pool_fees": {
      "protocol_fee": {
        "share": "0.01"
      },
      "swap_fee": {
        "share": "0.02"
      },
      "burn_fee": {
        "share": "0.01"
      }
    },
    "feature_toggle": {
      "withdrawals_enabled": true,
      "deposits_enabled": true,
      "swaps_enabled": true
    }
  }
}
```

| Key                  | Type                   | Description                                                                          |
| -------------------- | ---------------------- | ------------------------------------------------------------------------------------ |
| `owner`              | Option\<String>        | New owner of the contract                                                            |
| `fee_collector_addr` | Option\<String>        | New fee collector address                                                            |
| `pool_fees`          | Option\<PoolFee>       | New pool fees                                                                        |
| `feature_toggle`     | Option\<FeatureToggle> | If set, toggles features on/off based on the parameters specified in `FeatureToggle` |

### Withdraw

Withdraws liquidity from the pool. This message is to be sent to the cw20 token contract address.

```json
{
  "send": {
    "contract": "pool_contract_address",
    "amount": "1000",
    "msg": "ewogICJ3aXRoZHJhd19saXF1aWRpdHkiOiB7fQp9"
  }
}
```

| Key        | Type    | Description                   |
| ---------- | ------- | ----------------------------- |
| `contract` | String  | Contract to send the `msg` to |
| `amount`   | Uint128 | Amount of tokens to be sent   |
| `msg`      | Binary  | Encoded message in base64     |

where `ewogICJ3...kiOiB7fQp9` is the `withdraw_liquidity` message, encoded in base64:

```json
{
  "withdraw_liquidity": {}
}
```

## Queries

### Config

Retrieves the configuration of the pool.

{% tabs %}
{% tab title="Query" %}
```json
{
  "config": {}
}
```
{% endtab %}

{% tab title="Response (ConfigResponse)" %}
```json
{
  "owner": "juno1...",
  "fee_collector_addr": "juno1...",
  "pool_fees": {
    "protocol_fee": {
      "share": "0.001"
    },
    "swap_fee": {
      "share": "0.002"
    },
    "burn_fee": {
      "share": "0.001"
    }
  },
  "feature_toggle": {
    "withdrawals_enabled": true,
    "deposits_enabled": true,
    "swaps_enabled": true
  }
}
```

| Key                  | Type          | Description                        |
| -------------------- | ------------- | ---------------------------------- |
| `owner`              | Addr          | The contract's owner               |
| `fee_collector_addr` | Addr          | The fee collector contract address |
| `pool_fees`          | PoolFee       | Pool fees                          |
| `feature_toggle`     | FeatureToggle | Settings for the feature toggle    |
{% endtab %}
{% endtabs %}

### Pair

Retrieves information of the pool pair.

{% tabs %}
{% tab title="Query" %}
```json
{
  "pair": {}
}
```
{% endtab %}

{% tab title="Response (PairInfo)" %}
```json
{
  "asset_infos": [
    {
      "native_token": {
        "denom": "ujuno"
      }
    },
    {
      "token": {
        "contract_addr": "juno1..."
      }
    }
  ],
  "contract_addr": "juno1...",
  "liquidity_token": "juno1...",
  "asset_decimals": [
    6,
    6
  ]
}
```

| Key               | Type            | Description                             |
| ----------------- | --------------- | --------------------------------------- |
| `asset_infos`     | \[AssetInfo; 2] | Asset infos for the pair                |
| `contract_addr`   | String          | Pair contract address                   |
| `liquidity_token` | String          | LP token contract address for the pair  |
| `asset_decimals`  | \[u8; 2]        | Decimals for the assets within the pool |
{% endtab %}
{% endtabs %}

### Pool

Retrieves information about the pool, i.e. liquidity provided, asset infos and total LP shares.

{% tabs %}
{% tab title="Query" %}
```json
{
  "pool": {}
}
```
{% endtab %}

{% tab title="Response (PoolResponse)" %}
```json
{
  "assets": [
    {
      "info": {
        "native_token": {
          "denom": "ujuno"
        }
      },
      "amount": "178102491"
    },
    {
      "info": {
        "token": {
          "contract_addr": "juno1..."
        }
      },
      "amount": "36870272692"
    }
  ],
  "total_share": "1720147158"
}
```

| Key           | Type        | Description                         |
| ------------- | ----------- | ----------------------------------- |
| `assets`      | \[Asset; 2] | Assets within the pool              |
| `total_share` | Uint128     | Total supply of the pool's LP token |
{% endtab %}
{% endtabs %}

### Protocol fees

Retrieves the protocol fees on the pool. If `all_time` is `true`, it will return the fees collected since the inception of the pool. On the other hand, if `all_time` is set to `false`, only the fees that has been accrued by the pool but not collected by the fee collector will be returned.

Alternatively, if `asset_id` is set the accrued fees (non collected) for that specific asset will be returned.

{% tabs %}
{% tab title="Query" %}
```json
{
  "protocol_fees": {
    "asset_id": "ujuno",
    "all_time": false
  }
}
```

| Key        | Type            | Description                                    |
| ---------- | --------------- | ---------------------------------------------- |
| `asset_id` | Option\<String> | Asset id to return the protocol fees for       |
| `all_time` | Option\<bool>   | Defines whether to return all time fees or not |
{% endtab %}

{% tab title="Response (ProtocolFeesResponse)" %}
```json
{
  "fees": [
    {
      "info": {
        "native_token": {
          "denom": "ujuno"
        }
      },
      "amount": "42661"
    }
  ]
}
```

| Key    | Type        | Description                |
| ------ | ----------- | -------------------------- |
| `fees` | Vec\<Asset> | Fees collected by the pair |
{% endtab %}
{% endtabs %}

### Burned fees

Retrieves the fees that have been burned by pool. If `asset_id` is set, only the burned fees for that specific 
asset will be returned, otherwise it returns burned fees for both assets in the pool.

{% tabs %}
{% tab title="Query" %}
```json
{
  "burned_fees": {
    "asset_id": "uhuahua"
  }
}
```

| Key        | Type            | Description                            |
| ---------- | --------------- |----------------------------------------|
| `asset_id` | Option\<String> | Asset id to return the burned fees for |
{% endtab %}

{% tab title="Response (ProtocolFeesResponse)" %}
```json
{
  "fees": [
    {
      "info": {
        "native_token": {
          "denom": "uhuahua"
        }
      },
      "amount": "42661"
    }
  ]
}
```

| Key    | Type        | Description             |
| ------ | ----------- |-------------------------|
| `fees` | Vec\<Asset> | Fees burned by the pair |
{% endtab %}
{% endtabs %}

### Simulation

Performs a swap simulation for the given token.

{% tabs %}
{% tab title="Query (native/ibc token)" %}
```json
{
  "simulation": {
    "offer_asset": {
      "info": {
        "native_token": {
          "denom": "ujuno"
        }
      },
      "amount": "1000"
    }
  }
}
```

| Key           | Type  | Description                |
| ------------- | ----- | -------------------------- |
| `offer_asset` | Asset | Asset to simulate swap for |
{% endtab %}

{% tab title="Query (cw20 token)" %}
```json
{
  "simulation": {
    "offer_asset": {
      "info": {
        "token": {
          "contract_addr": "juno1..."
        }
      },
      "amount": 1000
    }
  }
}
```

| Key           | Type  | Description                |
| ------------- | ----- | -------------------------- |
| `offer_asset` | Asset | Asset to simulate swap for |
{% endtab %}

{% tab title="Response (SimulationResponse)" %}
```json
{
  "return_amount": "206395",
  "spread_amount": "1",
  "swap_fee_amount": "414",
  "protocol_fee_amount": "207",
  "burn_fee_amount": "207"
}
```

| Key                   | Type    | Description                                                          |
|-----------------------| ------- |----------------------------------------------------------------------|
| `return_amount`       | Uint128 | Amount that would be delivered to the user after the swap            |
| `spread_amount`       | Uint128 | Spread the swap would have                                           |
| `swap_fee_amount`     | Uint128 | Swap fees amount that would be distributed among liquidity providers |
| `protocol_fee_amount` | Uint128 | Protocol fees amount                                                 |
| `burn_fee_amount`     | Uint128 | Fees that would be burned, if any, by executing the swap             |
{% endtab %}
{% endtabs %}

### Reserve simulation

Performs a reverse swap simulation, i.e. given the ask asset, how much of the offer asset is needed to perform the swap.

{% tabs %}
{% tab title="Query (native/ibc token)" %}
```json
{
  "reverse_simulation": {
    "ask_asset": {
      "info": {
        "native_token": {
          "denom": "ujuno"
        }
      },
      "amount": "1000"
    }
  }
}
```

| Key         | Type  | Description                         |
| ----------- | ----- | ----------------------------------- |
| `ask_asset` | Asset | Desired asset to get after the swap |
{% endtab %}

{% tab title="Query (cw20 token)" %}
```json
{
  "reverse_simulation": {
    "ask_asset": {
      "info": {
        "token": {
          "contract_addr": "juno1..."
        }
      },
      "amount": "1000"
    }
  }
}
```

| Key         | Type  | Description                         |
| ----------- | ----- | ----------------------------------- |
| `ask_asset` | Asset | Desired asset to get after the swap |
{% endtab %}

{% tab title="Response (ReverseSimulationResponse)" %}
```json
{
  "offer_amount": "207639",
  "spread_amount": "0",
  "swap_fee_amount": "2",
  "protocol_fee_amount": "1",
  "burn_fee_amount": "1"
}
```

| Key                   | Type    | Description                                                          |
| --------------------- | ------- |----------------------------------------------------------------------|
| `offer_amount`        | Uint128 | Offer asset amount that is needed to get the given ask asset         |
| `spread_amount`       | Uint128 | Spread the swap would have                                           |
| `swap_fee_amount`     | Uint128 | Swap fees amount that would be distributed among liquidity providers |
| `protocol_fee_amount` | Uint128 | Protocol fees amount                                                 |
| `burn_fee_amount`     | Uint128 | Fees that would be burned, if any, by executing the swap             |
{% endtab %}
{% endtabs %}
