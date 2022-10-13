# Vault Router

The vault router contract is a convenient way to take flash loans from White Whale vaults. Instead of interacting with 
individual vaults, bots can request the vault router the asset they need to do the flash loan operation and the router 
will take care of communicating and requesting the funds to the appropriate vault.

An interesting feature that the White Whale Vault Router is pioneering is the possibility to take multiple flash loans at 
once.

The following are the messages that can be executed on the vault router:

## Instantiate

```json
{
  "owner": "inj1...",
  "vault_factory_addr": "inj1..."
}
```

## Migrate

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

## Next loan

Performs the next loan in case multiple flash loans are taken.

This message is called internally by the vault where the flash loan is being taken from. Cannot be called manually.

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
      (
      {
        "juno1..."
      },
      {
        "info": {
          "native_token": {
            "denom": "ujuno"
          }
        },
        "amount": "10000"
      }
      )
    ],
    "loaned_assets": [
      (
      {
        "juno1..."
      },
      {
        "info": {
          "native_token": {
            "denom": "ujuno"
          }
        },
        "amount": "10000"
      }
      )
    ]
  }
}
```

## Complete loan

Completes the flash-loan by paying back all outstanding loans, and returning profits to the sender.

This message is called internally by the vault router, cannot be called manually.

```json
{
  "complete_loan": {
    "initiator": "juno1...",
    "loaned_assets": [
      (
      {
        "juno1..."
      },
      {
        "info": {
          "native_token": {
            "denom": "ujuno"
          }
        },
        "amount": "10000"
      }
      )
    ]
  }
}
```

## Update config

```json
{
  "owner": "juno1...",
  "vault_factory_addr": "juno1..."
}
```

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

{% tab title="Response" %}
```json
{
  "owner": "juno1...",
  "vault_factory": "juno1..."
}
```
{% endtab %}
{% endtabs %}
