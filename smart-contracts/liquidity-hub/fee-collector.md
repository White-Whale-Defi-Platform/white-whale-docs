# Fee Collector

The local fee collector collects the fees for usage of the pool and vault network on a specific blockchain. Part of the 
collected fees goes back to the depositors of the White Whale pools and/or the single asset flash loan vaults. The 
remainder is sent to the interchain collector as protocol revenue. The protocol revenue is then distributed to WHALE stakers 
in the form of token buybacks.

The following are the messages that can be executed on the fee collector:


## Instantiate 

```json
{}
```

## Migrate 

```json
{}
```

## ExecuteMsg

### Add factory

```json
{
  "add_factory": {
    "factory_addr": "inj1..."
  }
}
```

### Collect fees


{% tabs %}
{% tab title="Contract fees" %}
```json
{
  "collect_fees": {
    "collect_fees_for": {
      "contracts": {
        "contracts": [
          "terra1...",
          "terra1..."
        ]
      }
    }
  }
}
```
{% endtab %}

{% tab title="Pool fees" %}
```json
{
  "collect_fees":{
    "collect_fees_for":{
      "factory":{
        "factory_addr":"terra1...",
        "factory_type":{
          "pool":{}
        }
      }
    }
  }
}
```
{% endtab %}

{% tab title="Vault fees" %}
```json
{
  "collect_fees":{
    "collect_fees_for":{
      "factory":{
        "factory_addr":"terra1...",
        "factory_type":{
          "vault":{}
        }
      }
    }
  }
}
```
{% endtab %}
{% endtabs %}


### Remove factory

```json
{
  "remove_factory": {
    "factory_addr": "terra1..."
  }
}
```

### Update config

```json
{
  "update_config": {
    "owner": "terra1..."
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
  "owner": "terra1..."
}
```
{% endtab %}
{% endtabs %}

### Factories

Queries factories added to the fee collector.

{% tabs %}
{% tab title="Query" %}
```json
{
  "factories": {
    "limit": 10
  }
}
```
{% endtab %}

{% tab title="Response" %}
```json
{
  "factories": [
    "terra1...",
    "terra1..."
  ]
}
```
{% endtab %}
{% endtabs %}

### Fees (contracts)

Queries the fees collected by individual contracts, whether they are pools or vaults.

{% tabs %}
{% tab title="Query" %}
```json
{
  "fees": {
    "query_fees_for": {
      "contracts": {
        "contracts": [
          {
            "address": "terra1...",
            "contract_type": {
              "pool": {}
            }
          },
          {
            "address": "terra1...",
            "contract_type": {
              "vault": {}
            }
          }
        ]
      }
    },
    "all_time": true
  }
}
```
{% endtab %}

{% tab title="Response" %}
```json
[
  {
    "info": {
      "native_token": {
        "denom": "uluna"
      }
    },
    "amount": "0"
  },
  {
    "info": {
      "token": {
        "contract_addr": "terra1..."
      }
    },
    "amount": "196116"
  },
  {
    "info": {
      "native_token": {
        "denom": "ujuno"
      }
    },
    "amount": "0"
  }
]
```
{% endtab %}
{% endtabs %}

### Fees (pool)

Queries the fees collected by a given pool factory's children.

{% tabs %}
{% tab title="Query" %}
```json
{
  "fees": {
    "query_fees_for": {
      "factory": {
        "factory_addr": "terra1...",
        "factory_type": {
          "pool": {}
        }
      }
    },
    "all_time": false
  }
}
```
{% endtab %}

{% tab title="Response" %}
```json
[
  {
    "info": {
      "native_token": {
        "denom": "uluna"
      }
    },
    "amount": "0"
  },
  {
    "info": {
      "token": {
        "contract_addr": "terra1..."
      }
    },
    "amount": "10936515"
  }
]
```
{% endtab %}
{% endtabs %}

### Fees (vault)

Queries the fees collected by a given vault factory's children.

{% tabs %}
{% tab title="Query" %}
```json
{
  "fees": {
    "query_fees_for": {
      "factory": {
        "factory_addr": "terra1...",
        "factory_type": {
          "vault": {}
        }
      }
    },
    "all_time": false
  }
}
```
{% endtab %}

{% tab title="Response" %}
```json
[
  {
    "info": {
      "token": {
        "contract_addr": "terra1..."
      }
    },
    "amount": "1000000"
  },
  {
    "info": {
      "native_token": {
        "denom": "ujuno"
      }
    },
    "amount": "1000000"
  },
  {
    "info": {
      "native_token": {
        "denom": "uluna"
      }
    },
    "amount": "1000000"
  }
]
```
{% endtab %}
{% endtabs %}
