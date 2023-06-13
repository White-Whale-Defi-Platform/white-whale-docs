# Incentive Factory

Migaloo's incentive factory contract is used to create incentive flows associated with LP tokens. Incentive contracts allow permissioned users to create an incentive contract associated with an LP token. Once an incentive contract is created for a LP token, it is stored in state, allowing the incentive factory to act as a incentive registry, which can be queried for reference. Note that the incentive factory is permissioned, meaning the messages can only be executed by the owner of the contract.

## Instantiate

Instantiates an instance of the incentive contract 

```json
{
    "lp_asset": {
      "native_token": {
        "denom": "uwhale"
      }
    },
    "fee_distributor_address": "migaloo1...",
}
```
| Key                       | Type      | Description                      |
| ------------------------- | --------- | -------------------------------- |
| `lp_asset`                | AssetInfo | Information about the LP asset   |
| `fee_distributor_address` | String    | Fee distributor contract address |

## Instantiate


```json
{
    "fee_collector_addr": "migaloo1...",
    "fee_distributor_addr": "migaloo1...",
    "create_flow_fee": {
        "native_token": {
            "denom": "uwhale"
        }
    },
    "max_concurrent_flows": 10,
    "incentive_code_id": 123,
    "max_flow_epoch_buffer": 10,
    "min_unbonding_duration": 10,
    "max_unbonding_duration": 10
}
```

| Key                      | Type   | Description                                                                                                                                     |
| ------------------------ | ------ | ----------------------------------------------------------------------------------------------------------------------------------------------- |
| `fee_collector_addr`     | String | The address of the fee collector to send flow creation fees to.                                                                                 |
| `fee_distributor_addr`   | String | Fee distributor contract address.                                                                                                               |
| `create_flow_fee`        | Asset  | The fee that must be paid to create a flow.                                                                                                     |
| `max_concurrent_flows`   | u64    | The maximum amount of flows that can exist for a single LP token at a single time.                                                              |
| `incentive_code_id`      | u64    | The code ID of the incentive contract.                                                                                                          |
| `max_flow_epoch_buffer`  | u64    | The maximum epoch buffer for a new flow (in epochs). New flows are allowed to start up to `current_epoch + start_epoch_buffer` into the future. |
| `min_unbonding_duration` | u64    | The minimum amount of seconds that a user must bond their tokens for.                                                                           |
| `max_unbonding_duration` | u64    | The maximum amount of seconds that a user must bond their tokens for.                                                                           |

## ExecuteMsg


### Create Incentive 

Creates a new incentive contract tied to the `lp_asset` specified.

```json
{
    "create_incentive": {
        "lp_asset": {
            "native_token": {
                "denom": "uwhale"
            }
        }
    }
}
```

| Key        | Type      | Description                    |
| ---------- | --------- | ------------------------------ |
| `lp_asset` | AssetInfo | Information about the LP asset |

### Update Config

Updates the configuration of the contract.


```json
{
    "update_config": {
        "owner": "migaloo1...",
        "fee_collector_addr": "migaloo1...",
        "fee_distributor_addr": "migaloo1...",
        "create_flow_fee": {
            "native_token": {
                "denom": "uwhale"
            }
        },
        "max_concurrent_flows": 10,
        "incentive_code_id": 123,
        "max_flow_epoch_buffer": 10,
        "min_unbonding_duration": 10,
        "max_unbonding_duration": 10
    }
}
```

| Key                      | Type   | Description                                                                                                                                             |
| ------------------------ | ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `owner`                  | String | The owner of the contract. If unspecified, the owner address will not change.                                                                           |
| `fee_collector_addr`     | String | The new fee collector address to send flow creation fees to. If unspecified, the fee collector address will not change.                                 |
| `fee_distributor_addr`   | String | The new fee distributor address to get epochs from. If unspecified, the fee distributor address will not change.                                        |
| `create_flow_fee`        | Asset  | The new fee that must be paid to create a flow. If unspecified, the flow fee will not change.                                                           |
| `max_concurrent_flows`   | u64    | The maximum amount of concurrent flows that can exist for a single LP token at a single time. If unspecified, the max concurrent flows will not change. |
| `incentive_code_id`      | u64    | The new code ID of the incentive contract. If unspecified, the incentive contract id will not change.                                                   |
| `max_flow_epoch_buffer`  | u64    | The new maximum start time buffer for a new flow (in seconds). If unspecified, the flow start buffer will not change.                                   |
| `min_unbonding_duration` | u64    | The minimum amount of seconds that a user must bond their tokens for. If unspecified, the `min_unbonding_duration` will not change.                     |
| `max_unbonding_duration` | u64    | The maximum amount of seconds that a user must bond their tokens for. If unspecified, the `max_unbonding_duration` will not change.                     |

### Migrate Incentive

Migrates an incentive contract to a new code ID.

```json
{
    "migrate_incentive": {
        "incentive_address": "migaloo1...",
        "code_id": 123
    }
}
```

| Key                 | Type   | Description                                                                                                                                 |
| ------------------- | ------ | ------------------------------------------------------------------------------------------------------------------------------------------- |
| `incentive_address` | String | The address of the incentive contract                                                                                                       |
| `code_id`           | u64    | The new code ID to migrate the incentive contract to. If unspecified, will default to the incentive factory's configured incentive code ID. |

## QueryMsg

### Config

Retrieves the config of the incentive factory.

```json
{
    "config": {}
}
```

### Incentive

Retrieves a specific incentive address.

```json
{
    "incentive": {
        "lp_asset": {
            "native_token": {
                "denom": "uwhale"
            }
        }
    }
}
```

| Key        | Type      | Description                    |
| ---------- | --------- | ------------------------------ |
| `lp_asset` | AssetInfo | Information about the LP asset |

### Incentives

Retrieves a list of incentive contracts.

```json
{
    "incentives": {
        "start_after": {
            "native_token": {
                "denom": "uwhale"
            }
        },
        "limit": 10
    }
}
```

| Key           | Type      | Description                                                                                                     |
| ------------- | --------- | --------------------------------------------------------------------------------------------------------------- |
| `start_after` | AssetInfo | An optional parameter specifying what incentive contract to start searching after.                              |
| `limit`       | u32       | The amount of incentive contracts to return. If unspecified, will default to a value specified by the contract. |

