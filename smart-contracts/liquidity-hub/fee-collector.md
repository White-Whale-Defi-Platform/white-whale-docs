# Fee Collector

The local fee collector collects the fees for usage of the pool and vault network on a specific blockchain. Part of the
collected fees goes back to the depositors of the White Whale pools and/or the single asset flash loan vaults. The
remainder is sent to the interchain collector as protocol revenue. The protocol revenue is then distributed to WHALE
stakers in the form of token buybacks.

The code for the fee collector contract can be
found [here](https://github.com/White-Whale-Defi-Platform/migaloo-core/tree/main/contracts/liquidity_hub/fee_collector).

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
            "address": "terra1...",
            "contract_type": {
              "vault": {}
            }
          },
          {
            "address": "terra1...",
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
| ------------------ | -------------- |------------------------------------------------------------------|
| `collect_fees_for` | CollectFeesFor | Enum specifiying to collect fees for either Contracts or Factory |
| `contracts`        | Vec<Contract>  | Contracts to collect fees from                                   |

{% endtab %}

{% tab title="Pool fees" %}

```json
{
  "collect_fees": {
    "collect_fees_for": {
      "factory": {
        "factory_addr": "terra1...",
        "factory_type": {
          "pool": {}
        }
      }
    }
  }
}
```

| Key                | Type           | Description                                                      |
| ------------------ | -------------- | ---------------------------------------------------------------- |
| `collect_fees_for` | CollectFeesFor | Enum specifiying to collect fees for either Contracts or Factory |
| `factory`          | Factory        | Factory data to collect fees from                                |

{% endtab %}

{% tab title="Vault fees" %}

```json
{
  "collect_fees": {
    "collect_fees_for": {
      "factory": {
        "factory_addr": "terra1...",
        "factory_type": {
          "vault": {}
        }
      }
    }
  }
}
```

| Key                | Type           | Description                                                      |
| ------------------ | -------------- | ---------------------------------------------------------------- |
| `collect_fees_for` | CollectFeesFor | Enum specifiying to collect fees for either Contracts or Factory |
| `factory`          | Factory        | Factory data to collect fees from                                |

{% endtab %}
{% endtabs %}

### Update config

Updates the configuration of the fee collector.

```json
{
  "update_config": {
    "owner": "terra1..."
  }
}
```

| Key     | Type           | Description               |
| ------- | -------------- | ------------------------- |
| `owner` | Option<String> | New owner of the contract |

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

{% tab title="Response" %}

```json
{
  "owner": "terra1..."
}
```

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
            "address": "terra1...",
            "contract_type": {
              "pool": {}
            }
          },
          {
            "address": "terra1...",
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

| Key              | Type          | Description                                                   |
| ---------------- | ------------- | ------------------------------------------------------------- |
| `query_fees_for` | QueryFeesFor  | Enum specifying to query fees for either Contracts or Factory |
| `contracts`      | Vec<Contract> | Contracts to query fees from                                  |
| `all_time`       | Option<bool>  | New owner of the contract                                     |

{% endtab %}

{% tab title="Query Pools Fees" %}

```json
{
  "fees": {
    "query_fees_for": {
      "factory": {
        "factory_addr": "terra1...",
        "factory_type": {
          "pool": {}
        }
      }
    },
    "all_time": false
  }
}
```

| Key              | Type         | Description                                                   |
|------------------|--------------|---------------------------------------------------------------|
| `query_fees_for` | QueryFeesFor | Enum specifying to query fees for either Contracts or Factory |
| `factory`        | Factory      | Factory data to query fees from                               |
| `all_time`       | Option<bool> | New owner of the contract                                     |

{% endtab %}

{% tab title="Query Vaults Fees" %}

```json
{
  "fees": {
    "query_fees_for": {
      "factory": {
        "factory_addr": "terra1...",
        "factory_type": {
          "vault": {}
        }
      }
    },
    "all_time": false
  }
}
```

| Key              | Type         | Description                                                   |
|------------------|--------------|---------------------------------------------------------------|
| `query_fees_for` | QueryFeesFor | Enum specifying to query fees for either Contracts or Factory |
| `factory`        | Factory      | Factory data to query fees from                               |
| `all_time`       | Option<bool> | New owner of the contract                                     |

{% endtab %}

{% tab title="Response" %}

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
    "info": {
      "token": {
        "contract_addr": "terra1..."
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

{% endtab %}
{% endtabs %}
