# Vault

The vault contract is a single-asset pool, used by bots to take flash-loans. Depositors of tokens into flash loan vaults 
benefit from fees paid when their vault is accessed for flash loans; the greater the volume, the more fees generated. 
Flash loan vaults are a great source of yield with no impermanent loss.

## Fees

There are three types of fees associated to the vaults, namely `flash_loan_fee`, `protocol_fee` and `burn_fee`. The `flash_loan_fee` 
remains in the vault, which makes the share's value of the liquidity provides to increase, benefiting all LPs.

The `protocol_fee` goes to the protocol, and it is to be collected by the Fee Collector contract of the Liquidity Hub.
The protocol revenue is then distributed to WHALE stakers in the form of token buybacks.

The `burn_fee` is used to burn a portion of the tokens when a flash-loan takes place.

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
    },
    "burn_fee": {
      "share": "0.01"
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
    },
    "burn_fee": {
      "share": "0.01"
    }
  },
  "fee_collector_addr": "juno1..."
}
```
{% endtab %}
{% endtabs %}

| Key                  | Type      | Description                                       |
| -------------------- | --------- | ------------------------------------------------- |
| `owner`              | String    | Contract owner address                            |
| `asset_info`         | AssetInfo | The asset info the vault shoudl manage            |
| `token_id`           | u64       | The code ID of the liquidity token to instantiate |
| `vault_fees`         | VaultFee  | The fees used for the vault                       |
| `fee_collector_addr` | String    | The address of the fee collector contract         |

## Migrate

Migrates the vault contract.

```json
{}
```

## ExecuteMsg

### Deposit

Deposits an amount of the vault's asset. The vault issues to the sender an amount of LP tokens proportional to the shares 
of the deposited amount into the vault. Note that in case of depositing a cw20 token, the message 
[increase\_allowance](terraswap-token.md#increase-allowance) should be called on the cw20 token contract before you can 
transfer cw20 tokens to the vault.

```json
{
  "deposit": {
    "amount": "1000"
  }
}
```

| Key      | Type    | Description                         |
| -------- | ------- | ----------------------------------- |
| `amount` | Uint128 | Amount to be deposited in the vault |

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


| Key                  | Type    | Description                                                   |
|----------------------|---------|---------------------------------------------------------------|
| `amount`             | Uint128 | Amount for the flash loan                                     |
| `msg`                | Binary  | Message to be executed with the flash loan, encoded in base64 |


### Collect protocol fees

Sends the accrued vault fees to the Fee Collector. This action can be triggered by anyone.

```json
{
  "collect_protocol_fees": {}
}
```

### Callback

This message triggers a `CallbackMsg` message, e.g. `AfterTrade` which makes sure the borrowed funds plus vault fees are 
returned after executing a flash loan. This message can only be called internally by the vault contract.

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

| Key           | Type                    | Description                                                                  |
| ------------- | ----------------------- | ---------------------------------------------------------------------------- |
| `after_trade` | CallbackMsg::AfterTrade | Callback parameters verified balances by the end of the flash loan execution |

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
      },
      "burn_fee": {
        "share": "0.01"
      }
    },
    "new_fee_collector_addr": "inj1..."
  }
}
```

| Key                      | Type              | Description                             |
| ------------------------ | ----------------- | --------------------------------------- |
| `flash_loan_enabled`     | Option\<bool>     | Toggle for the flash loan functionality |
| `deposit_enabled`        | Option\<bool>     | Toggle for the deposit functionality    |
| `withdraw_enabled`       | Option\<bool>     | Toggle for the withdraw functionality   |
| `new_owner`              | Option\<String>   | New owner address                       |
| `new_vault_fees`         | Option\<VaultFee> | New vault fees                          |
| `new_fee_collector_addr` | Option\<String>   | New fee collector address               |


### Withdraw

To withdraw from the vault, the user must burn the LP tokens they hold. To do that, the `Send` message from the cw20 
token contract should be used together with the `Cw20HookMsg::Withdraw` message. 

