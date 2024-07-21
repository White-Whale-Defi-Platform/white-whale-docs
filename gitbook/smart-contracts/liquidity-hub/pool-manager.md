# Pool Manager

## Instantiate

Instantiates an instance of the pool manager contract

```json
{
  "bonding_manager_addr": "migaloo1...",
  "incentive_manager_addr": "migaloo1...",
  "pool_creation_fee": {
    "denom": "uwhale",
    "amount": "1000000"
  }
}
```

| Key                      | Type   | Description                                               |
|--------------------------|--------|-----------------------------------------------------------|
| `bonding_manager_addr`   | String | The address of the bonding manager contract               |
| `incentive_manager_addr` | String | The address of the incentive manager contract             |
| `pool_creation_fee`      | Coin   | The fee required to create a new pool (prevents spamming) |

## ExecuteMsg

### CreatePool

Creates a new pool with the provided assets, their decimals for calculation fees, pool type and the identifier for a pool.
 
Creation of pools in the pool manager is permissionless, but a fee must be paid to create a pool which is specified in the contract configuration.
All pools and their information is stored in the one pool manager contract and any amount of pools with any variation of assets can be created. 

For example, two or more pools with the assets `uwhale` and `uusdc` can be created at anytime with different pool identifiers. A good example is two pools, same assets different pool types (stableswap vs constant product) however any variation is possible. 

```json
{
  "create_pool": {
    "asset_denoms": ["uwhale", "uusdc"],
    "asset_decimals": [6, 6],
    "pool_fees": {
      "protocol_fee": "0.003",
      "swap_fee": "0.003",
      "burn_fee": "0.0"
    },
    "pool_type": {
      "constant_product": {}
    },
    "pool_identifier": "whale-usdc-1"
  }
}
```

| Key                | Type                   | Description                                                                |
|--------------------|------------------------|----------------------------------------------------------------------------|
| `asset_denoms`     | Vec<String>            | The asset denoms for the pool                                              |
| `asset_decimals`   | Vec<u8>                | The decimals for the given asset denoms, in the same order as asset_denoms |
| `pool_fees`        | PoolFee                | The fees for the pool                                                      |
| `pool_type`        | PoolType               | The type of pool to create (ConstantProduct or StableSwap)                 |
| `pool_identifier`  | Option<String>         | The identifier for the pool (optional)                                     |

### ProvideLiquidity

Provides liquidity to the pool specified by the `pool_identifier`.
Liquidity balances are stored on a per-pool basis in order to not 
double count the assets of other pools with the same assets. 

If lock_position_identifier is provided, the LP tokens will be locked in the incentive manager for the specified duration.
Otherwise, the LP tokens will be sent to the receiver address.

The amount of liquidity to be provided is determined by the amount of assets provided in `info.funds`. If only one asset is provided then a single sided liquidity provision will be attempted.

```json
{
  "provide_liquidity": {
    "slippage_tolerance": "0.01",
    "max_spread": "0.05",
    "receiver": "migaloo1...",
    "pool_identifier": "whale-usdc-1",
    "unlocking_duration": 1209600,
    "lock_position_identifier": "position-1"
  }
}
```

| Key                        | Type           | Description                                                          |
|----------------------------|----------------|----------------------------------------------------------------------|
| `slippage_tolerance`       | Option<Decimal> | Maximum acceptable slippage for the operation                        |
| `max_spread`               | Option<Decimal> | Maximum allowable spread between bid and ask prices                  |
| `receiver`                 | Option<String>  | The receiver of the LP tokens (if different from sender)             |
| `pool_identifier`          | String         | The identifier for the pool to provide liquidity for                 |
| `unlocking_duration`       | Option<u64>    | Time in seconds to unlock tokens if participating in incentives      |
| `lock_position_identifier` | Option<String>  | Identifier of the position to lock LP tokens in incentive manager    |

### Swap

Swaps an offer asset to another asset in the pool specified by the `pool_identifier`. By providing a pool identifier when performing a swap, only the desired asset need be specified in the swap message
The amount to be swapped is provided in `info.funds` 

