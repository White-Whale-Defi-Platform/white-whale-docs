# Incentive 
The incentive contract is responsible for distributing the flow rewards to the LPs. It is also responsible for managing the liquidity flows and positions.
Incentive contracts allow any user to incentivize a pair created. External users can then create positions to utilize the flow by bonding their LP tokens. Users will receive rewards for _each active flow_.



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


## ExecuteMsg


### TakeGlobalWeightSnapshot

Makes a snapshot of the current global weight, at the current epoch.

```json 
{
    "take_global_weight_snapshot": {}
}
```

### OpenFlow

Opens a new liquidity flow

```json 
{
    "open_flow": {
      "start_epoch": 123,
      "end_epoch": 123,
      "curve": "Linear",
      "flow_asset": {
        "native_token": {
          "denom": "uwhale"
        }
      }
    }

}
```

| Key           | Type        | Description                                                                                         |
| ------------- | ----------- | --------------------------------------------------------------------------------------------------- |
| `start_epoch` | Option<u64> | The epoch at which the flow should start. If unspecified, the flow will start at the current epoch. |
| `end_epoch`   | u64         | The epoch at which the flow should end.                                                             |
| `curve`       | Curve       | The type of distribution curve.                                                                     |
| `flow_asset`  | Asset       | The asset to be distributed in this flow.                                                           |

### CloseFlow

Closes an existing liquidity flow.
Sender of the message must either be the contract admin or the creator of the flow.

```json 
{
    "close_flow": {
      "flow_id": 123
    }

}
```

| Key       | Type | Description                  |
| --------- | ---- | ---------------------------- |
| `flow_id` | u64  | The id of the flow to close. |


### OpenPosition

Creates a new position to earn flow rewards.

```json 
{
    "open_position": {
      "amount": "1000000",
      "unbonding_duration": 123456789,
      "receiver": "juno1..."
    }

}
```

| Key                  | Type           | Description                                                                                                                            |
| -------------------- | -------------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| `amount`             | Uint128        | The amount to add to the position.                                                                                                     |
| `unbonding_duration` | u64            | The amount of time (in seconds) before the LP tokens can be redeemed.                                                                  |
| `receiver`           | Option<String> | The receiver of the new position. This is mostly used for the frontend helper contract. If left empty, defaults to the message sender. |

### ExpandPosition

Expands an existing position to earn more flow rewards.

```json
{
    "expand_position": {
      "amount": "1000000",
      "unbonding_duration": 123456789
    }
}
```

| Key                  | Type           | Description                                                                                                                                 |
| -------------------- | -------------- | ------------------------------------------------------------------------------------------------------------------------------------------- |
| `amount`             | Uint128        | The amount to add to the existing position.                                                                                                 |
| `unbonding_duration` | u64            | The unbond completion timestamp to identify the position to add to.                                                                         |
| `receiver`           | Option<String> | The receiver of the expanded position. This is mostly used for the frontend helper contract. If left empty, defaults to the message sender. |

### ClosePosition

Closes an existing position to stop earning flow rewards.

```json
{
    "close_position": {
      "unbonding_duration": 123456789
    }
}
```

| Key                  | Type | Description                                      |
| -------------------- | ---- | ------------------------------------------------ |
| `unbonding_duration` | u64  | The unbonding duration of the position to close. |

### Withdraw

Withdraws the LP tokens from a closed position once the unbonding duration has passed.

```json
{
    "withdraw": {}
}
```

### Claim

Claims the flow rewards.

```json
{
    "claim": {}
}
```

