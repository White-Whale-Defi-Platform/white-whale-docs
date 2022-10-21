# Terraswap Pair

The pair contract is the pool itself. Creating a new pool should be done via the pool factory, so that the pool is indexed 
in the pool registry stored by the factory. A pool can be created with native, ibc or cw20 tokens.

## Liquidity Provision

A user or bot can provide liquidity by sending a `provide_liquidity` message and withdraw liquidity with `withdraw_liquidity`. 
Whenever liquidity is deposited into a pool, special tokens known as liquidity (LP) tokens are minted to the provider's 
address, in proportion to how much liquidity it contributed to the pool. These tokens are a representation of a liquidity 
provider's contribution to a pool. Whenever a trade occurs, the `swap_fee` percentage, which is a parameter specified by 
the `PoolFee`, is distributed pro-rata to all LPs in the pool at the moment of the trade. To receive the underlying liquidity 
back, plus commission fees that were accrued while their liquidity was locked, LPs must burn their liquidity tokens, which 
is done via `withdraw_liquidity`.

## Fees

There are two types of fees associated to the pools, namely `swap_fee` and `protocol_fee`. The `swap_fee` remains in the 
pool, causing a permanent increase in the constant product K. The value of this permanently increased pool goes to all LPs.

The `protocol_fee` goes to the protocol, and it is to be collected by the Fee Collector contract of the Liquidity Hub. 
The protocol revenue is then distributed to WHALE stakers in the form of token buybacks.

## Feature toggle

Pools contain a feature toggle, containing the following properties: `withdrawals_enabled`, `deposits_enabled` and `swaps_enabled`. 
Those features are `ON by default, but could be changed via governance. They could be changed in different scenarios, the ones
we could envision include for example if a critical bug is found in a given feature, it could be shut down while is being 
fixed to avoid exploits. Additionally, if for example liquidity is desired to be migrated to another pool, deposits could 
be disabled to prevent bots or users to deposit liquidity in the pool.

The code for the pair contract can be found [here](https://github.com/White-Whale-Defi-Platform/migaloo-core/tree/main/contracts/liquidity_hub/pool-network/terraswap_pair).

--- 

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
    }
  },
  "fee_collector_addr": "juno1..."
}
```

| Key                  | Type           | Description                                                                         |
| -------------------- | -------------- | ----------------------------------------------------------------------------------- |
| `asset_infos`        | [AssetInfo; 2] | Information about the two assets                                                    |
| `token_code_id`      | u64            | Code if for the token contract. Used by the factory to create the LP token contract |
| `asset_decimals`     | [u8; 2]        | Decimal places for the given assets                                                 |
| `pool_fees`          | PoolFee        | Pool fees for the given pair                                                        |
| `fee_collector_addr` | String         | Fee collector contract address                                                      |

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

Provides liquidity to the pool. Note that in case of providing liquidity with a cw20 token, the message [increase_allowance](https://app.gitbook.com/o/fVZwd36itixTM6EMRcZt/s/PtAatYv3uVRxf7beAOPp/liquidity-hub/overview-1/terraswap-token#increase-allowance)
should be called on the cw20 token contract before you can transfer cw20 tokens to the pool.

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
| `assets`             | [Asset; 2]       | Assets to provide liquidity with                                                                          |
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
    "msg": "ewogICJzd2FwIjogewogICAgIm9mZmVyX2Fzc2V0IjogewogICAgICAiaW5mbyIgOiB7CiAgICAgICAgInRva2VuIjogewogICAgICAgICAgImNvbnRyYWN0X2FkZHIiOiAianVubzEuLi4iCiAgICAgICAgfQogICAgICB9LAogICAgICAiYW1vdW50IjogIjEwMDAiCiAgICB9CiAgfQp9"
  }
}
```
where `ewog....fQp9` is the following message, encoded in base64:

```json
{
  "swap": {
    "offer_asset": {
      "info" : {
        "token": {
          "contract_addr": "juno1..."
        }
      },
      "amount": "1000"
    },
    "belief_price": "0.3524",
    "max_spread": "0.05",
    "to": "to_address"
  }
}
```

Note that `contract_addr` in the swap message is the cw20 token address to be swapped.

| Key            | Type             | Description                                                            |
| -------------- | ---------------- | ---------------------------------------------------------------------- |
| `offer_asset`  | Asset            | Asset to swap                                                          |
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
  },
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

| Key               | Type           | Description                             |
| ----------------- | -------------- | --------------------------------------- |
| `asset_infos`     | [AssetInfo; 2] | Asset infos for the pair                |
| `contract_addr`   | String         | Pair contract address                   |
| `liquidity_token` | String         | LP token contract address for the pair  |
| `asset_decimals`  | [u8; 2]        | Decimals for the assets within the pool |


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

| Key           | Type       | Description                         |
| ------------- | ---------- | ----------------------------------- |
| `assets`      | [Asset; 2] | Assets within the pool              |
| `total_share` | Uint128    | Total supply of the pool's LP token |


{% endtab %}
{% endtabs %}

### Protocol fees

Retrieves the protocol fees on the pool. If `all_time` is `true`, it will return the fees collected since
the inception of the pool. On the other hand, if `all_time` is set to `false`, only the fees that has been accrued by
the pool but not collected by the fee collector will be returned.

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
  "protocol_fee_amount": "207"
}
```

| Key                   | Type    | Description                                                          |
| --------------------- | ------- | -------------------------------------------------------------------- |
| `return_amount`       | Uint128 | Amount that would be delivered to the user after the swap            |
| `spread_amount`       | Uint128 | Spread the swap would have                                           |
| `swap_fee_amount`     | Uint128 | Swap fees amount that would be distributed among liquidity providers |
| `protocol_fee_amount` | Uint128 | Protocol fees amount                                                 |

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
  "protocol_fee_amount": "1"
}
```

| Key                   | Type    | Description                                                          |
| --------------------- | ------- | -------------------------------------------------------------------- |
| `offer_amount`        | Uint128 | Offer asset amount that is needed to get the given ask asset         |
| `spread_amount`       | Uint128 | Spread the swap would have                                           |
| `swap_fee_amount`     | Uint128 | Swap fees amount that would be distributed among liquidity providers |
| `protocol_fee_amount` | Uint128 | Protocol fees amount                                                 |

{% endtab %}
{% endtabs %}
