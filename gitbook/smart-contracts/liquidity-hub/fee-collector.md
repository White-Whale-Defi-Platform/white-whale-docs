# Fee Collector

The local fee collector collects the fees for usage of the pool and vault network on a specific blockchain. Part of the
collected fees goes back to the depositors of the White Whale pools and/or the single asset flash loan vaults. The
remainder is sent to the interchain collector as protocol revenue. The protocol revenue is then distributed to WHALE
stakers in the form of token buybacks.

The code for the fee collector contract can be
found [here](https://github.com/White-Whale-Defi-Platform/white-whale-core/tree/main/contracts/liquidity_hub/fee_collector).

---

The following are the messages that can be executed on the fee collector:

## Instantiate

Instantiates the fee collector.

```json
{}
```

## Migrate

Migrates the fee collector.

```json
{}
```

## ExecuteMsg

### Collect fees

Collects the fees accrued by the pools or vaults. It can be triggered in different ways:

- Fees can be collected for specific contracts, specifying the address and contract type (pool or vault)
- Fees can be collected for pools, specifying the pool factory address and factory type (pool)
- Fees can be collected for vaults, specifying the vault factory address and factory type (vault)

{% tabs %}
{% tab title="Contract fees" %}

```json
{
  "collect_fees": {
    "collect_fees_for": {
      "contracts": {
        "contracts": [
          {
            "address": "migaloo1...",
            "contract_type": {
              "vault": {}
            }
          },
          {
            "address": "migaloo1...",
            "contract_type": {
              "pool": {}
            }
          }
        ]
      }
    }
  }
}
```

| Key                | Type           | Description                                                      |
|--------------------|----------------|------------------------------------------------------------------|
| `collect_fees_for` | FeesFor        | Enum specifiying to collect fees for either Contracts or Factory |
| `contracts`        | Vec\<Contract> | Contracts to collect fees from                                   |

{% endtab %}

{% tab title="Pool fees" %}

```json
{
  "collect_fees": {
    "collect_fees_for": {
      "factory": {
        "factory_addr": "migaloo1...",
        "factory_type": {
          "pool": {}
        }
      }
    }
  }
}
```

| Key                | Type    | Description                                                      |
|--------------------|---------|------------------------------------------------------------------|
| `collect_fees_for` | FeesFor | Enum specifiying to collect fees for either Contracts or Factory |
| `factory`          | Factory | Factory data to collect fees from                                |

{% endtab %}

{% tab title="Vault fees" %}

```json
{
  "collect_fees": {
    "collect_fees_for": {
      "factory": {
        "factory_addr": "migaloo1...",
        "factory_type": {
          "vault": {}
        }
      }
    }
  }
}
```

| Key                | Type    | Description                                                      |
|--------------------|---------|------------------------------------------------------------------|
| `collect_fees_for` | FeesFor | Enum specifiying to collect fees for either Contracts or Factory |
| `factory`          | Factory | Factory data to collect fees from                                |

{% endtab %}
{% endtabs %}

### Update config

Updates the configuration of the fee collector.

```json
{
  "update_config": {
    "owner": "migaloo1...",
    "pool_router": "migaloo1...",
    "fee_distributor": "migaloo1...",
    "pool_factory": "migaloo1...",
    "vault_factory": "migaloo1..."
  }
}
```

| Key               | Type            | Description                  |
|-------------------|-----------------|------------------------------|
| `owner`           | Option\<String> | New owner of the contract    |
| `pool_router`     | Option\<String> | New pool router contract     |
| `fee_distributor` | Option\<String> | New fee distributor contract |
| `pool_factory`    | Option\<String> | New pool factory contract    |
| `vault_factory`   | Option\<String> | New vault factory contract   |

### Aggregate fees

Aggregates the fees in the fee collector.

{% tabs %}
{% tab title="Pool fees" %}

```json
{
  "aggregate_fees": {
    "aggregate_fees_for": {
      "factory": {
        "factory_addr": "migaloo1...",
        "factory_type": {
          "pool": {}
        }
      }
    }
  }
}
```

| Key                  | Type    | Description                                                      |
|----------------------|---------|------------------------------------------------------------------|
| `aggregate_fees_for` | FeesFor | Enum specifiying to collect fees for either Contracts or Factory |
| `factory`            | Factory | Factory data to collect fees from                                |

{% endtab %}

{% tab title="Vault fees" %}

```json
{
  "aggregate_fees": {
    "aggregate_fees_for": {
      "factory": {
        "factory_addr": "migaloo1...",
        "factory_type": {
          "vault": {}
        }
      }
    }
  }
}
```

| Key                  | Type    | Description                                                      |
|----------------------|---------|------------------------------------------------------------------|
| `aggregate_fees_for` | FeesFor | Enum specifiying to collect fees for either Contracts or Factory |
| `factory`            | Factory | Factory data to collect fees from                                |

{% endtab %}
{% tab title="Contract fees" %}

```json
{
  "aggregate_fees": {
    "aggregate_fees_for": {
      "contracts": {
        "contracts": [
          {
            "address": "migaloo1...",
            "contract_type": {
              "vault": {}
            }
          },
          {
            "address": "migaloo1...",
            "contract_type": {
              "pool": {}
            }
          }
        ]
      }
    }
  }
}
```

| Key                  | Type           | Description                                                      |
|----------------------|----------------|------------------------------------------------------------------|
| `aggregate_fees_for` | FeesFor        | Enum specifiying to collect fees for either Contracts or Factory |
| `contracts`          | Vec\<Contract> | Contracts to collect fees from                                   |

{% endtab %}
{% endtabs %}

### Forward fees

Forward fees to the fee distributor. This is called when creating a new epoch on the fee distributor. this will collect
and aggregate the fees, to send them back to the fee distributor.

{% hint style="warning" %}
Note: can only be called by the owner of the contract or the fee distributor.
{% endhint %}

```json
{
  "forward_fees": {
    "epoch": {
      "id": "1",
      "start_time": "1698851118",
      "total": [
        {
          "amount": "1000",
          "info": {
            "native_token": {
              "denom": "uwhale"
            }
          }
        }
      ],
      "available": [
        {
          "amount": "300",
          "info": {
            "native_token": {
              "denom": "uwhale"
            }
          }
        }
      ],
      "claimed": [
        {
          "amount": "700",
          "info": {
            "native_token": {
              "denom": "uwhale"
            }
          }
        }
      ],
      "global_index": {
        "bonded_amount": "3000",
        "bonded_assets": [
          {
            "info": {
              "native_token": {
                "denom": "ampWHALE"
              }
            },
            "amount": "1500"
          },
          {
            "info": {
              "native_token": {
                "denom": "bWHALE"
              }
            },
            "amount": "1500"
          }
        ],
        "timestamp": "1698851118",
        "weight": "1500000"
      }
    },
    "forward_fees_as": {
      "native_token": {
        "denom": "uwhale"
      }
    }
  }
}
```

| Key               | Type      | Description                                                                                                              |
|-------------------|-----------|--------------------------------------------------------------------------------------------------------------------------|
| `epoch`           | Epoch     | Epoch to be created once the msg is succesful. This variable is prebuilt on the fee distributor when calling `new_epoch` |
| `forward_fees_as` | AssetInfo | The asset to forward fees as. Currently not used, value taken from the fee distributor config.                           |

## Queries

### Config

Retrieves the configuration of the contract in a `Config` response.

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
  "owner": "migaloo1...",
  "pool_router": "migaloo1...",
  "fee_distributor": "migaloo1...",
  "pool_factory": "migaloo1...",
  "vault_factory": "migaloo1..."
}
```

| Key               | Type | Description              |
|-------------------|------|--------------------------|
| `owner`           | Addr | Address of the owner     |
| `pool_router`     | Addr | Pool router contract     |
| `fee_distributor` | Addr | Fee distributor contract |
| `pool_factory`    | Addr | Pool factory contract    |
| `vault_factory`   | Addr | Vault factory contract   |

{% endtab %}
{% endtabs %}

### Fees

Queries the fees collected by individual contracts, whether they are pools or vaults. Additionally, it can query the
fees collected by a given pool or vault factory's children.

{% tabs %}
{% tab title="Query Contracts Fees" %}

```json
{
  "fees": {
    "query_fees_for": {
      "contracts": {
        "contracts": [
          {
            "address": "migaloo1...",
            "contract_type": {
              "pool": {}
            }
          },
          {
            "address": "migaloo1...",
            "contract_type": {
              "vault": {}
            }
          }
        ]
      }
    },
    "all_time": true
  }
}
```

| Key              | Type           | Description                                                                                                                                                                                                                      |
|------------------|----------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `query_fees_for` | QueryFeesFor   | Enum specifying to query fees for either Contracts or Factory                                                                                                                                                                    |
| `contracts`      | Vec\<Contract> | Contracts to query fees from                                                                                                                                                                                                     |
| `all_time`       | Option\<bool>  | If `true`, it will return the fees collected since the inception of the pool/vault. On the other hand, if `false`, only the fees that has been accrued by the pool/vault but not collected by the fee collector will be returned |

{% endtab %}

{% tab title="Query Pools Fees" %}

```json
{
  "fees": {
    "query_fees_for": {
      "factory": {
        "factory_addr": "migaloo1...",
        "factory_type": {
          "pool": {}
        }
      }
    },
    "all_time": false
  }
}
```

| Key              | Type          | Description                                                                                                                                                                                                                      |
|------------------|---------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `query_fees_for` | QueryFeesFor  | Enum specifying to query fees for either Contracts or Factory                                                                                                                                                                    |
| `factory`        | Factory       | Factory data to query fees from                                                                                                                                                                                                  |
| `all_time`       | Option\<bool> | If `true`, it will return the fees collected since the inception of the pool/vault. On the other hand, if `false`, only the fees that has been accrued by the pool/vault but not collected by the fee collector will be returned |

{% endtab %}

{% tab title="Query Vaults Fees" %}

```json
{
  "fees": {
    "query_fees_for": {
      "factory": {
        "factory_addr": "migaloo1...",
        "factory_type": {
          "vault": {}
        }
      }
    },
    "all_time": false
  }
}
```

| Key              | Type          | Description                                                                                                                                                                                                                      |
|------------------|---------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `query_fees_for` | QueryFeesFor  | Enum specifying to query fees for either Contracts or Factory                                                                                                                                                                    |
| `factory`        | Factory       | Factory data to query fees from                                                                                                                                                                                                  |
| `all_time`       | Option\<bool> | If `true`, it will return the fees collected since the inception of the pool/vault. On the other hand, if `false`, only the fees that has been accrued by the pool/vault but not collected by the fee collector will be returned |

{% endtab %}

{% tab title="Response (Vec<Asset>)" %}

```json
[
  {
    "info": {
      "native_token": {
        "denom": "ujuno"
      }
    },
    "amount": "250050890"
  },
  {
    "Asset": {
      "token": {
        "contract_addr": "migaloo1..."
      }
    },
    "amount": "19610016"
  },
  {
    "info": {
      "native_token": {
        "denom": "ibc/C4CFF46FD6DE35CA4CF4CE031E643C8FDC9BA4B99AE598E9B0ED98FE3A2319F9"
      }
    },
    "amount": "15905454"
  }
]
```

| Key      | Type      | Description                                                   |
|----------|-----------|---------------------------------------------------------------|
| `info`   | AssetInfo | Enum specifying whether the asset is native/ibc or cw20 token |
| `amount` | Uint128   | Asset amount                                                  |

{% endtab %}
{% endtabs %}
