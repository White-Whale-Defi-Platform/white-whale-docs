# Fee Distributor 

The Fee Distributor is responsible for distributing the protocol fees collected by the Fee Collector to the various
stakeholders of the protocol.

## InstantiateMsg

```json
{
  "bonding_contract_addr": "string",
  "distribution_asset": {
    "asset": {
      "amount": "string",
      "info": {
        "native_token": {
          "denom": "string"
        },
        "token": {
          "contract_addr": "string"
        }
      }
    }
  },
  "epoch_config": {
    "duration": "string",
    "genesis_epoch": "string"
  },
  "fee_collector_addr": "string",
  "grace_period": "string"
}
```

## ExecuteMsg 

### NewEpoch

Creates a new epoch, forwarding available tokens from epochs that are past the grace period. Can only be executed by the fee collector.

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
        "owner": "string",
        "bonding_contract_addr": "string",
        "fee_collector_addr": "string",
        "grace_period": "string",
        "distribution_asset": {
            "asset": {
                "amount": "string",
                "info": {
                    "native_token": {
                        "denom": "string"
                    },
                    "token": {
                        "contract_addr": "string"
                    }
                }
            }
        },
        "epoch_config": {
            "duration": "string",
            "genesis_epoch": "string"
        }
    }
}
```

## QueryMsg

### Config

Returns the current epoch, which is the last on the EPOCHS map.

```json
{
  "config": {}
}
```

#### ConfigResponse

```json
{"config": {
    "owner": "string",
    "bonding_contract_addr": "string",
    "fee_collector_addr": "string",
    "grace_period": "string",
    "distribution_asset": {
        "asset": {
            "amount": "string",
            "info": {
                "native_token": {
                    "denom": "string"
                },
                "token": {
                    "contract_addr": "string"
                }
            }
        }
    },
    "epoch_config": {
        "duration": "string",
        "genesis_epoch": "string"
    }
}}
```

### CurrentEpoch

Returns the current epoch, which is the last on the EPOCHS map.

```json
{
  "current_epoch": {}
}
```

#### EpochResponse

```json
{
  "epoch": {
    "id": "string"
  }
}
```

### Epoch

Returns the epoch with the given id.

```json
{
  "epoch": {
    "id": "string"
  }
}
```

#### EpochResponse

```json
{
  "epoch": {
    "id": "string"
  }
}
```

### ClaimableEpochs

Returns the [Epoch]s that can be claimed.

```json
{
  "claimable_epochs": {}
}
```

#### ClaimableEpochsResponse

```json
{
  "epochs": [
    {
      "id": "string"
    }
  ]
}
```

### Claimable

Returns the [Epoch]s that can be claimed by an address.

```json
{
  "claimable": {
    "address": "string"
  }
}
```

#### ClaimableEpochsResponse

```json
{
  "epochs": [
    {
      "id": "string"
    }
  ]
}
```







