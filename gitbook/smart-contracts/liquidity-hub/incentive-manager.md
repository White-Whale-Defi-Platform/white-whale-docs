# Incentive Manager

## Instantiate

Instantiates an instance of the incentive manager contract

```json
{
  "owner": "migaloo1...",
  "epoch_manager_addr": "migaloo1...",
  "bonding_manager_addr": "migaloo1...",
  "create_incentive_fee": {
    "denom": "uwhale",
    "amount": "1000000000"
  },
  "max_concurrent_incentives": 7,
  "max_incentive_epoch_buffer": 14,
  "min_unlocking_duration": 86400,
  "max_unlocking_duration": 31536000,
  "emergency_unlock_penalty": "0.01"
}
```

| Key                          | Type    | Description                                                                                     |
|------------------------------|---------|-------------------------------------------------------------------------------------------------|
| `owner`                      | String  | The owner of the contract.                                                                      |
| `epoch_manager_addr`         | String  | The epoch manager address, where the epochs are managed.                                        |
| `bonding_manager_addr`       | String  | The bonding manager address, where protocol fees are distributed.                               |
| `create_incentive_fee`       | Coin    | The fee that must be paid to create an incentive.                                               |
| `max_concurrent_incentives`  | u32     | The maximum amount of incentives that can exist for a single LP token at a time.                |
| `max_incentive_epoch_buffer` | u32     | New incentives are allowed to start up to `current_epoch + start_epoch_buffer` into the future. |
| `min_unlocking_duration`     | u32     | The minimum amount of time that a user can lock their tokens for. In seconds.                   |
| `max_unlocking_duration`     | u32     | The maximum amount of time that a user can lock their tokens for. In seconds.                   |
| `emergency_unlock_penalty`   | Decimal | The penalty for unlocking a position before the unlocking duration finishes. In percentage.     |

## ExecuteMsg

### ManageIncentive

Manages an incentive based on the action, which can be:

- Fill: Fills an incentive. If the incentive doesn't exist, it creates a new one. If it exists already,
  it expands it given the sender created the original incentive and the params are correct.
- Close: Closes an incentive with the given identifier. If the incentive has expired, anyone can
  close it. Otherwise, only the incentive creator or the owner of the contract can close an incentive.

{% tabs %}
{% tab title="Fill" %}

```json
{
  "manage_incentive": {
    "fill": {
      "lp_denom": "factory/migaloo1.../uLP",
      "start_epoch": 10,
      "preliminary_end_epoch": 24,
      "curve": "linear",
      "incentive_asset": {
        "denom": "uwhale",
        "amount": "1000000000"
      },
      "incentive_identifier": "incentive_identifier"
    }
  }
}
```

