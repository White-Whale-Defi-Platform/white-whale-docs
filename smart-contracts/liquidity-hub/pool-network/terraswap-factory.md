# Factory

Migaloo's factory contract is used to create pair (pool) contracts. Pools are comprised of two tokens, which can be either 
native, ibc or cw20 tokens. Once a pool is created it's stored in state, meaning the factory acts as a pool registry, which 
can be queried for reference. Note that **the factory is permissioned**, meaning the messages can only be executed by the 
owner of the contract.

## Create a pair

Creating a pair (pool) can be done via the `create_pair` message. Note that for creating pools with native or ibc tokens,
`add_native_token_decimals` should be called in advance with a small amount of the desired asset (say one micro unit). This 
is used to whitelist native/ibc tokens, allowing pools to be created with those.

The code for the Factory contract can be found [here](https://github.com/White-Whale-Defi-Platform/migaloo-core/tree/main/contracts/liquidity_hub/pool-network/terraswap_factory).

---

The following are the messages that can be executed on the factory:

## Instantiate

Instantiates the pool factory.

```json
{
  "pair_code_id": 1,
  "token_code_id": 2,
  "fee_collector_addr": "fee_collector_addr"
}
```

## Migrate

Migratest the pool factory.

```json
{}
```

## ExecuteMsg

### Add Native Token Decimals

Used to validate native or ibc tokens, adding them to a whitelist so pools can be created with them. Along with this 
message, a small amount of the token should be transferred.

```json
{
  "add_native_token_decimals": {
    "denom": "ujuno",
    "decimals": 6
  }
}
```

### Create pair

Creates a pool with the given assets and pool fees. If the pool already exists, the transaction will fail.

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

Migrates a pool with the given address to the desired code id.

```json
{
  "migrate_pair": {
    "contract": "pair_address",
    "code_id": 123
  }
}
```

### Remove pair

Removes a pair for the pool registry. Note that the pool will still live on the blockchain, this action though will make it
invisible to the factory, meaning it will be orphan by the protocol. This action could be used  in case a pool is no longer 
desired, e.g. if a pool was set up incorrectly (and can't be fixed by updating the config). Ideally, this should only be done 
after the pool's liquidity has been withdrawn or migrated.

```json
{
  "remove_pair": {
    "pair_address": "pair_address"
  }
}
```

### Update config

Updates the configuration of the factory.

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

Retrieves the configuration of the factory.

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

Retrieves the native token decimals for the given `denom`.

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

Retrieves pool information for a given pair.

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

Retrieves multiple pool informations. Considering the pool registry can get extensive, pagination is possible. The default 
limit for the query is `10`, while the maximum is `30`.

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
