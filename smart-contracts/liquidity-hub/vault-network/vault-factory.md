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

{% tab title="Response" %}
```json
{
  "owner": "inj1...",
  "vault_id": 999,
  "token_id": 888,
  "fee_collector_addr": "inj1..."
}
```
{% endtab %}
{% endtabs %}

### Vault (native/ibc)

Retrieves the vault address given the `AssetInfo`.

{% tabs %}
{% tab title="Query" %}
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
{% endtab %}

{% tab title="Response" %}
```json
{
  "data": "juno1..."
}
```
{% endtab %}
{% endtabs %}

### Vault (cw20)

Retrieves the vault address given the `AssetInfo`.

{% tabs %}
{% tab title="Query" %}
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
{% endtab %}

{% tab title="Response" %}
```json
{
  "data": "juno1..."
}
```
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
{% endtab %}

{% tab title="Response" %}
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
{% endtab %}
{% endtabs %}
