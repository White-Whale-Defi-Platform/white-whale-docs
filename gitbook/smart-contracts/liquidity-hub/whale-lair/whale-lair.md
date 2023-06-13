# Whale Lair

The Whale Lair is a bonding contract used to bond WHALE LSDs.

## InstantiateMsg

```json
{
  "unbonding_period": "0",
  "growth_rate": "0",
  "bonding_assets": [
    {
      "native_token": {
        "denom": ""
      }
    }
  ]
}
```

| Key                | Type             | Description                                    |
| ------------------ | ---------------- | ---------------------------------------------- |
| `unbonding_period` | `Uint64`         | Unbonding period in nanoseconds.               |
| `growth_rate`      | `Decimal`        | Weight grow rate. Needs to be between 0 and 1. |
| `bonding_assets`   | `Vec<AssetInfo>` | [AssetInfo] of the assets that can be bonded.  |

## ExecuteMsg

### Bond

Bonds the specified [Asset]. This assumings the [Asset] is already white-listed for bonding.

```json
{
  "bond": {
    "info": {
      "native_token": {
        "denom": ""
      }
    },
    "amount": "0"
  }
}
```

| Key    | Type    | Description               |
| ------ | ------- | ------------------------- |
| `bond` | `Asset` | The [Asset] to be bonded. |

### Unbond

Unbonds the specified [Asset].

```json
{
  "unbond": {
    "info": {
      "native_token": {
        "denom": ""
      }
    },
    "amount": "0"
  }
}
```

| Key      | Type    | Description                 |
| -------- | ------- | --------------------------- |
| `unbond` | `Asset` | The [Asset] to be unbonded. |

### Withdraw

Sends withdrawable unbonded tokens to the user.

```json
{
  "withdraw": {
    "denom": ""
  }
}
```

| Key     | Type     | Description                             |
| ------- | -------- | --------------------------------------- |
| `denom` | `String` | The denom of the asset to be withdrawn. |

### UpdateConfig

Updates the [Config] of the contract.

```json
{
  "owner": "",
  "unbonding_period": "0",
  "growth_rate": "0",
  "fee_distributor_addr": ""
}
```

| Key                    | Type      | Description                                    |
| ---------------------- | --------- | ---------------------------------------------- |
| `owner`                | `String`  | The owner of the contract.                     |
| `unbonding_period`     | `Uint64`  | Unbonding period in nanoseconds.               |
| `growth_rate`          | `Decimal` | Weight grow rate. Needs to be between 0 and 1. |
| `fee_distributor_addr` | `String`  | The address of the fee distributor contract.   |

## QueryMsg

### Config

Returns the [Config] of te contract.

```json
{}
```

### Bonded

Returns the amount of assets that have been bonded by the specified address.

```json
{
  "address": ""
}
```

| Key       | Type     | Description           |
| --------- | -------- | --------------------- |
| `address` | `String` | The address to query. |

### Unbonding

Returns the amount of tokens of the given denom that are been unbonded by the specified address.

```json
{
  "address": "",
  "denom": "",
  "start_after": "0",
  "limit": "0"
}
```

| Key           | Type     | Description                            |
| ------------- | -------- | -------------------------------------- |
| `address`     | `String` | The address to query.                  |
| `denom`       | `String` | The denom to query.                    |
| `start_after` | `Uint64` | The start index for pagination.        |
| `limit`       | `Uint8`  | The maximum number of items to return. |

### Withdrawable

Returns the amount of unbonding tokens of the given denom for the specified address that can
be withdrawn, i.e. that have passed the unbonding period.

```json
{
  "address": "",
  "denom": ""
}
```

| Key       | Type     | Description           |
| --------- | -------- | --------------------- |
| `address` | `String` | The address to query. |
| `denom`   | `String` | The denom to query.   |

### Weight

Returns the weight of the address.

```json
{
  "address": "",
  "timestamp": "0",
  "global_weight": "0"
}
```

| Key             | Type        | Description                 |
| --------------- | ----------- | --------------------------- |
| `address`       | `String`    | The address to query.       |
| `timestamp`     | `Timestamp` | The timestamp to query.     |
| `global_weight` | `Uint128`   | The global weight to query. |

### TotalBonded

Returns the total amount of assets that have been bonded to the contract.

```json
{}
```

### GlobalIndex

Returns the global index of the contract.

```json
{}
```

## MigrateMsg

```json
{}
```

## BondedResponse

```json
{
  "total_bonded": "0",
  "bonded_assets": [
    {
      "info": {
        "native_token": {
          "denom": ""
        }
      },
      "amount": "0"
    }
  ]
}
```

| Key             | Type         | Description                                                       |
| --------------- | ------------ | ----------------------------------------------------------------- |
| `total_bonded`  | `Uint128`    | The total amount of assets that have been bonded to the contract. |
| `bonded_assets` | `Vec<Asset>` | The bonded assets.                                                |

## UnbondingResponse

```json
{
  "total_unbonding": "0",
  "unbonding_assets": [
    {
      "info": {
        "native_token": {
          "denom": ""
        }
      },
      "amount": "0"
    }
  ]
}
```

| Key                | Type         | Description                                                         |
| ------------------ | ------------ | ------------------------------------------------------------------- |
| `total_unbonding`  | `Uint128`    | The total amount of assets that have been unbonded to the contract. |
| `unbonding_assets` | `Vec<Asset>` | The unbonding assets.                                               |

## WithdrawableResponse

```json
{
  "total_withdrawable": "0",
  "withdrawable_assets": [
    {
      "info": {
        "native_token": {
          "denom": ""
        }
      },
      "amount": "0"
    }
  ]
}
```

| Key                   | Type         | Description                                                         |
| --------------------- | ------------ | ------------------------------------------------------------------- |
| `total_withdrawable`  | `Uint128`    | The total amount of assets that can be withdrawn from the contract. |
| `withdrawable_assets` | `Vec<Asset>` | The withdrawable assets.                                            |

## WeightResponse

```json
{
  "weight": "0"
}
```

| Key      | Type      | Description                |
| -------- | --------- | -------------------------- |
| `weight` | `Uint128` | The weight of the address. |
