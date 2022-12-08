# Factory

Migaloo's factory contract is used to create pair (pool) contracts. Pools are comprised of two tokens, which can be either 
native, ibc or cw20 tokens. Once a pool is created it's stored in state, meaning the factory acts as a pool registry, which 
can be queried for reference. Note that **the pool factory is permissioned**, meaning the messages can only be executed by the 
owner of the contract.

## Create a pair

Creating a pair (pool) can be done via the `create_pair` message. Note that for creating pools with native or ibc tokens,
`add_native_token_decimals` should be called in advance with a small amount of the desired asset (say one micro unit). This 
is used to whitelist native/ibc tokens, allowing pools to be created with those.

The code for the Factory contract can be found [here](https://github.com/White-Whale-Defi-Platform/migaloo-core/tree/main/contracts/liquidity_hub/pool-network/terraswap_factory).

---

The following are the messages that can be executed on the factory:

## Instantiate

Instantiates the pool factory.

```json
{
  "pair_code_id": 1,
  "token_code_id": 2,
  "fee_collector_addr": "fee_collector_addr"
}
```

| Key                  | Type   | Description                           |
| -------------------- | ------ | ------------------------------------- |
| `pair_code_id`       | u64    | Code id for the pair/pool contract    |
| `token_code_id`      | u64    | Code id for the token contract        |
| `fee_collector_addr` | String | Address of the fee collector contract |


## Migrate

Migratest the pool factory.

```json
{}
```

## ExecuteMsg

### Add Native Token Decimals

Used to validate native or ibc tokens, adding them to a whitelist so pools can be created with them. Along with this 
message, a small amount of the token should be transferred.

```json
{
  "add_native_token_decimals": {
    "denom": "ujuno",
    "decimals": 6
  }
}
```

| Key        | Type   | Description                   |
| ---------- | ------ | ----------------------------- |
| `denom`    | String | denom of the native/ibc asset |
| `decimals` | u8     | Decimal places for that asset |

### Create pair

Creates a pool with the given assets and pool fees. If the pool already exists, the transaction will fail.

```json
{
  "create_pair": {
    "asset_infos": [
      {
        "native_token": {
          "denom": "uluna"
        }
      },
      {
        "token": {
          "contract_addr": "terra1..."
        }
      }
    ],
    "pool_fees": {
      "protocol_fee": {
        "share": "0.001"
      },
      "swap_fee": {
        "share": "0.003"
      }
    }
  }
}
```

| Key           | Type           | Description                                              |
| ------------- | -------------- | -------------------------------------------------------- |
| `asset_infos` | [AssetInfo; 2] | Information about the two assets to create the pair with |
| `pool_fees`   | PoolFee        | Pool fees for the given pair                             |

### Migrate pair

Migrates a pool with the given address to the desired code id.

```json
{
  "migrate_pair": {
    "contract": "pair_address",
    "code_id": 123
  }
}
```

| Key        | Type         | Description                                     |
| ---------- |--------------| ----------------------------------------------- |
| `contract` | String       | Pair contract address to be migrated            |
| `code_id`  | Option\<u64> | Code id for the pair contract to be migrated to |

### Remove pair

Removes a pair for the pool registry. Note that the pool will still live on the blockchain, this action though will make it
invisible to the factory, meaning it will be orphan by the protocol. This action could be used  in case a pool is no longer 
desired, e.g. if a pool was set up incorrectly (and can't be fixed by updating the config). Ideally, this should only be done 
after the pool's liquidity has been withdrawn or migrated.

```json
{
  "remove_pair": {
    "asset_infos": [
      {
        "native_token": {
          "denom": "uluna"
        }
      },
      {
        "token": {
          "contract_addr": "terra1..."
        }
      }
    ]
  }
}
```

| Key           | Type           | Description                                                              |
| ------------- | -------------- |--------------------------------------------------------------------------|
| `asset_infos` | [AssetInfo; 2] | Asset infos of the Pair contract to be removed from the factory registry |

### Update config

Updates the configuration of the factory.

```json
{
  "update_config": {
    "owner": "owner",
    "fee_collector_addr": "fee_collector_addr",
    "token_code_id": 123,
    "pair_code_id": 456
  }
}
```

| Key                  | Type            | Description                                                                            |
| -------------------- |-----------------| -------------------------------------------------------------------------------------- |
| `owner`              | Option\<String> | New owner of the contract                                                              |
| `fee_collector_addr` | Option\<String> | New fee collector address                                                              |
| `token_code_id`      | Option\<u64>    | New code id for the token contract, used by the pair contract to create LP tokens from |
| `pair_code_id`       | Option\<u64>    | New code id for the pair contract, used by the factory to create pools from            |

### Update pair config

Updates the configuration of the pair created by the factory.

```json
{
  "update_pair_config": {
    "pair_addr": "pair_contract_addr",
    "fee_collector_addr": "fee_collector_addr",
    "pool_fees": {
      "protocol_fee": {
        "share": "0.001"
      },
      "swap_fee": {
        "share": "0.002"
      }
    },
    "feature_toggle": {
      "withdrawals_enabled": true,
      "deposits_enabled": true,
      "swaps_enabled": true
    }
  }
}
```

| Key                  | Type                   | Description                                |
| -------------------- | ---------------------- | ------------------------------------------ |
| `pair_addr`          | String                 | Pair contract address to update the config |
| `owner`              | Option\<String>        | New owner address                          |
| `fee_collector_addr` | Option\<String>        | New fee collector address                  |
| `pool_fees`          | Option\<PoolFee>       | New pool fees                              |
| `feature_toggle`     | Option\<FeatureToggle> | New feature toggle options for the pool    |

## Queries

### Config

Retrieves the configuration of the factory.

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
  "owner": "juno1...",
  "fee_collector_addr": "juno1...",
  "pair_code_id": 123,
  "token_code_id": 456
}
```

| Key                  | Type   | Description                    |
| -------------------- | ------ | ------------------------------ |
| `owner`              | String | Contract's owner address       |
| `fee_collector_addr` | String | Fee collector contract address |
| `pair_code_id`       | u64    | Code id for the pair contract  |
| `token_code_id`      | u64    | Code id for the token contract |


{% endtab %}
{% endtabs %}

### Native token decimals

Retrieves the native token decimals for the given `denom`.

{% tabs %}
{% tab title="Query" %}
```json
{
  "native_token_decimals": {
    "denom": "ujuno"
  }
}
```

| Key                  | Type   | Description                               |
|----------------------| ------ |-------------------------------------------|
| `denom`              | String | Native or IBC denom to query decimals for |


{% endtab %}

{% tab title="Response (NativeTokenDecimalsResponse)" %}
```json
{
  "decimals": 6
}
```

| Key        | Type | Description                                      |
| ---------- | ---- | ------------------------------------------------ |
| `decimals` | u8   | Native or IBC denom decimals for the given denom |

{% endtab %}
{% endtabs %}

### Pair

Retrieves pool information for a given pair.

{% tabs %}
{% tab title="Query" %}
```json
{
  "pair": {
    "asset_infos": [
      {
        "native_token": {
          "denom": "ujuno"
        }
      },
      {
        "token": {
          "contract_addr": "juno1..."
        }
      }
    ]
  }
}
```

| Key           | Type           | Description                                    |
| ------------- | -------------- | ---------------------------------------------- |
| `asset_infos` | [AssetInfo; 2] | Asset info for the pair to retrieve info about |

{% endtab %}

{% tab title="Response (PairInfo)" %}
```json
{
  "asset_infos": [
    {
      "native_token": {
        "denom": "ujuno"
      }
    },
    {
      "token": {
        "contract_addr": "juno1..."
      }
    }
  ],
  "contract_addr": "juno1...",
  "liquidity_token": "juno1...",
  "asset_decimals": [
    6,
    6
  ]
}
```

| Key               | Type           | Description                             |
| ----------------- | -------------- | --------------------------------------- |
| `asset_infos`     | [AssetInfo; 2] | Asset infos for the pair                |
| `contract_addr`   | String         | Pair contract address                   |
| `liquidity_token` | String         | LP token contract address for the pair  |
| `asset_decimals`  | [u8; 2]        | Decimals for the assets within the pool |

{% endtab %}
{% endtabs %}

### Pairs

Retrieves multiple pool informations. Considering the pool registry can get extensive, pagination is possible. The default 
limit for the query is `10`, while the maximum is `30`.

{% tabs %}
{% tab title="Query" %}
```json
{
  "pairs": {
    "start_after": [
      {
        "token": {
          "contract_addr": "juno1..."
        }
      },
      {
        "native_token": {
          "denom": "ujuno"
        }
      }
    ],
    "limit": 30
  }
}
```

| Key           | Type                    | Description                                                    |
| ------------- |-------------------------| -------------------------------------------------------------- |
| `start_after` | Option\<[AssetInfo; 2]> | Asset infos to start fetching from (when pagination is needed) |
| `limit`       | Option\<u32>            | How many items to fetch at once. Default is `10`, max `30`     |

{% endtab %}

{% tab title="Response (PairsResponse)" %}
```json
{
  "pairs": [
    {
      "asset_infos": [
        {
          "native_token": {
            "denom": "ujuno"
          }
        },
        {
          "token": {
            "contract_addr": "juno1..."
          }
        }
      ],
      "contract_addr": "juno1...",
      "liquidity_token": "juno1...",
      "asset_decimals": [
        6,
        6
      ]
    },
    {
      "asset_infos": [
        {
          "native_token": {
            "denom": "ujuno"
          }
        },
        {
          "native_token": {
            "denom": "ibc/107D152BB3176FAEBF4C2A84C5FFDEEA7C7CB4FE1BBDAB710F1FD25BCD055CBF"
          }
        }
      ],
      "contract_addr": "juno1...",
      "liquidity_token": "juno1...",
      "asset_decimals": [
        6,
        6
      ]
    }
  ]
}
```

| Key     | Type           | Description                                       |
|---------|----------------|---------------------------------------------------|
| `pairs` | Vec\<PairInfo> | Vector with information about the requested pairs |

{% endtab %}
{% endtabs %}
