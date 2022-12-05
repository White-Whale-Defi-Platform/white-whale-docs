<!-- Documents examples of flashloan usages -->
# Calling Flashloans

The White Whale Flashloan operation is a specific property of each of the [Vaults](/smart-contracts/liquidity-hub/vault-network/vault.md) deployed by White Whale. However, these flashloan messages are only executable by smart-contracts by design. So, to enable users (off-chain clients) to use flashloans without writing smart contracts, White Whale deployed a "Generalized Flashloan Router" [contract](../smart-contracts/liquidity-hub/vault-network/vault-router.md). This contract (also called vault-router) is able to perform all the required flashloan operations without the user to specify each step. 
A very important property of this contract is that it is able to "route" the requested asset by the user to the right vault, thus, we only need **one** flashloan router contract for all vaults deployed on a chain and a user simply has to provide the requested asset.

We will first briefly describe the message that a user needs to send to this flashloan router contract and then show a step-by-step example of how to obtain such a message for a specific use case.

## Flashloan Router
The flashloan router [contract](../smart-contracts/liquidity-hub/vault-network/vault-router.md) requires a specific ExecuteMsg to be executed properly, this Msg is called "Flashloan". The message is described briefly in [this](../smart-contracts/liquidity-hub/vault-network/vault-router.md#flashloan) section, however we will explain it with more details in this section. 

As described in the Vault Router page, the Flashloan message has the following JSON format: 
```json
{
  "assets": [
    {
      "info": {
        "native_token": {
          "denom": "ujuno"
        }
      },
      "amount": "10000"
    }
  ],
  "msgs": [
    {
      "wasm": {
        "execute": {
          "contract_addr": "juno1...",
          "msg": "binary",
          "funds": []
        }
      }
    }
  ]
}
```
However, from a client side, the message we need to send requires one extra layer nested layer with the `flash_loan` label, which leads to:
```json
"flash_loan": {
  "assets": [
    {
      "info": {
        "native_token": {
          "denom": "ujuno"
        }
      },
      "amount": "10000"
    }
  ],
  "msgs": [
    {
      "wasm": {
        "execute": {
          "contract_addr": "juno1...",
          "msg": "binary",
          "funds": []
        }
      }
    }
  ]
}
```
The above message requires only two fields to be provided by the user: 
| Key      | Type            | Description                                    |
|----------|-----------------|------------------------------------------------|
| `assets` | Vec\<Asset>     | A list/array of assets the user wants to borrow      |
| `msgs`    | Vec\<CosmosMsg> | A list/array of subsequent messages the contracts should perform given the borrowed funds |
### `Assets` field
The `assets` field holds a list of `asset` types, which has the following structure, depending on whether the user wants to borrow a `native_token` (or IBC) of the chain or a `token`, which is a CW20 token:

{% tabs %}
{% tab title="Native/IBC token" %}
```json
"asset": {
  "amount": "1000000", 
  "info": {
    "native_token":{
      "denom": "ujuno"
    }
  }
}
```
{% endtab %}
{% tab title="CW20 token"%}
```json
"asset": {
  "amount": "1000000", 
  "info": {
    "token":{
      
      "contract_addr": "juno12x12...." #the contract address of the CW20 token
    }
  }
}
```
{% endtab %}
{% endtabs %}

### `Msgs` field
The Msgs holds all messages that the contract should execute sequentially. Meaning it will first execute the first message, then the second and so on. This gives the opportunity to use the results from the first message in the second message, which is really helpful in arbitrage for example. 
Every entry in `Msgs` should have the following format: 
```json
      "wasm": {
        "execute": {
          "contract_addr": "juno1...",
          "msg": "binary",
          "funds": []
        }
      }
```
In which the user only has to change the lowest level fields: 
| Key      | Type            | Description                                    |
|----------|-----------------|------------------------------------------------|
`contract_addr`|string|The address of the wasm contract on which the contacts has to perform `msg`
`msg`|string|The base64 encoded message the contract needs to execute, see below for more details
`funds`|array|The funds the contract needs to use to execute this message, see below for more details. 

### `msg` field
in the above table is required to be of type string and should represent the base64 encoded message the contract needs to execute. Below an example of a native swap on a AMM-pool: 
```json
{
   "swap":{
      "max_spread":"0.05",
      "offer_asset":{
         "amount":"29830392",
         "info":{
            "native_token":{
               "denom":"uluna"
            }
         }
      },
      "belief_price":"0.649957"
   }
}
```
There's many tools available that are able to encode the above JSON format to base64 (like https://onlineasciitools.com/convert-ascii-to-base64) and it will lead to this base64 string: 
```
ewogICAic3dhcCI6ewogICAgICAibWF4X3NwcmVhZCI6IjAuMDUiLAogICAgICAib2ZmZXJfYXNz
ZXQiOnsKICAgICAgICAgImFtb3VudCI6IjI5ODMwMzkyIiwKICAgICAgICAgImluZm8iOnsKICAg
ICAgICAgICAgIm5hdGl2ZV90b2tlbiI6ewogICAgICAgICAgICAgICAiZGVub20iOiJ1bHVuYSIK
ICAgICAgICAgICAgfQogICAgICAgICB9CiAgICAgIH0sCiAgICAgICJiZWxpZWZfcHJpY2UiOiIw
LjY0OTk1NyIKICAgfQp9
```
This string should be used as the `msg` field. 
### `funds` field
The `funds` field should hold a list of assets that have to be used to perform `msg`, however, these assets are only linked to the `assets` field of the overall `flashloan` message. Meaning if we are going to use the flashloan assets on the first message, only the first message should have this `funds` field filled with the borrowed asset: 
```json
{
  "amount":"29830392",
  "denom":"uluna"
}
```
As said it is possible to use the result of the first message in the second message and so on. This allowed for chained swaps to be executed sequentially with the previous message's result as input. 
see [example](/client-docs/flashloan_example.md) for a full example.