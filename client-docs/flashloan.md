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
### Assets field
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

### Msgs field
can hold assets of two types: a `native_token`, which are the chain's nativily known tokens/assets, or the `token` type, which are tokens/assets described by a CW20 smart contract deployment. Since these are not native to a chain, they need to be specified differently. 
Each asset in the list of `assets` has to follow either one of the following formats, depending on whethere it is a native token or a CW20 token:
