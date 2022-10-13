# Terraswap Token

This is a standard CW20 token. CW20 is a specification for fungible tokens based on CosmWasm. The name and design is 
loosely based on Ethereum's ERC20 standard, but many changes have been made. The types in here can be imported by 
contracts that wish to implement this spec, or by contracts that call to any standard cw20 contract.

The following are the messages that can be executed on the cw20 token contract:

## Instantiate

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

### Burn

```json
{
  "burn": {
    "amount": "1000"
  }
}
```

### Burn from

```json
{
  "burn_from": {
    "owner": "juno1...",
    "amount": "1000"
  }
}
```

### Decrease allowance

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

### Increase allowance

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

### Mint

```json
{
  "mint": {
    "recipient": "juno1...",
    "amount": "1000"
  }
}
```

### Send

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

```json
{
  "transfer": {
    "recipient": "juno1...",
    "amount": "1000"
  }
}
```

### Transfer from

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

```json
{
  "update_minter": {
    "new_minter": "juno1..."
  }
}
```

### Upload logo

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