| Key                     | Type            | Description                                                                                                                                                            |
|-------------------------|-----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `lp_denom`              | String          | The LP asset denom to create the incentive for.                                                                                                                        |
| `start_epoch`           | Option\<u64>    | The epoch at which the incentive will start. If unspecified, it will start at the current epoch.                                                                       |
| `preliminary_end_epoch` | Option\<u64>    | The epoch at which the incentive should preliminarily end (if it's not expanded). If unspecified, the incentive will default to end at 14 epochs from the current one. |
| `curve`                 | Option\<Curve>  | The type of distribution curve. If unspecified, the distribution will be linear.                                                                                       |
| `incentive_asset`       | Coin            | The asset to be distributed in this incentive.                                                                                                                         |
| `incentive_identifier`  | Option\<String> | If set, it  will be used to identify the incentive.                                                                                                                    |

{% endtab %}

{% tab title="Close" %}

```json
{
  "manage_incentive": {
    "close": {
      "incentive_identifier": "incentive_identifier"
    }
  }
}
```

| Key                    | Type   | Description                        |
|------------------------|--------|------------------------------------|
| `incentive_identifier` | String | The incentive identifier to close. |

{% endtab %}
{% endtabs %}

### ManagePosition

Manages a position based on the action, which can be:

- Fill: Fills a position. If the position doesn't exist, it opens it. If it exists already, it
  expands it given the sender opened the original position and the params are correct.
- Close: Closes an existing position. The position stops earning incentive rewards.
- Withdraw: Withdraws the LP tokens from a position after the position has been closed and the unlocking duration has
  passed.

{% tabs %}
{% tab title="Fill" %}

```json
{
  "manage_position": {
    "fill": {
      "identifier": "position_identifier",
      "unlocking_duration": 86400,
      "receiver": "migaloo1..."
    }
  }
}
```

| Key                  | Type            | Description                                                                    |
|----------------------|-----------------|--------------------------------------------------------------------------------|
| `identifier`         | Option\<String> | The identifier of the position.                                                |
| `unlocking_duration` | u64             | The time it takes in seconds to unlock this position.                          |
| `receiver`           | Option\<String> | The receiver for the position.  If left empty, defaults to the message sender. |

{% endtab %}

{% tab title="Close" %}

```json
{
  "manage_position": {
    "close": {
      "identifier": "position_identifier",
      "lp_asset": {
        "denom": "factory/migaloo1.../uLP",
        "amount": "1000000000"
      }
    }
  }
}
```

| Key          | Type   | Description                                                                                                                   |
|--------------|--------|-------------------------------------------------------------------------------------------------------------------------------|
| `identifier` | String | The identifier of the position.                                                                                               |
| `lp_asset`   | String | The asset to remove from the position. If not set, the position will be closed in full. If not, it could be partially closed. |

{% endtab %}

{% tab title="Withdraw" %}

```json
{
  "manage_position": {
    "close": {
      "identifier": "position_identifier",
      "emergency_unlock": true
    }
  }
}
```

| Key                | Type          | Description                                                                                                                    |
|--------------------|---------------|--------------------------------------------------------------------------------------------------------------------------------|
| `identifier`       | String        | The identifier of the position.                                                                                                |
| `emergency_unlock` | Option\<bool> | Whether to unlock the position in an emergency. If set to true, the position will be unlocked immediately, but with a penalty. |

{% endtab %}
{% endtabs %}

### Claim

Claims the rewards for the user.

```json
{
  "claim": {}
}
```

### UpdateConfig

Updates the contract configuration.

```json
{
  "update_config": {
    "bonding_manager_addr": "migaloo1...",
    "epoch_manager_addr": "migaloo1...",
    "create_incentive_fee": {
      "denom": "uwhale",
      "amount": "1000000000"
    },
    "max_concurrent_incentives": 7,
    "max_incentive_epoch_buffer": 14,
    "min_unlocking_duration": 86400,
    "max_unlocking_duration": 31536000,
    "emergency_unlock_penalty": "0.01"
  }
}
```

| Key                          | Type             | Description                                                                                 |
|------------------------------|------------------|---------------------------------------------------------------------------------------------|
| `bonding_manager_addr`       | Option\<String>  | The address to of the bonding manager, to send fees to.                                     |
| `epoch_manager_addr`         | Option\<String>  | The epoch manager address, where the epochs are managed.                                    |
| `create_incentive_fee`       | Option\<Coin>    | The fee that must be paid to create an incentive.                                           |
| `max_concurrent_incentives`  | Option\<u32>     | The maximum amount of incentives that can exist for a single LP token at a time.            |
| `max_incentive_epoch_buffer` | Option\<u32>     | The maximum amount of epochs in the future a new incentive is allowed to start in.          |
| `min_unlocking_duration`     | Option\<u32>     | The minimum amount of time that a user can lock their tokens for. In seconds.               |
| `max_unlocking_duration`     | Option\<u32>     | The maximum amount of time that a user can lock their tokens for. In seconds.               |
| `emergency_unlock_penalty`   | Option\<Decimal> | The penalty for unlocking a position before the unlocking duration finishes. In percentage. |

### EpochChangedHook

Gets triggered by the epoch manager when a new epoch is created.

```json
{
  "epoch_changed_hook": {
    "current_epoch": {
      "id": 23,
      "start_time": "1571797419879305533"
    }
  }
}
```

| Key             | Type  | Description        |
|-----------------|-------|--------------------|
| `current_epoch` | Epoch | The current epoch. |

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


