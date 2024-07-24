# Pool Manager

The Pool Manager is a contract that handles liquidity pools in the White Whale DEX. It allows for the creation and
management of various types of liquidity pools, including constant product and stable swap pools and more. The contract
facilitates liquidity provision, token swaps, and multi-hop operations across different pools.

The Pool Manager enables permissionless creation of liquidity pools, requiring a fee to prevent spam. It supports
multiple pools for the same asset pair, each with a unique identifier. Users can provide liquidity, perform swaps, and
execute multi-hop operations across different pools. The contract manages pool creation, liquidity provision and
withdrawal, swaps, and maintains swap routes for efficient token exchanges.

## Instantiate

Instantiates an instance of the pool manager contract

```json
{
  "bonding_manager_addr": "migaloo1...",
  "incentive_manager_addr": "migaloo1...",
  "pool_creation_fee": {
    "denom": "uwhale",
    "amount": "1000000000"
  }
}
```

| Key                      | Type   | Description                             |
|--------------------------|--------|-----------------------------------------|
| `bonding_manager_addr`   | String | The bonding manager contract address.   |
| `incentive_manager_addr` | String | The incentive manager contract address. |
| `pool_creation_fee`      | Coin   | How much it costs to create a pool.     |

## ExecuteMsg

### CreatePool

Creates a new pool with the provided assets, their decimals for calculation fees, pool type and the identifier for a
pool.

Creation of pools in the pool manager is permissionless, but a fee must be paid to create a pool which is specified in
the contract configuration.
All pools and their information are stored in the one pool manager contract and any amount of pools with any variation
of assets can be created.

For example, two or more pools with the assets `uwhale` and `uusdc` can be created at anytime with different pool
identifiers. A good example is two pools, same assets different pool types (stableswap vs constant product) however any
variation is possible.

{% hint style="warning" %}
Note: In case of a pool being created on Osmosis, the `osmosis_fee` needs to be set to `0.001` as per the agreement
between
White Whale and Osmosis.
{% endhint %}

{% tabs %}
{% tab title="XYK Pool" %}

```json
    {
  "create_pool": {
    "asset_denoms": [
      "uwhale",
      "uusdc"
    ],
    "asset_decimals": [
      6,
      6
    ],
    "pool_fees": {
      "protocol_fee": {
        "share": "0.001"
      },
      "swap_fee": {
        "share": "0.002"
      },
      "burn_fee": {
        "share": "0"
      },
      "osmosis_fee": {
        "share": "0.001"
      },
      "extra_fees": [
        {
          "share": "0.001"
        }
      ]
    },
    "pool_type": "constant_product",
    "pool_identifier": "uwhale_uusdc_pool"
  }
}
```

{% endtab %}

{% tab title="Stableswap" %}

```json
    {
  "create_pool": {
    "asset_denoms": [
      "uusdt",
      "uusdc"
    ],
    "asset_decimals": [
      6,
      6
    ],
    "pool_fees": {
      "protocol_fee": {
        "share": "0.0002"
      },
      "swap_fee": {
        "share": "0.0003"
      },
      "burn_fee": {
        "share": "0"
      },
      "osmosis_fee": {
        "share": "0.001"
      },
      "extra_fees": []
    },
    "pool_type": {
      "stableswap": {
        "amp": 85
      }
    },
    "pool_identifier": "uusdt_uusdc_pool"
  }
}
```

{% endtab %}
{% endtabs %}

| Key               | Type            | Description                                                                                   |
|-------------------|-----------------|-----------------------------------------------------------------------------------------------|
| `asset_denoms`    | Vec\<String>    | The asset denoms for the pool.                                                                |
| `asset_decimals`  | Vec\<u8>        | The decimals for the given asset denoms, provided in the same order as `asset_denoms`.        |
| `pool_fees`       | PoolFee         | The fees for the pool.                                                                        |
| `pool_type`       | PoolType        | The type of pool to create. It can be either constant product or stableswap.                  |
| `pool_identifier` | Option\<String> | The identifier for the pool. If not set, a number (pool counter) will be assigned as pool id. |

### ProvideLiquidity

Provides liquidity to the pool specified by the `pool_identifier`.
Liquidity balances are stored on a per-pool basis in order to not
double count the assets of other pools with the same assets.

If `lock_position_identifier` is provided, the LP tokens will be locked in the incentive manager for the specified
duration.
Otherwise, the LP tokens will be sent to the receiver address.

