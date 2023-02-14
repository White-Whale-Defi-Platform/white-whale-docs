# Vault Router

The vault router contract is a convenient way to take flash loans from White Whale vaults. Instead of interacting with 
individual vaults, bots can request the vault router the desired asset to do the flash loan operation with and the router 
will take care of communicating and requesting the funds to the appropriate vault.

An interesting feature that the White Whale Vault Router is pioneering is the possibility to take multiple flash loans at 
once.

The code for the vault router can be found [here](https://github.com/White-Whale-Defi-Platform/white-whale-core/tree/main/contracts/liquidity_hub/vault-network/vault_router).

---

The following are the messages that can be executed on the vault router:

## Instantiate

Instantiates the vault router.

```json
{
  "owner": "inj1...",
  "vault_factory_addr": "inj1..."
}
```

| Key                  | Type   | Description                       |
| -------------------- | ------ | --------------------------------- |
| `owner`              | String | The owner of the router           |
| `vault_factory_addr` | String | The address for the vault factory |

## Migrate

Migrates the vault router.

```json
{}
```

## ExecuteMsg

## Flashloan

Retrieves the desired `assets` and runs the `msgs`, paying the required amount back the vaults after running the messages, 
and returning the profit to the sender.

```json
{
  "assets": [
    {
      "info": {
        "native_token": {
          "denom": "ujuno"
        }
      },
      "amount": "10000"
    }
  ],
  "msgs": [
    {
      "wasm": {
        "execute": {
          "contract_addr": "juno1...",
          "msg": "binary",
          "funds": []
        }
      }
    }
  ]
}
```

| Key      | Type            | Description                                    |
|----------|-----------------|------------------------------------------------|
| `assets` | Vec\<Asset>     | Desired assets for the flash loan(s)           |
| `msg`    | Vec\<CosmosMsg> | Messages to be executed with the flash loan(s) |


## Next loan

Performs the next loan in case multiple flash loans are taken. This message is called internally by the vault where the 
flash loan is being taken from. Cannot be called manually.

```json
{
  "next_loan": {
    "initiator": "juno1...",
    "payload": [
      {
        "wasm": {
          "execute": {
            "contract_addr": "juno1...",
            "msg": "binary",
            "funds": []
          }
        }
      }
    ],
    "to_loan": [
      [
        "juno1...",
        {
          "info":{
            "native_token":{
              "denom":"ujunox"
            }
          },
          "amount":"10000"
        }
      ]
    ],
    "loaned_assets": [
      [
        "juno1...",
        {
          "info":{
            "native_token":{
              "denom":"ujunox"
            }
          },
          "amount":"10000"
        }
      ]
    ]
  }
}
```

| Key             | Type                  | Description                                               |
| --------------- | --------------------- | --------------------------------------------------------- |
| `initiator`     | Addr                  | The address to pay back all profits to                    |
| `source_vault`  | String                | The vault contract that calls the `NextLoan message       |
| `payload`       | Vec\<CosmosMsg>       | The final message to run once all assets have been loaned |
| `to_loan`       | Vec\<(String, Asset)> | The next loans to run                                     |
| `loaned_assets` | Vec\<(String, Asset)> | The assets that have been loaned                          |

## Complete loan

Completes the flash-loan by paying back all outstanding loans, and returning profits to the sender. This message is called 
internally by the vault router, cannot be called manually.

```json
{
  "complete_loan": {
    "initiator": "juno1...",
    "loaned_assets": [
      [
        "juno1...",
        {
          "info":{
            "native_token":{
              "denom":"ujunox"
            }
          },
          "amount":"10000"
        }
      ]
    ]
  }
}
```

| Key             | Type                  | Description                                                                                                       |
| --------------- | --------------------- | ----------------------------------------------------------------------------------------------------------------- |
| `initiator`     | Addr                  | The address to pay back all profits to                                                                            |
| `loaned_assets` | Vec\<(String, Asset)> | A vec of tuples where the first value represents the vault address, and the second value represents the loan size |

## Update config

Updates the configuration of the vault router.

```json
{
   "update_config":{
      "owner":"juno1...",
      "vault_factory_addr":"juno1..."
   }
}
```

| Key                  | Type            | Description               |
|----------------------|-----------------|---------------------------|
| `owner`              | Option\<String> | New owner of the router   |
| `vault_factory_addr` | Option\<String> | New vault factory address |

## Queries

Retrieves the configuration of the vault router. Returns a `Config` struct.

### Config

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
  "owner": "juno1...",
  "vault_factory": "juno1..."
}
```

| Key                  | Type | Description               |
|----------------------|------|---------------------------|
| `owner`              | Addr | New owner of the router   |
| `vault_factory_addr` | Addr | New vault factory address |

{% endtab %}
{% endtabs %}
