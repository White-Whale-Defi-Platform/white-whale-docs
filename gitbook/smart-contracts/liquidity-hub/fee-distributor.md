# Fee Distributor

The Fee Distributor is responsible for distributing the protocol fees collected by the Fee Collector to the various
stakeholders of the protocol.

## InstantiateMsg

```json
{
  "bonding_contract_addr": "migaloo1...",
  "distribution_asset": {
    "native_token": {
      "denom": "uwhale"
    }
  },
  "epoch_config": {
    "duration": "86400000000000",
    "genesis_epoch": "1698851118000000000"
  },
  "fee_collector_addr": "migaloo1...",
  "grace_period": "21"
}
```

| Key                     | Type        | Description                                                                                                                             |
|-------------------------|-------------|-----------------------------------------------------------------------------------------------------------------------------------------|
| `bonding_contract_addr` | String      | Whale Lair contract address                                                                                                             |
| `distribution_asset`    | AssetInfo   | The asset to be distributed                                                                                                             |
| `epoch_config`          | EpochConfig | The configuration for the epoch                                                                                                         |
| `fee_collector_addr`    | String      | Fee collector contract address                                                                                                          |
| `grace_period`          | Uint64      | The duration of the grace period in epochs, i.e. how many expired epochs can be claimed back in time after new epochs have been created |

## ExecuteMsg

### NewEpoch

Creates a new epoch, forwarding available tokens from epochs that are past the grace period. Can only be executed by the
fee collector.

```json
{
  "new_epoch": {}
}
```

### Claim

Claims tokens from the current epoch and all epochs that are in the grace period. Sends all tokens to the sender.

```json
{
  "claim": {}
}
```

### UpdateConfig

Updates the [Config] of the contract.

```json
{
  "update_config": {
    "owner": "migaloo1...",
    "bonding_contract_addr": "migaloo1...",
    "fee_collector_addr": "migaloo1...",
    "grace_period": "21",
    "distribution_asset": {
      "native_token": {
        "denom": "uwhale"
      }
    },
    "epoch_config": {
      "duration": "86400000000000",
      "genesis_epoch": "1698851118000000000"
    }
  }
}
```

| Key                     | Type                 | Description                            |
|-------------------------|----------------------|----------------------------------------|
| `owner`                 | Option\<String>      | New owner address                      |
| `bonding_contract_addr` | Option\<String>      | New Whale Lair address                 |
| `fee_collector_addr`    | Option\<String>      | New Fee Collector address              |
| `grace_period`          | Option\<Uint64>      | New grace period                       |
| `distribution_asset`    | Option\<AssetInfo>   | New AssetInfo to distribute rewards in |
| `epoch_config`          | Option\<EpochConfig> | New configuration for the epoch        |

## QueryMsg

### Config

Returns the current epoch, which is the last on the EPOCHS map.

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
    "owner": "migaloo1...",
    "bonding_contract_addr": "migaloo1...",
    "fee_collector_addr": "migaloo1...",
    "grace_period": "21",
    "distribution_asset": {
      "native_token": {
        "denom": "uwhale"
      }
    },
    "epoch_config": {
      "duration": "86400000000000",
      "genesis_epoch": "1698851118000000000"
    }
  }
}
```

| Key                     | Type                 | Description                            |
|-------------------------|----------------------|----------------------------------------|
| `owner`                 | Option\<String>      | New owner address                      |
| `bonding_contract_addr` | Option\<String>      | New Whale Lair address                 |
| `fee_collector_addr`    | Option\<String>      | New Fee Collector address              |
| `grace_period`          | Option\<Uint64>      | New grace period                       |
| `distribution_asset`    | Option\<AssetInfo>   | New AssetInfo to distribute rewards in |
| `epoch_config`          | Option\<EpochConfig> | New configuration for the epoch        |

{% endtab %}
{% endtabs %}

### CurrentEpoch

Returns the current epoch, which is the last on the EPOCHS map.

{% tabs %}
{% tab title="Query" %}

```json
{
  "current_epoch": {}
}
```

{% endtab %}

{% tab title="Response (EpochResponse)" %}

```json
{
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
  }
}
```

| Key     | Type  | Description          |
|---------|-------|----------------------|
| `epoch` | Epoch | Details of the epoch |

{% endtab %}
{% endtabs %}

### Epoch

Returns the epoch with the given id.

{% tabs %}
{% tab title="Query" %}

```json
{
  "epoch": {
    "id": "1"
  }
}
```

{% endtab %}

{% tab title="Response (EpochResponse)" %}

```json
{
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
  }
}
```

| Key     | Type  | Description          |
|---------|-------|----------------------|
| `epoch` | Epoch | Details of the epoch |

{% endtab %}
{% endtabs %}

### ClaimableEpochs

Returns the [Epoch]s that can be claimed.

{% tabs %}
{% tab title="Query" %}

```json
{
  "claimable_epochs": {}
}
```

{% endtab %}

{% tab title="Response (ClaimableEpochsResponse)" %}

```json
{
  "epochs": [
    {
      "id": "2",
      "start_time": "1698937518",
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
    {
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
    }
  ]
}
```

| Key      | Type        | Description              |
|----------|-------------|--------------------------|
| `epochs` | Vec\<Epoch> | List of claimable epochs |

{% endtab %}
{% endtabs %}

### Claimable

Returns the Epochs that can be claimed by an address.

{% tabs %}
{% tab title="Query" %}

```json
{
  "claimable": {
    "address": "migaloo1..."
  }
}
```

{% endtab %}

{% tab title="Response (ClaimableEpochsResponse)" %}

```json
{
  "epochs": [
    {
      "id": "2",
      "start_time": "1698937518",
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
    {
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
    }
  ]
}
```

| Key      | Type        | Description              |
|----------|-------------|--------------------------|
| `epochs` | Vec\<Epoch> | List of claimable epochs |

{% endtab %}
{% endtabs %}