The amount of liquidity to be provided is determined by the amount of assets provided in `info.funds`. If only one asset
is provided then a single sided liquidity provision will be attempted.

```json
    {
  "provide_liquidity": {
    "slippage_tolerance": "0.01",
    "max_spread": "0.1",
    "receiver": "migaloo1...",
    "pool_identifier": "uwhale_uusdc_pool",
    "unlocking_duration": 2678400,
    "lock_position_identifier": "lp_lock_identifier"
  }
}
```

| Key                        | Type             | Description                                                                                                                                                                                                                                                      |
|----------------------------|------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `slippage_tolerance`       | Option\<Decimal> | A percentage value representing the acceptable slippage for the operation. When provided, if the slippage exceeds this value, the liquidity provision will not be executed.                                                                                      |
| `max_spread`               | Option\<Decimal> | The decimals for the given asset denoms, provided in the same order as `asset_denoms`.  The maximum allowable spread between the bid and ask prices for the pool. When provided, if the spread exceeds this value, the liquidity provision will not be executed. | `pool_fees`       | PoolFee          | The fees for the pool                                                                                                                                                       |
| `receiver`                 | Option\<String>  | The receiver of the LP.                                                                                                                                                                                                                                          |
| `pool_identifier`          | String           | The identifier for the pool to provide liquidity for.                                                                                                                                                                                                            |
| `unlocking_duration`       | Option\<u64>     | The amount of time in seconds to unlock tokens if taking part on the incentives. If not passed, the tokens will not be locked and the LP tokens will be returned to the user.                                                                                    |
| `lock_position_identifier` | Option\<String>  | The identifier of the position to lock the LP tokens in the incentive manager, if any.                                                                                                                                                                           |

### Swap

Swaps an offer asset to another asset in the pool specified by the `pool_identifier`. By providing a pool identifier
when performing a swap, only the desired asset need be specified in the swap message
The amount to be swapped is provided in `info.funds`

```json
    {
  "swap": {
    "ask_asset_denom": "uusdc",
    "belief_price": "0.5",
    "max_spread": "5000",
    "receiver": "migaloo1...",
    "pool_identifier": "uwhale_uusdc_pool"
  }
}
```

| Key               | Type             | Description                                                                                                            |
|-------------------|------------------|------------------------------------------------------------------------------------------------------------------------|
| `ask_asset_denom` | String           | The return asset of the swap.                                                                                          |
| `belief_price`    | Option\<Decimal> | The belief price of the swap.                                                                                          |
| `max_spread`      | Option\<Decimal> | The maximum spread to incur when performing the swap. If the spread exceeds this value, the swap will not be executed. |
| `receiver`        | Option\<String>  | The recipient of the output tokens. If not provided, the tokens will be sent to the sender of the message.             |
| `pool_identifier` | String           | The identifier for the pool to swap in.                                                                                |

### WithdrawLiquidity

Withdraws liquidity from the pool specified by the `pool_identifier`. A withdrawal of liquidity will result in the
burning of any LP tokens that are returned as a part of the withdrawal. The LP token should be sent in the transaction.

```json
    {
  "withdraw_liquidity": {
    "pool_identifier": "uwhale_uusdc_pool"
  }
}
```

| Key               | Type   | Description                                   |
|-------------------|--------|-----------------------------------------------|
| `pool_identifier` | String | The identifier for the pool to withdraw from. |

### ExecuteSwapOperations

Execute multiple [`SwapOperations`] to allow for multi-hop swaps.

```json
    {
  "execute_swap_operations": {
    "operations": [
      {
        "whale_swap": {
          "token_in_denom": "uluna",
          "token_out_denom": "uwhale",
          "pool_identifier": "uluna_uwhale_pool"
        }
      },
      {
        "whale_swap": {
          "token_in_denom": "uwhale",
          "token_out_denom": "uusdc",
          "pool_identifier": "uwhale_uusdc_pool"
        }
      }
    ],
    "minimum_receive": "1000000",
    "receiver": "migaloo1...",
    "max_spread": "0.1"
  }
}
```

| Key               | Type                | Description                                                                                                                                                                                     |
|-------------------|---------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `operations`      | Vec\<SwapOperation> | The operations that should be performed in sequence. The amount in each swap will be the output from the previous swap. The first swap will use whatever funds are sent in the [`MessageInfo`]. |**
| `minimum_receive` | Option\<Uint128>    | The minimum amount of the output (i.e., final swap operation token) required for the message to succeed.                                                                                        |**
| `receiver`        | Option\<String>     | The (optional) recipient of the output tokens. If left unspecified, tokens will be sent to the sender of the message.                                                                           |**
| `max_spread`      | Option\<Decimal>    | The (optional) maximum spread to incur when performing any swap. Maximum 50%. If left unspecified, it will use the default max spread value from the contract.                                  |**