The following should be sent to the LP (CW20 token) contract.

```json
{
  "send": {
    "contract": "vault_contract",
    "amount": "1000",
    "msg": "ewogICJ3aXRoZHJhdyI6IHt9Cn0="
  }
}
```

where `ewogICJ3aXRoZHJhdyI6IHt9Cn0=` is the base64 encoded message:

```json
{
  "withdraw": {}
}
```

| Key        | Type   | Description                         |
| ---------- | ------ | ----------------------------------- |
| `contract` | String | Vault contract address              |
| `amount`   | String | Amount of LP tokens to be withdrawn |
| `msg`      | Binary | The `Cw20HookMsg::Withdraw` message |

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
    },
    "burn_fee": {
      "share": "0.001"
    }
  }
}
```

| Key                  | Type      | Description                         |
| -------------------- | --------- | ----------------------------------- |
| `owner`              | Addr      | The owner of the vault              |
| `asset_info`         | AssetInfo | The asset info the vault manages    |
| `flash_loan_enabled` | bool      | If flash-loans are enabled          |
| `deposit_enabled`    | bool      | If deposits are enabled             |
| `withdraw_enabled`   | bool      | If withdrawals are enabled          |
| `liquidity_token`    | Addr      | The address of the liquidity token  |
| `fee_collector_addr` | Addr      | The address of the fee collector    |
| `fees`               | VaultFee  | The fees associated with this vault |


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

| Key      | Type    | Description                                                               |
| -------- | ------- | ------------------------------------------------------------------------- |
| `amount` | Uint128 | Amount that must be sent back to the contract to pay off a loan taken out |

{% endtab %}

{% tab title="Response (PaybackAmountResponse)" %}
```json
{
  "payback_amount": "10030",
  "protocol_fee": "10",
  "flash_loan_fee": "20",
  "burn_fee": "20"
}
```

| Key              | Type    | Description                                                                                        |
| ---------------- | ------- | -------------------------------------------------------------------------------------------------- |
| `payback_amount` | Uint128 | The total amount that must be returned. Equivalent to `amount` + `protocol_fee` + `flash_loan_fee` |
| `protocol_fee`   | Uint128 | The amount of fee paid to the protocol                                                             |
| `flash_loan_fee` | Uint128 | The amount of fee paid to vault holders                                                            |
| `burn_fee`       | Uint128 | Fees that would be burned, if any, by executing a flashloan                                        |

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

| Key        | Type | Description                                        |
| ---------- | ---- | -------------------------------------------------- |
| `all_time` | bool | If `true`, will return the all time collected fees |


{% endtab %}

{% tab title="Response (ProtocolFeesResponse)" %}
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

| Key    | Type  | Description                      |
| ------ | ----- | -------------------------------- |
| `fees` | Asset | Fees collected accrued the vault |


{% endtab %}
{% endtabs %}

### Burned fees

Retrieves the fees that have been burned by vault.

{% tabs %}
{% tab title="Query" %}
```json
{
  "burned_fees": {}
}
```

{% endtab %}

{% tab title="Response (ProtocolFeesResponse)" %}
```json
{
  "fees": {
    "info": {
      "native_token": {
        "denom": "uhuahua"
      }
    },
    "amount": "47516"
  }
}
```

| Key    | Type  | Description              |
| ------ | ----- |--------------------------|
| `fees` | Asset | Fees burned by the vault |


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

| Key      | Type    | Description                                                                  |
|----------|---------|------------------------------------------------------------------------------|
| `amount` | Uint128 | Amount of LP tokens to calculate the share of the assets stored in the vault |


{% endtab %}

{% tab title="Response (Uint128)" %}
```json
{
  "data": "10002558"
}
```

| Key    | Type    | Description                                                                                 |
|--------|---------|---------------------------------------------------------------------------------------------|
| `data` | Uint128 | The share of assets sotred in the vault that the given `amount` of LP tokens is entitled to |

{% endtab %}
{% endtabs %}
