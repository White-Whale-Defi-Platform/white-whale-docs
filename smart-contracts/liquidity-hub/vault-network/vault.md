# Vault

The vault contract is a single-asset pool, used by bots to take flash-loans.

The following are the messages that can be executed on the vault:


## Instantiate (native)

```json
{
  "owner": "inj1...",
  "asset_info": {
    "native_token": {
      "denom": "inj"
    }
  },
  "token_id": 123,
  "vault_fees": {
    "protocol_fee": {
      "share": "0.01"
    },
    "flash_loan_fee": {
      "share": "0.02"
    }
  },
  "fee_collector_addr": "inj1..."
}
```

## Instantiate (cw20)

```json
{
  "owner": "juno1...",
  "asset_info": {
    "token": {
      "contract_addr": "juno1..."
    }
  },
  "token_id": 123,
  "vault_fees": {
    "protocol_fee": {
      "share": "0.01"
    },
    "flash_loan_fee": {
      "share": "0.02"
    }
  },
  "fee_collector_addr": "juno1..."
}
```

## Migrate

```json
{}
```

## ExecuteMsg

### Callback (to be called internally by the contract)


```json
{
  "callback": {
    "after_trade": {
      "old_balance": "10000",
      "loan_amount": "10000"
    }
  }
}
```

### Collect protocol fees

```json
{
  "collect_protocol_fees": {}
}
```

### Deposit

```json
{
  "deposit": {
    "amount": "1000"
  }
}
```

### Flashloan

```json
{
  "flash_loan": {
    "amount": "1000",
    "msg": ""
  }
}
```

the `msg` is a message in base64 of the operations to be executed with the flashloan.

### Update config

```json
{
  "update_config": {
    "flash_loan_enabled": true,
    "deposit_enabled": true,
    "withdraw_enabled": true,
    "new_owner": "inj1...",
    "new_vault_fees": {
      "protocol_fee": {
        "share": "0.01"
      },
      "flash_loan_fee": {
        "share": "0.02"
      }
    },
    "new_fee_collector_addr": "inj1..."
  }
}
```

## Queries

### Config

```json
{
  "config": {}
}
```

### Get payback amount

```json
{
  "get_payback_amount": {
    "amount": "10000"
  }
}
```

### Protocol fees

```json
{
  "protocol_fees": {
    "all_time": false
  }
}
```

### Share

```json
{
  "share": {
    "amount": "1000"
  }
}
```

## Query responses


### Config

```json
{
  "owner": "juno1...",
  "asset_info": {
    "native_token": {
      "denom": "ujuno"
    }
  },
  "flash_loan_enabled": true,
  "deposit_enabled": true,
  "withdraw_enabled": true,
  "liquidity_token": "juno1...",
  "fee_collector_addr": "juno1...",
  "fees": {
    "protocol_fee": {
      "share": "0.001"
    },
    "flash_loan_fee": {
      "share": "0.002"
    }
  }
}
```

### Get payback amount

```json
{
  "payback_amount": "10030",
  "protocol_fee": "10",
  "flash_loan_fee": "20"
}
```

### Protocol fees (native)

```json
{
  "fees": {
    "info": {
      "native_token": {
        "denom": "ujuno"
      }
    },
    "amount": "47516"
  }
}
```

### Protocol fees (cw20)

```json
{
  "fees": {
    "info": {
      "token": {
        "contract_addr": "juno1..."
      }
    },
    "amount": "10000"
  }
}
```

### Share

```json
{
  "data": "10002558"
}
```