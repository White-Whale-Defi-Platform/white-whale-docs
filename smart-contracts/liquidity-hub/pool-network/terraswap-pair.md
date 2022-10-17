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

There are two types of fees associated to the pools, namely `swap_fee` and `protocol_fee`. The `swap_fee `remains in the 
pool, causing a permanent increase in the constant product K. The value of this permanently increased pool goes to all LPs.

The `protocol_fee` goes to the protocol, and it is to be collected by the Fee Collector contract of the Liquidity Hub. 
The protocol revenue is then distributed to WHALE stakers in the form of token buybacks.

## Feature toggle

Pools contain a feature toggle, containing the following properties: `withdrawals_enabled`, `deposits_enabled` and `swaps_enabled`. 
Those features are `ON by default, but could be changed via governance. They could changed in different scenarios, the once 
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

### Provide liquidity native/ibc

Provides liquidity for a pool with native or ibc tokens.

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
    ]
  }
}
```

### Provide liquidity cw20

Provides liquidity for a pool with cw20 tokens. Note that the message [increase_allowance](https://app.gitbook.com/o/fVZwd36itixTM6EMRcZt/s/PtAatYv3uVRxf7beAOPp/liquidity-hub/overview-1/terraswap-token#increase-allowance) 
should be called on the cw20 token before you can transfer cw20 tokens to the pool.

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
    ]
  }
}
```

### Swap native

Swaps a native token.

```json
{
  "swap": {
    "offer_asset": {
      "info" : {
        "native_token": {
          "denom": "ujuno"
        }
      },
      "amount": "1000"
    }
  }
}
```

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
    }
  }
}
```

Note that `contract_addr` in the swap message is the cw20 token address to be swapped.

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

{% tab title="Response" %}
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

{% tab title="Response" %}
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

{% tab title="Response" %}
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
{% endtab %}
{% endtabs %}

### Protocol fees

Retrieves the protocol fees on the pool. If `all_time` is `true`, it will return the fees collected since
the inception of the pool. On the other hand, if `all_time` is set to `false`, only the fees that has been accrued by
the pool but not collected by the fee collector will be returned.

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
{% endtab %}

{% tab title="Response" %}
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
{% endtab %}

{% tab title="Response" %}
```json
{
  "return_amount": "206395",
  "spread_amount": "1",
  "swap_fee_amount": "414",
  "protocol_fee_amount": "207"
}
```
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
{% endtab %}

{% tab title="Response" %}
```json
{
  "offer_amount": "207639",
  "spread_amount": "0",
  "swap_fee_amount": "2",
  "protocol_fee_amount": "1"
}
```
{% endtab %}
{% endtabs %}
