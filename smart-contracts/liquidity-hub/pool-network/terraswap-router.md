# Terraswap Router

The router contract is used to find the swap route for two tokens. Say there are two pools: A-B and B-C. There is no way 
to directly swap A for C, as there is no pool A-C. With the router contract, you can concatenate swap operations so that 
if you want to swap A for C, what you effectively do is A->B->C.

The router is mainly used by bots and the UI.

The following are the messages that can be executed on the router:

## Instantiate

```json
{
  "terraswap_factory": "juno1..."
}
```

## Migrate

```json
{}
```

## ExecuteMsg

### Asset minimum receive

```json
{
  "assert_minimum_receive": {
    "asset_info": {
      "native_token": {
        "denom": "ibc/C4CFF46FD6DE35CA4CF4CE031E643C8FDC9BA4B99AE598E9B0ED98FE3A2319F9"
      }
    },
    "prev_balance": "1000",
    "minimum_receive": "1000",
    "receiver": ""
  }
}
```

### Swap Operations

```json
{
  "execute_swap_operations": {
    "operations": [
      {
        "terra_swap": {
          "offer_asset_info": {
            "native_token": {
              "denom": "ibc/C4CFF46FD6DE35CA4CF4CE031E643C8FDC9BA4B99AE598E9B0ED98FE3A2319F9"
            }
          },
          "ask_asset_info": {
            "native_token": {
              "denom": "ujuno"
            }
          }
        }
      },
      {
        "terra_swap": {
          "offer_asset_info": {
            "native_token": {
              "denom": "ujuno"
            }
          },
          "ask_asset_info": {
            "token": {
              "contract_addr": "juno1..."
            }
          }
        }
      }
    ],
    "minimum_receive": "1000",
    "to": ""
  }
}
```

### Swap Operation (called internally by the contract itself)

```json
{
  "execute_swap_operation": {
    "operation": {
      "terra_swap": {
        "offer_asset_info": {
          "native_token": {
            "denom": "ibc/C4CFF46FD6DE35CA4CF4CE031E643C8FDC9BA4B99AE598E9B0ED98FE3A2319F9"
          }
        },
        "ask_asset_info": {
          "native_token": {
            "denom": "ujuno"
          }
        }
      }
    },
    "to": ""
  }
}
```

### Receive (Cw20ReceiveMsg)

```json
{
  "sender": "",
  "amount": "",
  "msg": ""
}
```

### Swap operations (cw20)

```json
{
  "execute_swap_operations": {
    "operations": [
      {
        "terra_swap": {
          "offer_asset_info": {
            "native_token": {
              "denom": "ibc/C4CFF46FD6DE35CA4CF4CE031E643C8FDC9BA4B99AE598E9B0ED98FE3A2319F9"
            }
          },
          "ask_asset_info": {
            "native_token": {
              "denom": "ujuno"
            }
          }
        }
      },
      {
        "terra_swap": {
          "offer_asset_info": {
            "native_token": {
              "denom": "ujuno"
            }
          },
          "ask_asset_info": {
            "token": {
              "contract_addr": "juno1..."
            }
          }
        }
      }
    ],
    "minimum_receive": "1000",
    "to": ""
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
  "terraswap_factory": "juno1..."
}
```
{% endtab %}
{% endtabs %}

### Reverse simulate swap operations

{% tabs %}
{% tab title="Query" %}
```json
{
  "reverse_simulate_swap_operations": {
    "operations": [
      {
        "terra_swap": {
          "offer_asset_info": {
            "native_token": {
              "denom": "ibc/C4CFF46FD6DE35CA4CF4CE031E643C8FDC9BA4B99AE598E9B0ED98FE3A2319F9"
            }
          },
          "ask_asset_info": {
            "native_token": {
              "denom": "ujuno"
            }
          }
        }
      },
      {
        "terra_swap": {
          "offer_asset_info": {
            "native_token": {
              "denom": "ujuno"
            }
          },
          "ask_asset_info": {
            "token": {
              "contract_addr": "juno1"
            }
          }
        }
      }
    ],
    "ask_amount": "100"
  }
}
```
{% endtab %}

{% tab title="Response" %}
```json
{
  "amount": "0"
}
```
{% endtab %}
{% endtabs %}

### Simulate swap operations

{% tabs %}
{% tab title="Query" %}
```json
{
  "simulate_swap_operations":{
    "operations":[
      {
        "terra_swap":{
          "offer_asset_info":{
            "native_token":{
              "denom":"uluna"
            }
          },
          "ask_asset_info":{
            "native_token":{
              "denom":"ibc/27394FB092D2ECCD56123C74F36E4C1F926001CEADA9CA97EA622B25F41E5EB2"
            }
          }
        }
      },
      {
        "terra_swap":{
          "offer_asset_info":{
            "native_token":{
              "denom":"ibc/27394FB092D2ECCD56123C74F36E4C1F926001CEADA9CA97EA622B25F41E5EB2"
            }
          },
          "ask_asset_info":{
            "native_token":{
              "denom":"ibc/4CD525F166D32B0132C095F353F4C6F033B0FF5C49141470D1EFDA1D63303D04"
            }
          }
        }
      }
    ],
    "offer_amount":"100"
  }
}
```
{% endtab %}

{% tab title="Response" %}
```json
{
  "amount": "0"
}
```
{% endtab %}
{% endtabs %}
