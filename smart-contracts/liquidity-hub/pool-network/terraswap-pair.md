# Terraswap Pair

The pair contract is the pool itself. This contract is used by the factory to spawn new pools as needed, so no
need to create pools manually. Also, the pool factory is an integral part of the Liquidity Hub, so you must use it
for creating pools for a correct functioning of the protocol.

The following are the messages that can be executed on the pair contract:

## Instantiate

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

```json
{}
```

## ExecuteMsg

### Collect protocol fees

```json
{
  "collect_protocol_fees": {}
}
```

### Provide liquidity cw20

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

### Provide liquidity native/ibc

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

### Swap native

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

### Swap cw20 (to be sent to the cw20 token contract address)

```json
{
  "send": {
    "contract": "juno1...",
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

### Update config

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

```json 
{
  "send": {
    "contract": "pair_contract_address",
    "amount": "1000",
    "msg": "ewogICJ3aXRoZHJhd19saXF1aWRpdHkiOiB7fQp9"
  },
}
```

where `ewogICJ3...kiOiB7fQp9` is the following message, encoded in base64:

```json 
{
  "withdraw_liquidity": {}
}
```

## Queries

### Config

```json 
{
  "config": {}
}
```

### Pair

```json 
{
  "pair": {}
}
```

### Pool

```json 
{
  "pool": {}
}
```

### Protocol fees

```json 
{
  "protocol_fees": {
    "asset_id": "ujuno",
    "all_time": false
  }
}
```

### Reserve simulation (native)

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

### Reserve simulation (cw20)

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

### Simulation (native)

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

### Simulation (cw20)

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

## Query responses


### Config

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

### Pair

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

### Pool

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

### Protocol fees

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

### Reverse simulation

```json 
{
  "offer_amount": "207639",
  "spread_amount": "0",
  "swap_fee_amount": "2",
  "protocol_fee_amount": "1"
}
```

### Simulation

```json 
{
  "return_amount": "206395",
  "spread_amount": "1",
  "swap_fee_amount": "414",
  "protocol_fee_amount": "207"
}
```