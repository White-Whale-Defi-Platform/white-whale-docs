# Terraswap Token

This is a standard CW20 token. CW20 is a specification for fungible tokens based on CosmWasm. The name and design is 
loosely based on Ethereum's ERC20 standard, but many changes have been made. The types in here can be imported by 
contracts that wish to implement this spec, or by contracts that call to any standard cw20 contract.

The token contract is used by the pool contract to create LP tokens.

The code for the token contract can be found [here](https://github.com/White-Whale-Defi-Platform/white-whale-core/tree/main/contracts/liquidity_hub/pool-network/terraswap_token).

---

The following are the messages that can be executed on the cw20 token contract:

## Instantiate

Instantiates a cw20 token.

```json
{
  "name": "WHALE",
  "symbol": "WHALE",
  "decimals": 6,
  "initial_balances": [
    {
      "address": "juno1...",
      "amount": "10"
    }
  ],
  "mint": {
    "minter": "juno1...",
    "cap": "1000"
  }
}
```

## ExecuteMsg

### Increase allowance

Only with "approval" extension. Allows spender to access an additional amount tokens from the owner's (env.sender) account. 
If expires is Some(), overwrites current allowance expiration with this one.

```json
{
  "increase_allowance": {
    "spender": "juno1...",
    "amount": "1000",
    "expires": {
      "at_height": 9999,
      "at_time": 9999,
      "never": {}
    }
  }
}
```

### Decrease allowance

Only with "approval" extension. Lowers the spender's access of tokens from the owner's (env.sender) account by amount.
If expires is Some(), overwrites current allowance expiration with this one.

```json
{
  "decrease_allowance": {
    "spender": "juno1...",
    "amount": "1000",
    "expires": {
      "at_height": 9999,
      "at_time": 9999,
      "never": {}
    }
  }
}
```

### Burn

Burn is a base message to destroy tokens forever. 

```json
{
  "burn": {
    "amount": "1000"
  }
}
```

### Burn from

Only with "approval" extension. Destroys tokens forever

```json
{
  "burn_from": {
    "owner": "juno1...",
    "amount": "1000"
  }
}
```

### Mint

Only with the "mintable" extension. If authorized, creates amount new tokens and adds to the recipient balance.

```json
{
  "mint": {
    "recipient": "juno1...",
    "amount": "1000"
  }
}
```

### Send

Send is a base message to transfer tokens to a contract and trigger an action on the receiving contract.

```json
{
  "send": {
    "contract": "juno1...",
    "amount": "1000",
    "msg": ""
  }
}
```

### Send from

Only with "approval" extension. Sends amount tokens from owner -> contract if env.sender has sufficient pre-approval.

```json
{
  "send_from": {
    "owner": "juno1...",
    "contract": "juno1...",
    "amount": "1000",
    "msg": ""
  }
}
```

### Transfer

Transfer is a base message to move tokens to another account without triggering actions.

```json
{
  "transfer": {
    "recipient": "juno1...",
    "amount": "1000"
  }
}
```

### Transfer from

Only with "approval" extension. Transfers amount tokens from owner -> recipient if env.sender has sufficient pre-approval.

```json
{
  "transfer_from": {
    "owner": "juno1...",
    "recipient": "juno1...",
    "amount": "1000"
  }
}
```

### Update marketing

Only with the "marketing" extension. If authorized, updates marketing metadata. Setting None/null for any of these will 
leave it unchanged. Setting Some("") will clear this field on the contract storage

```json
{
  "update_marketing": {
    "project": "https://whitewhale.money",
    "description": "Interchain Arbitrage Infrastructure",
    "marketing": ""
  }
}
```

### Update minter

Only with the "mintable" extension. The current minter may set a new minter. Setting the minter to None will remove the 
token's minter forever.

```json
{
  "update_minter": {
    "new_minter": "juno1..."
  }
}
```

### Upload logo

If set as the "marketing" role on the contract, upload a new URL, SVG, or PNG for the token.

```json
{
  "upload_logo": {
    "url": "https://whitewhale.money",
    "embedded": {
      "svg": "",
      "png": ""
    }
  }
}
```

## Queries

### All accounts

Only with "enumerable" extension. Returns all accounts that have balances. Supports pagination.

{% tabs %}
{% tab title="Query" %}
```json
{
  "all_accounts": {
    "start_after": "juno1...",
    "limit": 10
  }
}
```
{% endtab %}

{% tab title="Response" %}
```json
{
  "accounts": [
    "juno1...",
    "juno1...",
    "juno1..."
  ]
}
```
{% endtab %}
{% endtabs %}

### All allowances

Only with "enumerable" extension (and "allowances"). Returns all allowances this owner has approved. Supports pagination.

{% tabs %}
{% tab title="Query" %}
```json
{
  "all_allowances": {
    "owner": "juno1...",
    "start_after": "juno1...",
    "limit": 10
  }
}
```
{% endtab %}

{% tab title="Response" %}
```json
{
  "allowances": []
}
```
{% endtab %}
{% endtabs %}

### All spender allowances

Only with "enumerable" extension (and "allowances"). Returns all allowances this spender has been granted. Supports pagination.

{% tabs %}
{% tab title="Query" %}
```json
{
  "all_spender_allowances": {
    "spender": "juno1...",
    "start_after": "juno1...",
    "limit": 10
  }
}
```
{% endtab %}

{% tab title="Response" %}
```json
{
  "allowance": "0",
  "expires": {
    "never": {}
  }
}
```
{% endtab %}
{% endtabs %}

### Allowance

Only with "allowance" extension. Returns how much spender can use from owner account, 0 if unset.

{% tabs %}
{% tab title="Query" %}
```json
{
  "allowance": {
    "owner": "juno1...",
    "spender": "juno1..."
  }
}
```
{% endtab %}

{% tab title="Response" %}
```json
{
  "allowance": "0",
  "expires": {
    "never": {}
  }
}
```
{% endtab %}
{% endtabs %}

### Balance

Returns the current balance of the given address, 0 if unset.

{% tabs %}
{% tab title="Query" %}
```json
{
  "balance": {
    "address": "juno1..."
  }
}
```
{% endtab %}

{% tab title="Response" %}
```json
{
  "balance": "1000000"
}
```
{% endtab %}
{% endtabs %}

### Download logo

Only with "marketing" extension. Downloads the embedded logo data (if stored on chain). Errors if no logo data is stored 
for this contract.

{% tabs %}
{% tab title="Query" %}
```json
{
  "download_logo": {}
}
```
{% endtab %}

{% tab title="Response" %}
```json
```
{% endtab %}
{% endtabs %}

### Marketing info

Only with "marketing" extension. Returns more metadata on the contract to display in the client:
description, logo, project url, etc.

{% tabs %}
{% tab title="Query" %}
```json
{
  "marketing_info": {}
}
```
{% endtab %}

{% tab title="Response" %}
```json
{
  "project": "",
  "description": "",
  "logo": "",
  "marketing": ""
}
```
{% endtab %}
{% endtabs %}

### Minter

Only with "mintable" extension. Returns who can mint and the hard cap on maximum tokens after minting.

{% tabs %}
{% tab title="Query" %}
```json
{
  "minter": {}
}
```
{% endtab %}

{% tab title="Response" %}
```json
{
  "minter": "juno1...",
  "cap": "1000000000"
}
```
{% endtab %}
{% endtabs %}

### Token info

Returns metadata on the contract - name, decimals, supply, etc.

{% tabs %}
{% tab title="Query" %}
```json
{
  "token_info": {}
}
```
{% endtab %}

{% tab title="Response" %}
```json
{
  "name": "WHALE",
  "symbol": "WHALE",
  "decimals": 6,
  "total_supply": "1000000000000"
}
```
{% endtab %}
{% endtabs %}
