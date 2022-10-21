# Vault Factory

The vault factory contract is used to create vaults. Similarly to the pool factory, the vault factory acts as a 
directory for the vaults that have been created through the factory. Note that **the vault factory is permissioned**, meaning 
the messages can only be executed by the owner of the contract.

The code for the vault factory contract can be found [here](https://github.com/White-Whale-Defi-Platform/migaloo-core/tree/main/contracts/liquidity_hub/vault-network/vault_factory).

---

The following are the messages that can be executed on the vault factory:

## Instantiate

Instantiates the vault factory. Requires storing the vault and token contracts in advance so that the contract code ids 
can be provided.

```json
{
  "owner": "inj1...",
  "vault_id": 123,
  "token_id": 456,
  "fee_collector_addr": "inj1..."
}
```

| Key                  | Type   | Description                                  |
| -------------------- | ------ | -------------------------------------------- |
| `owner`              | String | The owner of the factory                     |
| `vault_id`           | u64    | The code ID for the vault contract           |
| `token_id`           | u64    | The code ID for the liquidity token contract |
| `fee_collector_addr` | String | The address where fees get collected         |

## Migrate

Migrates the vault factory.

```json
{}
```

## ExecuteMsg

### Create vault (native/ibc)

Creates a vault. Includes token info and vault fees.

{% tabs %}
{% tab title="Native/IBC token" %}
```json
{
  "create_vault" : {
    "asset_info": {
      "native_token": {
        "denom": "uluna"
      }
    },
    "fees": {
      "protocol_fee": {
        "share": "0.01"
      },
      "flash_loan_fee": {
        "share": "0.02"
      }
    }
  }
}

```
{% endtab %}

{% tab title="CW20 token" %}
```json
{
  "create_vault" : {
    "asset_info": {
      "token": {
        "contract_addr": "inj1..."
      }
    },
    "fees": {
      "protocol_fee": {
        "share": "0.01"
      },
      "flash_loan_fee": {
        "share": "0.02"
      }
    }
  }
}
```
{% endtab %}
{% endtabs %}


| Key          | Type      | Description                       |
| ------------ | --------- | --------------------------------- |
| `asset_info` | AssetInfo | Asset info to create a vault with |
| `fees`       | VaultFee  | Fees for the vault                |


### Migrate vaults

Migrates vault contracts to the given vault code id. If `vault_addr` is provided, the message migrates only that given vault. 
Otherwise, it migrates all the vaults created by the factory.

```json
{
  "migrate_vaults": {
    "vault_addr": "inj1...",
    "vault_code_id": 666
  }
}
```

| Key             | Type            | Description                                 |
| --------------- | --------------- | ------------------------------------------- |
| `vault_addr`    | Option\<String> | Vault address to migrate                    |
| `vault_code_id` | u64             | Code id of the vault contract to migrate to |

### Update config

Updates the configuration of the vault factory.

```json
{
  "update_config": {
    "owner": "inj1...",
    "fee_collector_addr": "inj1...",
    "vault_id": 123,
    "token_id": 456
  }
}
```

| Key                  | Type            | Description                                   |
| -------------------- | --------------- | --------------------------------------------- |
| `owner`              | Option\<String> | New owner of the factory                      |
| `fee_collector_addr` | Option\<String> | New fee collector address                     |
| `vault_id`           | Option\<u64>    | New code id for creating vault contracts with |
| `token_id`           | Option\<u64>    | New code id for the token contract            |

### Update vault config

Updates the configuration of the given vault with the provided `UpdateConfigParams`.

```json
{
  "update_vault_config": {
    "vault_addr": "inj1...",
    "params": {
      "flash_loan_enabled" : true,
      "deposit_enabled" : true,
      "withdraw_enabled" : true,
      "new_owner" : "inj1...",
      "new_vault_fees" : {
        "protocol_fee": {
          "share": "0.02"
        },
        "flash_loan_fee": {
          "share": "0.03"
        }
      },
      "new_fee_collector_addr" : "inj1..."
    }
  }
}
```

| Key          | Type               | Description                          |
| ------------ | ------------------ | ------------------------------------ |
| `vault_addr` | String             | Vault address                        |
| `params`     | UpdateConfigParams | Parameters to update the config with |


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

{% tab title="Response (Config)" %}
```json
{
  "owner": "inj1...",
  "vault_id": 999,
  "token_id": 888,
  "fee_collector_addr": "inj1..."
}
```

| Key                  | Type | Description                    |
| -------------------- | ---- | ------------------------------ |
| `owner`              | Addr | The factory owner              |
| `vault_id`           | u64  | Code id for the vault contract |
| `token_id`           | u64  | Code id for the token contract |
| `fee_collector_addr` | Addr | Fee collector address          |


{% endtab %}
{% endtabs %}

### Vault

Retrieves the vault address given the `AssetInfo`.

{% tabs %}
{% tab title="Query (native/IBC token)" %}
```json
{
  "vault": {
    "asset_info": {
      "native_token": {
        "denom": "ujuno"
      }
    }
  }
}
```

| Key          | Type      | Description                                        |
| ------------ | --------- | -------------------------------------------------- |
| `asset_info` | AssetInfo | Asset info of the vault to retrieve the address of |


{% endtab %}

{% tab title="Query (cw20 token)" %}
```json
{
  "vault": {
    "asset_info": {
      "token": {
        "contract_addr": "juno1..."
      }
    }
  }
}
```

| Key          | Type      | Description                                        |
| ------------ | --------- | -------------------------------------------------- |
| `asset_info` | AssetInfo | Asset info of the vault to retrieve the address of |


{% endtab %}

{% tab title="Response (Option<String>)" %}
```json
{
  "data": "juno1..."
}
```

| Key    | Type            | Description                        |
|--------|-----------------|------------------------------------|
| `data` | Option\<String> | Address of the vault, if it exists |


{% endtab %}
{% endtabs %}

### Vaults

Retrieves the addresses for all the vaults. Returns an `Option<Vec<String>>`.

{% tabs %}
{% tab title="Query" %}
```json
{
  "vaults": {
    "start_after": [
      117,
      106,
      117,
      110,
      111
    ],
    "limit": 10
  }
}
```

| Key           | Type             | Description                                                |
| ------------- | ---------------- | ---------------------------------------------------------- |
| `start_after` | Option\<Vec<u8>> | Asset info reference (as bytes) to paginate from           |
| `limit`       | Option\<u32>     | How many items to fetch at once. Default is `10`, max `30` |

{% endtab %}

{% tab title="Response (VaultsResponse)" %}
```json
{
  "vaults": [
    {
      "vault": "juno1...",
      "asset_info_reference": [
        1,
        2,
        3,
        4,
        5,
        6
      ]
    },
    {
      "vault": "juno1...",
      "asset_info_reference": [
        1,
        2,
        3,
        4,
        5,
        6
      ]
    }
  ]
}
```

| Key      | Type            | Description                        |
| -------- | --------------- | ---------------------------------- |
| `vaults` | Vec\<VaultInfo> | Vault infos for the queried vaults |

{% endtab %}
{% endtabs %}
