# Factory

The factory contract is used to create pools. Pools are comprised of two tokens, which can be either native, ibc or cw20 tokens. Once a pool is created it's stored in state, meaning the factory acts as a pool registry.

Note that the factory is permissioned, meaning the messages can only be executed by the owner of the contract.

The following are the messages that can be executed on the factory:



## Instantiate

```json
{
  "pair_code_id": 1,
  "token_code_id": 2,
  "fee_collector_addr": "fee_collector_addr"
}
```

## Migrate

```json
{}
```

## ExecuteMsg

### Add Native Token Decimals

```json
{
  "add_native_token_decimals": {
    "denom": "ujuno",
    "decimals": 6
  }
}
```

### Create pair

```json
{
  "create_pair": {
    "asset_infos": [
      {
        "native_token": {
          "denom": "ujuno"
        }
      },
      {
        "token": {
          "contract_addr": "juno1..."
        }
      }
    ],
    "pool_fees": {
      "protocol_fee": {
        "share": "0.001"
      },
      "swap_fee": {
        "share": "0.003"
      }
    }
  }
}
```

### Migrate pair

```json
{
  "migrate_pair": {
    "contract": "pair_address",
    "code_id": 123
  }
}
```

### Remove pair

```json
{
  "remove_pair": {
    "pair_address": "pair_address"
  }
}
```

### Update config

```json
{
  "update_config": {
    "owner": "owner",
    "fee_collector_addr": "fee_collector_addr",
    "token_code_id": 123,
    "pair_code_id": 456
  }
}
```

## Queries

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
  "fee_collector_addr": "juno1...",
  "pair_code_id": 123,
  "token_code_id": 456
}
```
{% endtab %}
{% endtabs %}

### Native token decimals

{% tabs %}
{% tab title="Query" %}
```json
{
  "native_token_decimals": {
    "denom": "ujuno"
  }
}
```
{% endtab %}

{% tab title="Response" %}
```json
{
  "decimals": 6
}
```
{% endtab %}
{% endtabs %}

### Pair

{% tabs %}
{% tab title="Query" %}
```json
{
  "pair": {
    "asset_infos": [
      {
        "native_token": {
          "denom": "ujuno"
        }
      },
      {
        "token": {
          "contract_addr": "juno1..."
        }
      }
    ]
  }
}
```
{% endtab %}

{% tab title="Response" %}
```json
{
  "asset_infos": [
    {
      "native_token": {
        "denom": "ujuno"
      }
    },
    {
      "token": {
        "contract_addr": "juno1..."
      }
    }
  ],
  "contract_addr": "juno1...",
  "liquidity_token": "juno1...",
  "asset_decimals": [
    6,
    6
  ]
}
```
{% endtab %}
{% endtabs %}

### Pairs

{% tabs %}
{% tab title="Query" %}
```json
{
  "pairs": {
    "start_after": [
      {
        "token": {
          "contract_addr": "juno1..."
        }
      },
      {
        "native_token": {
          "denom": "ujuno"
        }
      }
    ],
    "limit": 30
  }
}
```
{% endtab %}

{% tab title="Response" %}
```json
{
  "pairs": [
    {
      "asset_infos": [
        {
          "native_token": {
            "denom": "ujuno"
          }
        },
        {
          "token": {
            "contract_addr": "juno1..."
          }
        }
      ],
      "contract_addr": "juno1...",
      "liquidity_token": "juno1...",
      "asset_decimals": [
        6,
        6
      ]
    },
    {
      "asset_infos": [
        {
          "native_token": {
            "denom": "ujuno"
          }
        },
        {
          "native_token": {
            "denom": "ibc/107D152BB3176FAEBF4C2A84C5FFDEEA7C7CB4FE1BBDAB710F1FD25BCD055CBF"
          }
        }
      ],
      "contract_addr": "juno1...",
      "liquidity_token": "juno1...",
      "asset_decimals": [
        6,
        6
      ]
    }
  ]
}
```
{% endtab %}
{% endtabs %}
