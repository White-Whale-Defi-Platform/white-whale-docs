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
{% endtab %}
{% endtabs %}

### Get payback amount

Retrieves the `Uint128` amount that must be sent back to the contract to pay off a loan taken out, in a `PaybackAmountResponse` response.

{% tabs %}
{% tab title="Query" %}
```json
{
  "get_payback_amount": {
    "amount": "10000"
  }
}
```
{% endtab %}

{% tab title="Response" %}
```json
{
  "payback_amount": "10030",
  "protocol_fee": "10",
  "flash_loan_fee": "20"
}
```
{% endtab %}
{% endtabs %}

### Protocol fees

Retrieves the protocol fees on the vault. If `all_time` is `true`, it will return the fees collected since 
the inception of the vault. On the other hand, if `all_time` is set to `false`, only the fees that has been accrued by 
the vault but not collected by the fee collector will be returned.

{% tabs %}
{% tab title="Query" %}
```json
{
  "protocol_fees": {
    "all_time": false
  }
}
```
{% endtab %}

{% tab title="Response" %}
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
{% endtab %}
{% endtabs %}

### Share

Retrieves the share of the assets stored in the vault that a given `amount` of lp tokens is entitled to in a `Uint128` response.

{% tabs %}
{% tab title="Query" %}
```json
{
  "share": {
    "amount": "1000"
  }
}
```
{% endtab %}

{% tab title="Response" %}
```json
{
  "data": "10002558"
}
```
{% endtab %}
{% endtabs %}
