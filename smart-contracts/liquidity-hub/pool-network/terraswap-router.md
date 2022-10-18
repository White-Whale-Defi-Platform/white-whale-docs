# Terraswap Router

The router contract is used to execute multi-hop swaps. Say there are two pools: ATOM-JUNO and JUNO-LUNA. There is no way 
to directly swap ATOM for LUNA, as there is no ATOM-LUNA pool. With the router contract, it is possible to can concatenate 
swap operations so that it becomes possible to swap ATOM for LUNA via JUNO, i.e. ATOM->JUNO->LUNA.

The router is mainly used by bots and the UI.

The code for the router contract can be found [here](https://github.com/White-Whale-Defi-Platform/migaloo-core/tree/main/contracts/liquidity_hub/pool-network/terraswap_router).

---

The following are the messages that can be executed on the router:

## Instantiate

Instantiates the router. Requires to have instantiated the factory first. 

```json
{
  "terraswap_factory": "juno1..."
}
```

## Migrate

Migrates the router.

```json
{}
```

## ExecuteMsg

### Asset minimum receive

Checks whether the ask amount is equal to or above a minimum amount.

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

Executes swap operations. It can be a multi-hop swap as the example described above, but it doesn't need to be.

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

### Swap Operation

Executes a swap operation. This is called internally by the contract itself.

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

Receives a `Cw20ReceiveMsg` message, being the only valid message `ExecuteSwapOperations`, used to execute swap operations 
when the token to be swapped is a cw20 token.

```json
{
  "send": {
    "contract": "router_contract_address",
    "amount": "1000",
    "msg": "ewogI...7fQp9"
  }
}
```

where `ewogI...7fQp9` is the `ExecuteSwapOperations` message, encoded in base64.

## Queries

### Config

Retrieves the configuration of the router contract.

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

### Simulate swap operations

Performs a simulation for swap operations.

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
    "offer_amount":"1000"
  }
}
```
{% endtab %}

{% tab title="Response" %}
```json
{
  "amount": "5000"
}
```
{% endtab %}
{% endtabs %}


### Reverse simulate swap operations

Performs a reverse simulation for swap operations, i.e. given the ask asset, how much of the offer asset is needed to perform
the swap.

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
    "ask_amount": "1000"
  }
}
```
{% endtab %}

{% tab title="Response" %}
```json
{
  "amount": "5000"
}
```
{% endtab %}
{% endtabs %}