```json
{
  "swap": {
    "ask_asset_denom": "uusdc",
    "belief_price": "1.01",
    "max_spread": "0.05",
    "receiver": "migaloo1...",
    "pool_identifier": "whale-usdc-1"
  }
}
```

| Key                | Type           | Description                                                   |
|--------------------|----------------|---------------------------------------------------------------|
| `ask_asset_denom`  | String         | The denom of the asset to receive                              |
| `belief_price`     | Option<Decimal> | The belief price of the swap                                  |
| `max_spread`       | Option<Decimal> | Maximum spread to incur when performing the swap              |
| `receiver`         | Option<String>  | The recipient of the output tokens (if different from sender) |
| `pool_identifier`  | String         | The identifier for the pool to swap in                        |

### WithdrawLiquidity

Withdraws liquidity from the pool specified by the `pool_identifier`. A withdrawal of liquidity will result in the burning of any LP tokens that are returned as a part of the withdrawal.

```json
{
  "withdraw_liquidity": {
    "pool_identifier": "whale-usdc-1"
  }
}
```

| Key               | Type   | Description                                    |
|-------------------|--------|------------------------------------------------|
| `pool_identifier` | String | The identifier for the pool to withdraw from   |

### ExecuteSwapOperations

Executes multiple swap operations to allow for multi-hop swaps.

```json
{
  "execute_swap_operations": {
    "operations": [
      {
        "whale_swap": {
          "token_in_denom": "uwhale",
          "token_out_denom": "uusdc",
          "pool_identifier": "whale-usdc-1"
        }
      },
      {
        "whale_swap": {
          "token_in_denom": "uusdc",
          "token_out_denom": "uatom",
          "pool_identifier": "usdc-atom-1"
        }
      }
    ],
    "minimum_receive": "1000000",
    "receiver": "migaloo1...",
    "max_spread": "0.05"
  }
}
```

| Key                | Type                  | Description                                                   |
|--------------------|------------------------|---------------------------------------------------------------|
| `operations`       | Vec<SwapOperation>     | The sequence of swap operations to perform                    |
| `minimum_receive`  | Option<Uint128>        | Minimum amount of output token required for success           |
| `receiver`         | Option<String>         | The recipient of the output tokens (if different from sender) |
| `max_spread`       | Option<Decimal>        | Maximum spread to incur when performing any swap              |

### AddSwapRoutes

Adds swap routes to the router.

```json
{
  "add_swap_routes": {
    "swap_routes": [
      {
        "offer_asset_denom": "uwhale",
        "ask_asset_denom": "uatom",
        "swap_operations": [
          {
            "whale_swap": {
              "token_in_denom": "uwhale",
              "token_out_denom": "uusdc",
              "pool_identifier": "whale-usdc-1"
            }
          },
          {
            "whale_swap": {
              "token_in_denom": "uusdc",
              "token_out_denom": "uatom",
              "pool_identifier": "usdc-atom-1"
            }
          }
        ]
      }
    ]
  }
}
```

| Key           | Type           | Description                        |
|---------------|----------------|------------------------------------|
| `swap_routes` | Vec<SwapRoute> | The swap routes to add to the router |

### RemoveSwapRoutes

Removes swap routes from the router.

```json
{
  "remove_swap_routes": {
    "swap_routes": [
      {
        "offer_asset_denom": "uwhale",
        "ask_asset_denom": "uatom",
        "swap_operations": [
          {
            "whale_swap": {
              "token_in_denom": "uwhale",
              "token_out_denom": "uusdc",
              "pool_identifier": "whale-usdc-1"
            }
          },
          {
            "whale_swap": {
              "token_in_denom": "uusdc",
              "token_out_denom": "uatom",
              "pool_identifier": "usdc-atom-1"
            }
          }
        ]
      }
    ]
  }
}
```

| Key           | Type           | Description                           |
|---------------|----------------|---------------------------------------|
| `swap_routes` | Vec<SwapRoute> | The swap routes to remove from the router |

### UpdateConfig

