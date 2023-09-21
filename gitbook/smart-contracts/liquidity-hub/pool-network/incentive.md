# Incentive

The incentive contract is responsible for distributing the flow rewards to the LPs. It is also responsible for managing
the liquidity flows and positions.
Incentive contracts allow any user to incentivize a pool. External users can then create positions to get rewards from
flows by locking their LP tokens. Users will receive rewards for _each active flow_.

What is a flow?

So every incentive contract is able to have multiple flows. A flow is a stream of rewards that are distributed among
users who lock their LP tokens. A flow has a start and end epoch, and a curve that determines how the rewards are
distributed. A flow can be open, expanded and closed.

A flow is open when it is created, and users can add to their positions.

The flow can only be closed by the flow creator or the contract admin. When a flow is closed, the unclaimed rewards are
returned to the creator.

The flow can be expanded indefinitely, but due to some limitations, the flow gets "reset" after a period of 180 epochs.
When a flow gets reset, nothing changes for you as a flow creator in practice, as the flow continues to distribute
rewards as usual. If you are a user however, you will need to claim your rewards within those 180 epochs (about 6
months), otherwise you will lose the rewards you were entitled to as they will become claimable by all the LP holders.

## Instantiate

Instantiates an instance of the incentive contract

```json
{
  "lp_asset": {
    "native_token": {
      "denom": "factory/migaloo1.../uLP"
    }
  },
  "fee_distributor_address": "migaloo1..."
}
```

| Key                       | Type      | Description                      |
|---------------------------|-----------|----------------------------------|
| `lp_asset`                | AssetInfo | Information about the LP asset   |
| `fee_distributor_address` | String    | Fee distributor contract address |

## ExecuteMsg

### TakeGlobalWeightSnapshot

Makes a snapshot of the current global weight, at the current epoch. Used to accurately calculate the rewards share.

```json 
{
  "take_global_weight_snapshot": {}
}
```

### OpenFlow

Opens a new liquidity flow.

```json 
{
  "open_flow": {
    "start_epoch": 123,
    "end_epoch": 123,
    "curve": "linear",
    "flow_asset": {
      "amount": "1000000",
      "native_token": {
        "denom": "uwhale"
      }
    },
    "flow_label": "my_alias"
  }
}
```

| Key           | Type            | Description                                                                                                                           |
|---------------|-----------------|---------------------------------------------------------------------------------------------------------------------------------------|
| `start_epoch` | Option\<u64>    | The epoch at which the flow should start. If unspecified, the flow will start at the current epoch.                                   |
| `end_epoch`   | Option\<u64>    | The epoch at which the flow should end. If unspecified, the flow will end in 14 epochs, or 2 weeks if the epoch is set to last a day. |
| `curve`       | Option\<Curve>  | The type of distribution curve. If not set, the default curve will be Linear.                                                         |
| `flow_asset`  | Asset           | The asset to be distributed in this flow.                                                                                             |
| `flow_label`  | Option\<String> | If set, the label will be used to identify the flow, in addition to the flow_id.                                                      |

### CloseFlow

Closes an existing liquidity flow.
Sender of the message must either be the contract admin or the creator of the flow.

{% tabs %}
{% tab title="Close Flow with a Flow ID" %}

```json 
{
  "close_flow": {
    "flow_identifier": {
      "id": 123
    }
  }
}
```

{% endtab %}

{% tab title="Close Flow with a Flow Label" %}

```json 
{
  "close_flow": {
    "flow_identifier": {
      "label": "my_alias"
    }
  }
}
```

{% endtab %}
{% endtabs %}

| Key               | Type           | Description                          |
|-------------------|----------------|--------------------------------------|
| `flow_identifier` | FlowIdentifier | The identifier of the flow to close. |

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

| Key                  | Type            | Description                                                                                                                            |
|----------------------|-----------------|----------------------------------------------------------------------------------------------------------------------------------------|
| `amount`             | Uint128         | The amount to add to the position.                                                                                                     |
| `unbonding_duration` | u64             | The amount of time (in seconds) before the LP tokens can be redeemed.                                                                  |
| `receiver`           | Option\<String> | The receiver of the new position. This is mostly used for the frontend helper contract. If left empty, defaults to the message sender. |

### ExpandPosition

Expands an existing position to earn more flow rewards.

```json
{
  "expand_position": {
    "amount": "1000000",
    "unbonding_duration": 123456789,
    "receiver": "migaloo1..."
  }
}
```

| Key                  | Type            | Description                                                                                                                                 |
|----------------------|-----------------|---------------------------------------------------------------------------------------------------------------------------------------------|
| `amount`             | Uint128         | The amount to add to the existing position.                                                                                                 |
| `unbonding_duration` | u64             | The unbond completion timestamp to identify the position to add to.                                                                         |
| `receiver`           | Option\<String> | The receiver of the expanded position. This is mostly used for the frontend helper contract. If left empty, defaults to the message sender. |

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
|----------------------|------|--------------------------------------------------|
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

