# Vault

The vault contract is a single-asset pool, used by bots to take flash-loans. Depositors of tokens into flash loan vaults 
benefit from fees paid when their vault is accessed for flash loans; the greater the volume, the more fees generated. 
Flash loan vaults are a great source of yield with no impermanent loss.

## Fees

There are two types of fees associated to the vaults, namely `flash_loan_fee` and `protocol_fee`. The `flash_loan_fee` 
remains in the vault, which makes the share's value of the liquidity provides to increase, benefiting all LPs.

The `protocol_fee` goes to the protocol, and it is to be collected by the Fee Collector contract of the Liquidity Hub.
The protocol revenue is then distributed to WHALE stakers in the form of token buybacks.

## Feature toggle

Pools contain a feature toggle, containing the following properties: `withdraw_enabled`, `deposit_enabled` and `flash_loan_enabled`.
Those features are `ON` by default, but could be changed via governance. They could be changed in different scenarios, the ones
we could envision include for example if a critical bug is found in a given feature, it could be shut down while is being
fixed to avoid exploits. Additionally, if for example liquidity is desired to be migrated to another pool, deposits could
be disabled to prevent bots or users to deposit liquidity in the pool.

The code for the vault contract can be found [here](https://github.com/White-Whale-Defi-Platform/migaloo-core/tree/main/contracts/liquidity_hub/vault-network/vault).

---

The following are the messages that can be executed on the vault:

## Instantiate

Instantiates a vault. Includes providing information about the asset infos, token contract code id and fees among others.  

{% tabs %}
{% tab title="Native/IBC token" %}
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
{% endtab %}

{% tab title="CW20 token" %}
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
{% endtab %}
{% endtabs %}

## Migrate

Migrates the vault contract.

```json
{}
```

## ExecuteMsg

### Deposit

Deposits an amount of the vault's asset. The vault issues to the sender an amount of LP tokens proportional to the shares 
of the deposited amount into the vault.

```json
{
  "deposit": {
    "amount": "1000"
  }
}
```

### Flashloan

Performs a flash loan operation, executing the provided message. The `msg` is a message in base64 of the operation to be 
executed with the flash loan.

```json
{
  "flash_loan": {
    "amount": "1000",
    "msg": ""
  }
}
```

### Collect protocol fees

Sends the accrued vault fees to the Fee Collector. This action can be triggered by anyone.

```json
{
  "collect_protocol_fees": {}
}
```

### Callback

This message triggers the `after_trade` function, which makes sure the borrowed funds plus vault fees are returned after 
executing a flash loan. This message can only be called internally by the vault contract.

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

### Update config

Updates the configuration of the vault.

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