Updates the configuration of the contract.

```json
{
  "update_config": {
    "bonding_manager_addr": "migaloo1...",
    "pool_creation_fee": {
      "denom": "uwhale",
      "amount": "2000000"
    },
    "feature_toggle": {
      "withdrawals_enabled": true,
      "deposits_enabled": true,
      "swaps_enabled": true
    }
  }
}
```

| Key                    | Type                  | Description                                           |
|------------------------|------------------------|-------------------------------------------------------|
| `bonding_manager_addr` | Option<String>         | The new bonding-manager contract address              |
| `pool_creation_fee`    | Option<Coin>           | The new fee that must be paid when a pool is created  |
| `feature_toggle`       | Option<FeatureToggle>  | The new feature toggles of the contract               |

## QueryMsg

### Config

Returns the configuration of the contract.

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
  "config": {
    "bonding_manager_addr": "migaloo1...",
    "incentive_manager_addr": "migaloo1...",
    "pool_creation_fee": {
      "denom": "uwhale",
      "amount": "1000000"
    },
    "feature_toggle": {
      "withdrawals_enabled": true,
      "deposits_enabled": true,
      "swaps_enabled": true
    }
  }
}
```
{% endtab %}
{% endtabs %}

### AssetDecimals

Retrieves the decimals for the given asset in a specific pool.

{% tabs %}
{% tab title="Query" %}
```json
{
  "asset_decimals": {
    "pool_identifier": "whale-usdc-1",
    "denom": "uwhale"
  }
}
```
{% endtab %}

{% tab title="Response (AssetDecimalsResponse)" %}
```json
{
  "pool_identifier": "whale-usdc-1",
  "denom": "uwhale",
  "decimals": 6
}
```
{% endtab %}
{% endtabs %}

### Simulation

Simulates a swap.

{% tabs %}
{% tab title="Query" %}
```json
{
  "simulation": {
    "offer_asset": {
      "denom": "uwhale",
      "amount": "1000000"
    },
    "ask_asset_denom": "uusdc",
    "pool_identifier": "whale-usdc-1"
  }
}
```
{% endtab %}

{% tab title="Response (SimulationResponse)" %}
```json
{
  "return_amount": "990000",
  "spread_amount": "5000",
  "swap_fee_amount": "3000",
  "protocol_fee_amount": "2000",
  "burn_fee_amount": "0"
}
```
{% endtab %}
{% endtabs %}

### ReverseSimulation

Simulates a reverse swap.

{% tabs %}
{% tab title="Query" %}
```json
{
  "reverse_simulation": {
    "ask_asset": {
      "denom": "uusdc",
      "amount": "990000"
    },
    "offer_asset_denom": "uwhale",
    "pool_identifier": "whale-usdc-1"
  }
}
```
{% endtab %}

{% tab title="Response (ReverseSimulationResponse)" %}
```json
{
  "offer_amount": "1000000",
  "spread_amount": "5000",
  "swap_fee_amount": "3000",
  "protocol_fee_amount": "2000",
  "burn_fee_amount": "0"
}
```
{% endtab %}
{% endtabs %}

### SwapRoute

Gets the swap route for the given offer and ask assets.

{% tabs %}
{% tab title="Query" %}
```json
{
  "swap_route": {
    "offer_asset_denom": "uwhale",
    "ask_asset_denom": "uatom"
  }
}
```
{% endtab %}

{% tab title="Response (SwapRouteResponse)" %}
```json
{
  "swap_route": {
    "offer_asset_denom": "uwhale",
    "ask_asset_denom": "uatom",
    "swap_operations": [
      {
        "whale_swap": {
          "token_in_denom": "uwhale",
          "token_out_denom": "uusdc",
          "pool_identifier": "whale-usdc-1"
        }
      },
      {
        "whale_swap": {
          "token_in_denom": "uusdc",
          "token_out_denom": "uatom",
          "pool_identifier": "usdc-atom-1"
        }
      }
    ]
  }
}
```
{% endtab %}
{% endtabs %}

### SwapRoutes

Gets all registered swap routes.

{% tabs %}
{% tab title="Query" %}
```json
{
  "swap_routes": {}
}
```
{% endtab %}

{% tab title="Response (SwapRoutesResponse)" %}
```json
{
  "swap_routes": [
    {
      "offer_asset_denom": "uwhale",
      "ask_asset_denom": "uatom",
      "swap_operations": [
        {
          "whale_swap": {
            "token_in_denom": "uwhale",
            "token_out_denom": "uusdc",
            "pool_identifier": "whale-usdc-1"
          }
        },
        {
          "whale_swap": {
            "token_in_denom": "uusdc",
            "token_out_denom": "uatom",
            "pool_identifier": "usdc-atom-1"
          }
        }
      ]
    }
  ]
}
```
{% endtab %}
{% endtabs %}

### SimulateSwapOperations

Simulates swap operations.

{% tabs %}
{% tab title="Query" %}
```json
{
  "simulate_swap_operations": {
    "offer_amount": "1000000",
    "operations": [
      {
        "whale_swap": {
          "token_in_denom": "uwhale",
          "token_out_denom": "uusdc",
          "pool_identifier": "whale-usdc-1"
        }
      },
      {
        "whale_swap": {
          "token_in_denom": "uusdc",
          "token_out_denom": "uatom",
          "pool_identifier": "usdc-atom-1"
        }
      }
    ]
  }
}
```
{% endtab %}

{% tab title="Response (SimulateSwapOperationsResponse)" %}
```json
{
  "amount": "980000"
}
```
{% endtab %}
{% endtabs %}

### ReverseSimulateSwapOperations

Simulates reverse swap operations.

{% tabs %}
{% tab title="Query" %}
```json
{
  "reverse_simulate_swap_operations": {
    "ask_amount": "980000",
    "operations": [
      {
        "whale_swap": {
          "token_in_denom": "uwhale",
          "token_out_denom": "uusdc",
          "pool_identifier": "whale-usdc-1"
        }
      },
      {
        "whale_swap": {
          "token_in_denom": "uusdc",
          "token_out_denom": "uatom",
          "pool_identifier": "usdc-atom-1"
        }
      }
    ]
  }
}
```
{% endtab %}

{% tab title="Response (ReverseSimulateSwapOperationsResponse)" %}
```json
{
  "amount": "1000000"
}
```
{% endtab %}
{% endtabs %}

### Pools

Retrieves the pool information for the given pool identifier or all pools.

{% tabs %}
{% tab title="Query" %}
```json
{
  "pools": {
    "pool_identifier": "whale-usdc-1",
    "start_after": null,
    "limit": 10
  }
}
```
{% endtab %}

{% tab title="Response (PoolsResponse)" %}
```json
{
  "pools": [
    {
      "pool_info": {
        "pool_identifier": "whale-usdc-1",
        "asset_denoms": ["uwhale", "uusdc"],
        "lp_denom": "uwhale_uusdc_lp",
        "asset_decimals": [6, 6],
        "assets": [
          {
            "denom": "uwhale",
            "amount": "1000000"
          },
          {
            "denom": "uusdc",
            "amount": "1000000"
          }
        ],
        "pool_type": {
          "constant_product": {}
        },
        "pool_fees": {
          "protocol_fee": "0.003",
          "swap_fee": "0.003",
          "burn_fee": "0.0"
        }
      },
      "total_share": {
        "denom": "uwhale_uusdc_lp",
        "amount": "1000000"
      }
    }
  ]
}
```
{% endtab %}
{% endtabs %}

### SwapRouteCreator

Retrieves the creator of the swap route to get from offer to ask asset.

{% tabs %}
{% tab title="Query" %}
```json
{
  "swap_route_creator": {
    "offer_asset_denom": "uwhale",
    "ask_asset_denom": "uatom"
  }
}
```
{% endtab %}

{% tab title="Response (SwapRouteCreatorResponse)" %}
```json
{
  "creator": "migaloo1..."
}
```
{% endtab %}
{% endtabs %}