# Whale Lair

The Whale Lair is a bonding contract used to bond WHALE LSDs.

{% hint style="warning" %}
Note: the contract treats all LSDs as equal, i.e. 10 ampWHALE will have the same weight as 10 bWHALE.
{% endhint %}

## InstantiateMsg

```json
{
  "unbonding_period": "86400000000000",
  "growth_rate": "0.01",
  "bonding_assets": [
    {
      "native_token": {
        "denom": "ampWHALE"
      }
    },
    {
      "native_token": {
        "denom": "bWHALE"
      }
    }
  ]
}
```

| Key                | Type            | Description                                   |
|--------------------|-----------------|-----------------------------------------------|
| `unbonding_period` | Uint64          | Unbonding period in nanoseconds               |
| `growth_rate`      | Decimal         | Weight grow rate. Needs to be between 0 and 1 |
| `bonding_assets`   | Vec\<AssetInfo> | AssetInfo of the assets that can be bonded    |

## ExecuteMsg

### Bond

Bonds the specified [Asset]. This assumes the [Asset] is already white-listed for bonding.

```json
{
  "bond": {
    "asset": {
      "info": {
        "native_token": {
          "denom": "ampWHALE"
        }
      },
      "amount": "1000"
    }
  }
}
```

| Key    | Type  | Description            |
|--------|-------|------------------------|
| `bond` | Asset | The Asset to be bonded |

### Unbond

Unbonds the specified [Asset].

```json
{
  "unbond": {
    "asset": {
      "info": {
        "native_token": {
          "denom": "ampWHALE"
        }
      },
      "amount": "1000"
    }
  }
}
```

| Key      | Type  | Description              |
|----------|-------|--------------------------|
| `unbond` | Asset | The Asset to be unbonded |

### Withdraw

Sends withdrawable unbonded tokens to the user.

```json
{
  "withdraw": {
    "denom": "ampWHALE"
  }
}
```

| Key     | Type   | Description                            |
|---------|--------|----------------------------------------|
| `denom` | String | The denom of the asset to be withdrawn |

### UpdateConfig

Updates the Config of the contract.

```json
{
  "update_config": {
    "owner": "migaloo1...",
    "unbonding_period": "172800000000000",
    "growth_rate": "0.02",
    "fee_distributor_addr": "migaloo1..."
  }
}
```

| Key                    | Type             | Description                                   |
|------------------------|------------------|-----------------------------------------------|
| `owner`                | Option\<String>  | The owner of the contract                     |
| `unbonding_period`     | Option\<Uint64>  | Unbonding period in nanoseconds               |
| `growth_rate`          | Option\<Decimal> | Weight grow rate. Needs to be between 0 and 1 |
| `fee_distributor_addr` | Option\<String>  | The address of the fee distributor contract   |

## QueryMsg

### Config

Returns the configuration of the contract.

{% tabs %}
{% tab title="Query" %}

```json
{
  "config": {}
}
```

{% endtab %}

{% tab title="Response (Config)" %}

```json
{
  "owner": "migaloo1...",
  "unbonding_period": "172800000000000",
  "growth_rate": "0.02",
  "bonding_assets": [
    {
      "native_token": {
        "denom": "ampWHALE"
      }
    },
    {
      "native_token": {
        "denom": "bWHALE"
      }
    }
  ],
  "fee_distributor_addr": "migaloo1..."
}
```

| Key                    | Type            | Description                                   |
|------------------------|-----------------|-----------------------------------------------|
| `owner`                | Addr            | The contract's owner                          |
| `unbonding_period`     | Uint64          | Unbonding period in nanoseconds               |
| `growth_rate`          | Decimal         | Weight grow rate. Needs to be between 0 and 1 |
| `bonding_assets`       | Vec\<AssetInfo> | AssetInfo of the assets that can be bonded    |
| `fee_distributor_addr` | Addr            | The address of the fee distributor contract   |

{% endtab %}
{% endtabs %}

### Bonded

Returns the amount of assets that have been bonded by the specified address.

{% tabs %}
{% tab title="Query" %}

```json
{
  "bonded": {
    "address": "migaloo1..."
  }
}
```

| Key       | Type   | Description                     |
|-----------|--------|---------------------------------|
| `address` | String | The address to run the query on |

{% endtab %}

{% tab title="Response (BondedResponse)" %}

```json
{
  "total_bonded": "1000",
  "bonded_assets": [
    {
      "amount": "500",
      "info": {
        "native_token": {
          "denom": "ampWHALE"
        }
      }
    },
    {
      "amount": "500",
      "info": {
        "native_token": {
          "denom": "bWHALE"
        }
      }
    }
  ],
  "first_bonded_epoch_id": 10
}
```

| Key                     | Type        | Description                                                                                                |
|-------------------------|-------------|------------------------------------------------------------------------------------------------------------|
| `total_bonded`          | Uint128     | How much in total the address has bonded. Again, all LSDs are considered fungible for this calculation     |
| `bonded_assets`         | Vec\<Asset> | The list of LSDs bonded by the address                                                                     |
| `first_bonded_epoch_id` | Uint64      | The first epoch when this address bonded. Used to perform some rewards calculations on the fee distributor |

{% endtab %}
{% endtabs %}