### AddSwapRoutes

Adds swap routes to the router. Once a Swap Route is added it can't be modified. It can however be removed by either the
creator of the route or the contract owner, added again if needed.

{% hint style="warning" %}
Note: This is needed so the buybacks can be done by the Bonding Manager correctly.
{% endhint %}

```json
    {
  "add_swap_routes": {
    "swap_routes": [
      {
        "offer_asset_denom": "uluna",
        "ask_asset_denom": "uwhale",
        "swap_operations": [
          {
            "whale_swap": {
              "token_in_denom": "uluna",
              "token_out_denom": "uwhale",
              "pool_identifier": "uluna_uwhale_pool"
            }
          }
        ]
      }
    ]
  }
}
```

| Key           | Type           | Description                             |
|---------------|----------------|-----------------------------------------|
| `swap_routes` | Vec\SwapRoute> | The swap routes to add to the contract. |

### RemoveSwapRoutes

Removes swap routes to the router. Only the creator of the route or the contract owner can remove a swap route.

```json
    {
  "remove_swap_routes": {
    "swap_routes": [
      {
        "offer_asset_denom": "uluna",
        "ask_asset_denom": "uwhale",
        "swap_operations": [
          {
            "whale_swap": {
              "token_in_denom": "uluna",
              "token_out_denom": "uwhale",
              "pool_identifier": "uluna_uwhale_pool"
            }
          }
        ]
      }
    ]
  }
}
```

| Key           | Type           | Description                                  |
|---------------|----------------|----------------------------------------------|
| `swap_routes` | Vec\SwapRoute> | The swap routes to remove from the contract. |

### UpdateConfig

Updates the configuration of the contract. If a field is not specified (i.e., set to `None`), it will not be modified.

```json
    {
  "update_config": {
    "bonding_manager_addr": "migaloo1...",
    "pool_creation_fee": {
      "denom": "uwhale",
      "amount": "1000000000"
    },
    "feature_toggle": {
      "withdrawals_enabled": true,
      "deposits_enabled": true,
      "swaps_enabled": true
    }
  }
}
```

| Key                    | Type                   | Description                                                                                             |
|------------------------|------------------------|---------------------------------------------------------------------------------------------------------|
| `bonding_manager_addr` | Option\<String>        | The new bonding-manager contract address.                                                               |
| `pool_creation_fee`    | Option\<Coin>          | The new fee that must be paid when a pool is created.                                                   |
| `feature_toggle`       | Option\<FeatureToggle> | The new feature toggles of the contract, allowing fine-tuned control over which operations are allowed. |

### UpdateOwnership(::cw_ownable::Action)

Implements `cw_ownable`. Updates the contract's ownership. `::cw_ownable::Action` can be `TransferOwnership`,
`AcceptOwnership` and `RenounceOwnership`.

{% tabs %}
{% tab title="TransferOwnership" %}

Propose to transfer the contract's ownership to another account, optionally with an expiry time. Can only be called by
the contract's current owner. Any existing pending ownership transfer is overwritten.

```json
    {
  "update_ownership": {
    "transfer_ownership": {
      "new_owner": "migaloo1...",
      "expiry": {
        "at_height": "424242424242"
      }
    }
  }
}
```

| Key         | Type                | Description                         |
|-------------|---------------------|-------------------------------------|
| `new_owner` | String              | The new owner proposed,             |
| `expiry`    | Option\<Expiration> | Optional expiration time parameter. |

{% endtab %}

{% tab title="AcceptOwnership" %}

Accept the pending ownership transfer. Can only be called by the pending owner.

```json
    {
  "update_ownership": {
    "accept_ownership": {}
  }
}
```

{% endtab %}

{% tab title="RenounceOwnership" %}

Give up the contract's ownership and the possibility of appointing a new owner. Can only be invoked by the contract's
current owner. Any existing pending ownership transfer is canceled.

```json
    {
  "update_ownership": {
    "renounce_ownership": {}
  }
}
```

{% endtab %}
{% endtabs %}

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
        "asset_denoms": [
          "uwhale",
          "uusdc"
        ],
        "lp_denom": "uwhale_uusdc_lp",
        "asset_decimals": [
          6,
          6
        ],
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