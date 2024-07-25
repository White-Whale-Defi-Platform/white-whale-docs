# Vault Manager

## Instantiate

Instantiates an instance of the vault manager contract

```json
{
  "owner": "migaloo1...",
  "bonding_manager_addr": "migaloo1...",
  "vault_creation_fee": {
    "denom": "uwhale",
    "amount": "1000"
  }
}
```

| Key                    | Type   | Description                                                      |
|------------------------|--------|------------------------------------------------------------------|
| `owner`                | String | The owner of the contract                                        |
| `bonding_manager_addr` | String | The bonding manager address, where protocol fees are distributed |
| `vault_creation_fee`   | Coin   | The fee to create a vault                                        |

## ExecuteMsg

### CreateVault

Creates a new vault given the asset info the vault should manage deposits and withdrawals for and the fees.

```json
{
  "create_vault": {
    "asset_denom": "migaloo1...",
    "fees": {
      "protocol_fee": {
        "share": "0.001"
      },
      "flash_loan_fee": {
        "share": "0.002"
      }
    },
    "vault_identifier": "vault_identifier"
  }
}
```

| Key                | Type            | Description                                       |
|--------------------|-----------------|---------------------------------------------------|
| `asset_denom`      | String          | The asset to create a vault for.                  |
| `fees`             | VaultFee        | The fees associated with the vault                |
| `vault_identifier` | Option\<String> | The identifier associated with the vault, if any. |

### UpdateConfig

Updates the configuration of the vault manager. If a field is not specified, it will not be modified.

```json
{
  "update_config": {
    "bonding_manager_addr": "migaloo1...",
    "vault_creation_fee": {
      "denom": "uwhale",
      "amount": "1000"
    },
    "flash_loan_enabled": true,
    "deposit_enabled": true,
    "withdraw_enabled": true
  }
}
```

| Key                    | Type            | Description                      |
|------------------------|-----------------|----------------------------------|
| `bonding_manager_addr` | Option\<String> | The new bonding manager address. |
| `vault_creation_fee`   | Option\<String> | The new vault creation fee.      |
| `flash_loan_enabled`   | Option\<bool>   | If flash loans are enabled.      |
| `deposit_enabled`      | Option\<bool>   | If deposits are enabled.         |
| `withdraw_enabled`     | Option\<bool>   | If withdrawals are enabled.      |

### Deposit

Deposits a given asset into the vault manager. The asset must be send together with the message.

```json
{
  "deposit": {
    "vault_identifier": "vault_identifier_123"
  }
}
```

| Key                | Type   | Description                                        |
|--------------------|--------|----------------------------------------------------|
| `vault_identifier` | String | The vault identifier of the vault to deposit into. |

### Withdraw

Withdraws from the vault manager. The LP token must be sent together with the message.

```json
{
  "withdraw": {}
}
```

### FlashLoan

Retrieves the desired `asset` and runs the `payload`, paying the required amount back to the vault after running the
messages in the payload, and returning the profit to the sender.

```json
{
  "flash_loan": {
    "asset": {
      "denom": "uluna",
      "amount": "1000"
    },
    "vault_identifier": "vault_identifier_123",
    "payload": [
      {
        "wasm": {
          "execute": {
            "msg": "eyJzd2FwIjp7Im1heF9zcHJlYWQiOiIwLjA1Iiwib2ZmZXJfYXNzZXQiOnsiYW1vdW50IjoiMjk4MzAzOTIiLCJpbmZvIjp7Im5hdGl2ZV90b2tlbiI6eyJkZW5vbSI6InVsdW5hIn19fSwiYmVsaWVmX3ByaWNlIjoiMC42NDk5NTcifX0=",
            "funds": [
              {
                "denom": "uluna",
                "amount": "29830392"
              }
            ],
            "contract_addr": "terra1fd68ah02gr2y8ze7tm9te7m70zlmc7vjyyhs6xlhsdmqqcjud4dql4wpxr"
          }
        }
      },
      {
        "wasm": {
          "execute": {
            "msg": "eyJzd2FwIjp7Im1heF9zcHJlYWQiOiIwLjA1Iiwib2ZmZXJfYXNzZXQiOnsiYW1vdW50IjoiNDU4OTU5NjciLCJpbmZvIjp7Im5hdGl2ZV90b2tlbiI6eyJkZW5vbSI6ImliYy9CMzUwNEUwOTI0NTZCQTYxOENDMjhBQzY3MUE3MUZCMDhDNkNBMEZEMEJFN0M4QTVCNUEzRTJERDkzM0NDOUU0In19fSwiYmVsaWVmX3ByaWNlIjoiMC4wNjUzMTYifX0=",
            "funds": [
              {
                "denom": "ibc/B3504E092456BA618CC28AC671A71FB08C6CA0FD0BE7C8A5B5A3E2DD933CC9E4",
                "amount": "45895967"
              }
            ],
            "contract_addr": "terra1w579ysjvpx7xxhckxewk8sykxz70gm48wpcuruenl29rhe6p6raslhj0m6"
          }
        }
      },
      {
        "wasm": {
          "execute": {
            "msg": "eyJzZW5kIjp7ImFtb3VudCI6IjcwMjY3MDc3NyIsImNvbnRyYWN0IjoidGVycmExZTZ0MzdmZ2preHJ6ZHgyczk1ZnlxNmpkcmE1czgyNzIwdmh0bXh2eDR5aGN2bnNyZXk0c3NtcnlhNiIsIm1zZyI6ImV5SnpkMkZ3SWpwN0ltSmxiR2xsWmw5d2NtbGpaU0k2SWpJekxqSTJOall5T0NJc0ltMWhlRjl6Y0hKbFlXUWlPaUl3TGpBd01EVWlmWDA9In19",
            "funds": [],
            "contract_addr": "terra1nsuqsk6kh58ulczatwev87ttq2z6r3pusulg9r24mfj2fvtzd4uq3exn26"
          }
        }
      }
    ]
  }
}
```

| Key                | Type            | Description                               |
|--------------------|-----------------|-------------------------------------------|
| `asset`            | Coin            | The asset to flash-loan.                  |
| `vault_identifier` | String          | The vault identifier to flash-loan from.  |
| `payload`          | Vec\<CosmosMsg> | The messages to run after the flash-loan. |

### Callback

Callback message for post-processing flash-loans.

```json
{
  "callback": {
    "after_flash_loan": {
      "old_asset_balance": "100000",
      "loan_asset": {
        "denom": "uluna",
        "amount": "1000"
      },
      "vault_identifier": "vault_identifier_123",
      "sender": "migaloo1..."
    }
  }
}
```

| Key                 | Type    | Description                                                                          |
|---------------------|---------|--------------------------------------------------------------------------------------|
| `old_asset_balance` | Uint128 | The contract balance of the asset that was borrowed before the flash-loan was taken. |
| `loan_asset`        | Coin    | The amount of the asset that was borrowed                                            |
| `vault_identifier`  | String  | The identifier of the vault that the flash-loan was taken from.                      |
| `sender`            | Addr    | The original sender of the flash-loan                                                |