### Unbonding

Returns the amount of tokens of the given denom that are been unbonded by the specified address. Allows pagination.

{% tabs %}
{% tab title="Query" %}

```json
{
  "unbonding": {
    "address": "migaloo1...",
    "denom": "ampWHALE",
    "start_after": "1337",
    "limit": "10"
  }
}
```

| Key           | Type            | Description                                          |
|---------------|-----------------|------------------------------------------------------|
| `address`     | String          | The address to run the query on                      |
| `denom`       | String          | The denom to check the unbonding amounts for         |
| `start_after` | Option\<String> | If paginating, the block to start the lookup from    |
| `limit`       | Option\<u8>     | If paginating, The maximum number of items to return |

{% endtab %}

{% tab title="Response (UnbondingResponse)" %}

```json
{
  "total_amount": "1000",
  "unbonding_requests": [
    {
      "asset": {
        "amount": "500",
        "info": {
          "native_token": {
            "denom": "ampWHALE"
          }
        }
      },
      "timestamp": "1698851118",
      "weight": "15000"
    }
  ]
}
```

| Key                  | Type       | Description                                                                                              |
|----------------------|------------|----------------------------------------------------------------------------------------------------------|
| `total_amount`       | Uint128    | How much in total the address is unbonding. Again, all LSDs are considered fungible for this calculation |
| `unbonding_requests` | Vec\<Bond> | The list of Bonds currently unbonding                                                                    |

{% endtab %}
{% endtabs %}

### Withdrawable

Returns the amount of unbonding tokens of the given denom for the specified address that can
be withdrawn, i.e. that have passed the unbonding period.

{% tabs %}
{% tab title="Query" %}

```json
{
  "withdrawable": {
    "address": "migaloo1...",
    "denom": "ampWHALE"
  }
}
```

| Key       | Type     | Description           |
|-----------|----------|-----------------------|
| `address` | `String` | The address to query. |
| `denom`   | `String` | The denom to query.   |

{% endtab %}

{% tab title="Response (WithdrawableResponse)" %}

```json
{
  "withdrawable_amount": "1000"
}
```

| Key                   | Type    | Description                                                 |
|-----------------------|---------|-------------------------------------------------------------|
| `withdrawable_amount` | Uint128 | The total amount that is withdrawable for the queried denom |

{% endtab %}
{% endtabs %}

### Weight

Returns the weight of the address.

{% tabs %}
{% tab title="Query" %}

```json
{
  "weight": {
    "address": "migaloo1",
    "timestamp": "1698851118",
    "global_weight": "1500"
  }
}
```

| Key             | Type                 | Description                                    |
|-----------------|----------------------|------------------------------------------------|
| `address`       | String               | The address to query.                          |
| `timestamp`     | Option\<Timestamp>   | The timestamp at which to query the weight     |
| `global_weight` | Option\<GlobalIndex> | The GlobalIndex to be used to query the weight |

{% endtab %}

{% tab title="Response (BondingWeightResponse)" %}

```json
{
  "address": "migaloo1...",
  "weight": "1500",
  "global_weight": "3000",
  "share": "0.5",
  "timestamp": "1698851118"
}
```

| Key             | Type      | Description                                                                                 |
|-----------------|-----------|---------------------------------------------------------------------------------------------|
| `address`       | String    | The address being queried                                                                   |
| `weight`        | Uint128   | The weight of the address                                                                   |
| `global_weight` | Uint128   | The total weight in the contract, i.e. the sum of all weights held by all bonding addresses |
| `share`         | Decimal   | The share of the contract                                                                   |
| `timestamp`     | Timestamp | The timestamp for this weight result                                                        |

{% endtab %}
{% endtabs %}

### TotalBonded

Returns the total amount of assets that have been bonded to the contract.

{% tabs %}
{% tab title="Query" %}

```json
{
  "total_bonded": {}
}
```

{% endtab %}

{% tab title="Response (BondedResponse)" %}

```json
{
  "total_bonded": "3000",
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
  "first_bonded_epoch_id": "0"
}
```

| Key                     | Type        | Description                                                                            |
|-------------------------|-------------|----------------------------------------------------------------------------------------|
| `total_bonded`          | Uint128     | How much in total is bonded in the contract                                            |
| `bonded_assets`         | Vec\<Asset> | The list of LSDs bonded in the contract                                                |
| `first_bonded_epoch_id` | Uint64      | Not used for this query, yet it's here since we reuse the same response type as before |

{% endtab %}
{% endtabs %}

### GlobalIndex

Returns the global index of the contract.

{% tabs %}
{% tab title="Query" %}

```json
{
  "global_index": {}
}
```

{% endtab %}

{% tab title="Response (GlobalIndex)" %}

```json
{
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
```

| Key             | Type        | Description                                            |
|-----------------|-------------|--------------------------------------------------------|
| `bonded_amount` | Uint128     | How much in total is bonded in the contract            |
| `bonded_assets` | Vec\<Asset> | The list of LSDs bonded in the contract                |
| `timestamp`     | Timestamp   | The timestamp at which the total bond was registered   |
| `weight`        | Uint64      | The total weight of the bond at the given block height |

{% endtab %}
{% endtabs %}

## MigrateMsg

```json
{}
```