### Expand Flow

Expands an existing flow.

```json
{
  "expand_flow": {
    "flow_identifier": {
      "label": "my_alias"
    },
    "end_epoch": 123,
    "flow_asset": {
      "amount": "1000000",
      "info": {
        "native_token": {
          "denom": "uwhale"
        }
      }
    }
  }
}
```

| Key               | Type           | Description                                                                                                 |
|-------------------|----------------|-------------------------------------------------------------------------------------------------------------|
| `flow_identifier` | FlowIdentifier | The identifier of the flow to expand, whether an id or a label.                                             |
| `end_epoch`       | Option\<u64>   | The epoch at which the flow should end. If not set, the flow will be expanded a default value of 14 epochs. |
| `flow_asset`      | Asset          | The asset to expand this flow with.                                                                         |

## QueryMsg

### Config

Retrieves the current contract configuration.

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
  "factory_address": "migaloo1...",
  "fee_distributor_address": "migaloo1...",
  "lp_asset": {
    "native_token": {
      "denom": "factory/migaloo1.../uLP"
    }
  }
}
```

| Key                       | Type      | Description                                       |
|---------------------------|-----------|---------------------------------------------------|
| `factory_address`         | Addr      | The address of the incentive factory              |
| `fee_distributor_address` | Addr      | Fee distributor contract                          |
| `lp_asset`                | AssetInfo | The LP token asset tied to the incentive contract |

{% endtab %}
{% endtabs %}

### Flow

Retrieves a specific flow. If start_epoch and end_epoch are set, the asset_history and emitted_tokens will be filtered
to only include epochs within the range. The maximum gap between the start_epoch and end_epoch is 100 epochs.

{% tabs %}
{% tab title="Query" %}

```json
{
  "flow": {
    "flow_identifier": {
      "id": 123
    },
    "start_epoch": 1500,
    "end_epoch": 1600
  }
}
```

| Key               | Type           | Description                                                                                  |
|-------------------|----------------|----------------------------------------------------------------------------------------------|
| `flow_identifier` | FlowIdentifier | The id of the flow to find.                                                                  |
| `start_epoch`     | Option\<u64>   | If set, filters the asset_history and emitted_tokens to only include epochs from start_epoch |
| `end_epoch`       | Option\<u64>   | If set, filters the asset_history and emitted_tokens to only include epochs until end_epoch  |

{% endtab %}

{% tab title="Response (FlowResponse)" %}

```json
{
  "flow": {
    "flow_id": 1,
    "flow_label": "my_alias",
    "flow_creator": "migaloo1...",
    "flow_asset": {
      "info": {
        "native_token": {
          "denom": "uwhale"
        }
      },
      "amount": "10000000"
    },
    "claimed_amount": "500000000",
    "curve": "linear",
    "start_epoch": 100,
    "end_epoch": 200,
    "emitted_tokens": {
      "1": "10000000",
      "2": "20000000"
    },
    "asset_history": {
      "1": [
        "5000000",
        100
      ],
      "2": [
        "6000000",
        150
      ]
    }
  }
}
```

| Key    | Type          | Description                    |
|--------|---------------|--------------------------------|
| `flow` | Option\<Flow> | The flow that was searched for |

{% endtab %}
{% endtabs %}

### Flows

Retrieves the current flows. If start_epoch and end_epoch are set, the asset_history and emitted_tokens will be filtered
to only include epochs within the range. The maximum gap between the start_epoch and end_epoch is 100 epochs.

{% tabs %}
{% tab title="Query" %}

```json
{
  "flows": {
    "start_epoch": 1500,
    "end_epoch": 1600
  }
}
```

| Key           | Type         | Description                                                                                  |
|---------------|--------------|----------------------------------------------------------------------------------------------|
| `start_epoch` | Option\<u64> | If set, filters the asset_history and emitted_tokens to only include epochs from start_epoch |
| `end_epoch`   | Option\<u64> | If set, filters the asset_history and emitted_tokens to only include epochs until end_epoch  |

{% endtab %}

{% tab title="Response (FlowsResponse)" %}

```json
{
  "flows": [
    {
      "flow_id": 1,
      "flow_label": "my_alias",
      "flow_creator": "migaloo1...",
      "flow_asset": {
        "info": {
          "native_token": {
            "denom": "uwhale"
          }
        },
        "amount": "10000000"
      },
      "claimed_amount": "500000000",
      "curve": "linear",
      "start_epoch": 100,
      "end_epoch": 200,
      "emitted_tokens": {
        "1": "10000000",
        "2": "20000000"
      },
      "asset_history": {
        "1": [
          "5000000",
          100
        ],
        "2": [
          "6000000",
          150
        ]
      }
    },
    {
      "flow_id": 2,
      "flow_label": "another_alias",
      "flow_creator": "migaloo1...",
      "flow_asset": {
        "info": {
          "native_token": {
            "denom": "uwhale"
          }
        },
        "amount": "10000000"
      },
      "claimed_amount": "500000000",
      "curve": "linear",
      "start_epoch": 100,
      "end_epoch": 200,
      "emitted_tokens": {
        "1": "10000000",
        "2": "20000000",
        "3": "30000000"
      },
      "asset_history": {
        "1": [
          "5000000",
          100
        ],
        "2": [
          "6000000",
          150
        ]
      }
    }
  ]
}
```

| Key     | Type      | Description       |
|---------|-----------|-------------------|
| `flows` | Vec<Flow> | The current flows |

{% endtab %}
{% endtabs %}

### Positions

Retrieves the positions for an address.

{% tabs %}
{% tab title="Query" %}

```json
{
  "positions": {
    "address": "migaloo1..."
  }
}
```

| Key       | Type   | Description           |
|-----------|--------|-----------------------|
| `address` | String | The address to query. |

{% endtab %}

{% tab title="Response (PositionsResponse)" %}

```json
{
  "timestamp": 123456789,
  "positions": [
    {
      "open_position": {
        "amount": "1000000000",
        "unbonding_duration": 3600,
        "weight": "500000000"
      }
    },
    {
      "closed_position": {
        "amount": "5000",
        "unbonding_duration": 86400,
        "weight": "500000000"
      }
    }
  ]
}
```

| Key         | Type                | Description                        |
|-------------|---------------------|------------------------------------|
| `timestamp` | u64                 | The current time of the blockchain |
| `positions` | Vec\<QueryPosition> | All the positions a user has       |

{% endtab %}
{% endtabs %}

### Rewards

Retrieves the rewards for an address.

{% tabs %}
{% tab title="Query" %}

```json
{
  "rewards": {
    "address": "juno1..."
  }
}
```

| Key       | Type   | Description           |
|-----------|--------|-----------------------|
| `address` | String | The address to query. |

{% endtab %}

{% tab title="Response (RewardsResponse)" %}

```json
{
  "rewards": [
    {
      "amount": "10000000",
      "info": {
        "native_token": {
          "denom": "uwhale"
        }
      }
    },
    {
      "amount": "500000",
      "info": {
        "token": {
          "contract_addr": "migaloo1..."
        }
      }
    }
  ]
}
```

| Key       | Type        | Description                                                                                 |
|-----------|-------------|---------------------------------------------------------------------------------------------|
| `rewards` | Vec\<Asset> | The rewards that is available to a user if they executed the `claim` function at this point |

{% endtab %}
{% endtabs %}

### GlobalWeight

Retrieves the global weight for an epoch.

{% tabs %}
{% tab title="Query" %}

```json
{
  "global_weight": {
    "epoch_id": 123
  }
}
```

| Key        | Type | Description                             |
|------------|------|-----------------------------------------|
| `epoch_id` | u64  | The epoch to get the global weight for. |

{% endtab %}

{% tab title="Response (GlobalWeightResponse)" %}

```json
{
  "global_weight": "1000000000",
  "epoch_id": 123456
}
```

| Key             | Type    | Description                                                     |
|-----------------|---------|-----------------------------------------------------------------|
| `global_weight` | Uint128 | The global weight of the incentive contract for the given epoch |
| `epoch_id`      | u64     | Epoch id for which the global weight is calculated              |

{% endtab %}
{% endtabs %}

### CurrentEpochRewardsShare

Retrieves the rewards share of an address for the current epoch.

{% tabs %}
{% tab title="Query" %}

```json
{
  "current_epoch_rewards_share": {
    "address": "migaloo1..."
  }
}
```

| Key       | Type   | Description           |
|-----------|--------|-----------------------|
| `address` | String | The address to query. |

{% endtab %}

{% tab title="Response (RewardsShareResponse)" %}

```json
{
  "address": "migaloo1...",
  "global_weight": "1000000",
  "address_weight": "500000",
  "share": "0.5",
  "epoch_id": 123456
}
```

| Key              | Type       | Description                                                     |
|------------------|------------|-----------------------------------------------------------------|
| `address`        | Addr       | The address the rewards were retrieved for                      |
| `global_weight`  | Uint128    | The global weight of the incentive contract for the given epoch |
| `address_weight` | Uint128    | The weight of the address                                       |
| `share`          | Decimal256 | The rewards share of the address                                |
| `epoch_id`       | u64        | The epoch which the rewards were computed for                   |

{% endtab %}
{% endtabs %}

