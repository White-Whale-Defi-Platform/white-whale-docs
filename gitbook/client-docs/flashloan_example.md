# Flashloan example on Terra
This example will show an actual example of an arbitrage message using the White Whale Flashloans. Obviously this example was succesfully executed in the past and therefore won't work anymore and is only used as a reference. 
The whole message looks like this: 
```json

{
  "flash_loan": {
    "msgs": [
      {
        "wasm": {
          "execute": {
            "msg": "eyJzd2FwIjp7Im1heF9zcHJlYWQiOiIwLjA1Iiwib2ZmZXJfYXNzZXQiOnsiYW1vdW50IjoiMjk4MzAzOTIiLCJpbmZvIjp7Im5hdGl2ZV90b2tlbiI6eyJkZW5vbSI6InVsdW5hIn19fSwiYmVsaWVmX3ByaWNlIjoiMC42NDk5NTcifX0=",
            "funds": [
              {
                "denom": "uluna",
                "amount": "29830392"
              }
            ],
            "contract_addr": "terra1fd68ah02gr2y8ze7tm9te7m70zlmc7vjyyhs6xlhsdmqqcjud4dql4wpxr"
          }
        }
      },
      {
        "wasm": {
          "execute": {
            "msg": "eyJzd2FwIjp7Im1heF9zcHJlYWQiOiIwLjA1Iiwib2ZmZXJfYXNzZXQiOnsiYW1vdW50IjoiNDU4OTU5NjciLCJpbmZvIjp7Im5hdGl2ZV90b2tlbiI6eyJkZW5vbSI6ImliYy9CMzUwNEUwOTI0NTZCQTYxOENDMjhBQzY3MUE3MUZCMDhDNkNBMEZEMEJFN0M4QTVCNUEzRTJERDkzM0NDOUU0In19fSwiYmVsaWVmX3ByaWNlIjoiMC4wNjUzMTYifX0=",
            "funds": [
              {
                "denom": "ibc/B3504E092456BA618CC28AC671A71FB08C6CA0FD0BE7C8A5B5A3E2DD933CC9E4",
                "amount": "45895967"
              }
            ],
            "contract_addr": "terra1w579ysjvpx7xxhckxewk8sykxz70gm48wpcuruenl29rhe6p6raslhj0m6"
          }
        }
      },
      {
        "wasm": {
          "execute": {
            "msg": "eyJzZW5kIjp7ImFtb3VudCI6IjcwMjY3MDc3NyIsImNvbnRyYWN0IjoidGVycmExZTZ0MzdmZ2preHJ6ZHgyczk1ZnlxNmpkcmE1czgyNzIwdmh0bXh2eDR5aGN2bnNyZXk0c3NtcnlhNiIsIm1zZyI6ImV5SnpkMkZ3SWpwN0ltSmxiR2xsWmw5d2NtbGpaU0k2SWpJekxqSTJOall5T0NJc0ltMWhlRjl6Y0hKbFlXUWlPaUl3TGpBd01EVWlmWDA9In19",
            "funds": [],
            "contract_addr": "terra1nsuqsk6kh58ulczatwev87ttq2z6r3pusulg9r24mfj2fvtzd4uq3exn26"
          }
        }
      }
    ],
    "assets": [
      {
        "info": {
          "native_token": {
            "denom": "uluna"
          }
        },
        "amount": "29830392"
      }
    ]
  }
}
```
As described in [Calling Flashloans](/client-docs//flashloan.md), the `asset` field holds a list of assets we want to borrow from one of the White Whale vaults. In this example, we wanted to borrow 29830392uluna, which is ~29.8 luna. 
After getting the flashloan from the luna vault in this case, the contract executes the messages in the `msgs` field sequentially. 

## First message
```json
{
        "wasm": {
          "execute": {
            "msg": "eyJzd2FwIjp7Im1heF9zcHJlYWQiOiIwLjA1Iiwib2ZmZXJfYXNzZXQiOnsiYW1vdW50IjoiMjk4MzAzOTIiLCJpbmZvIjp7Im5hdGl2ZV90b2tlbiI6eyJkZW5vbSI6InVsdW5hIn19fSwiYmVsaWVmX3ByaWNlIjoiMC42NDk5NTcifX0=",
            "funds": [
              {
                "denom": "uluna",
                "amount": "29830392"
              }
            ],
            "contract_addr": "terra1fd68ah02gr2y8ze7tm9te7m70zlmc7vjyyhs6xlhsdmqqcjud4dql4wpxr"
          }
        }
      },
```
Which, as we can see, uses the borrowed assets from the `assets` field in the `funds` field. This is an important detail of designing the message. Next, the `contract_addr` field is filled with the AMM pool address of the pool we wanted to swap this luna on, namely `terra1fd68ah02gr2y8ze7tm9te7m70zlmc7vjyyhs6xlhsdmqqcjud4dql4wpxr`, which is an AMM pool that holds luna and axlUSDC. Lastly, the `msg` field is filled with the base64 encoded message to be executed, if we decode it (using https://base64.guru/converter/decode/ascii for example) we can see it says: 
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
## Second message
```json
{
        "wasm": {
          "execute": {
            "msg": "eyJzd2FwIjp7Im1heF9zcHJlYWQiOiIwLjA1Iiwib2ZmZXJfYXNzZXQiOnsiYW1vdW50IjoiNDU4OTU5NjciLCJpbmZvIjp7Im5hdGl2ZV90b2tlbiI6eyJkZW5vbSI6ImliYy9CMzUwNEUwOTI0NTZCQTYxOENDMjhBQzY3MUE3MUZCMDhDNkNBMEZEMEJFN0M4QTVCNUEzRTJERDkzM0NDOUU0In19fSwiYmVsaWVmX3ByaWNlIjoiMC4wNjUzMTYifX0=",
            "funds": [
              {
                "denom": "ibc/B3504E092456BA618CC28AC671A71FB08C6CA0FD0BE7C8A5B5A3E2DD933CC9E4",
                "amount": "45895967"
              }
            ],
            "contract_addr": "terra1w579ysjvpx7xxhckxewk8sykxz70gm48wpcuruenl29rhe6p6raslhj0m6"
          }
        }
      }
```
This second message is send to the `contract_addr` `"terra1w579ysjvpx7xxhckxewk8sykxz70gm48wpcuruenl29rhe6p6raslhj0m6"` which is an AMM pool that holds axlUSDC and ASTRO (Astroport's protocol token). Since axlUSDC is an IBC-token and therefore treated as a `native_token`, the overall message looks a whole lot like the first message of the `msgs` field, it just has different entries for the required fields. Please note that the amount of uaxlUSDC used in this second swap (45895967) is **precalculated**, we have to enter this value ourselves and the contract does not derive it for us. 

## Third message
The third and last message from this specific example holds another swap on an AMM pool, namely the ASTRO-Luna pool. 
```json
{
        "wasm": {
          "execute": {
            "msg": "eyJzZW5kIjp7ImFtb3VudCI6IjcwMjY3MDc3NyIsImNvbnRyYWN0IjoidGVycmExZTZ0MzdmZ2preHJ6ZHgyczk1ZnlxNmpkcmE1czgyNzIwdmh0bXh2eDR5aGN2bnNyZXk0c3NtcnlhNiIsIm1zZyI6ImV5SnpkMkZ3SWpwN0ltSmxiR2xsWmw5d2NtbGpaU0k2SWpJekxqSTJOall5T0NJc0ltMWhlRjl6Y0hKbFlXUWlPaUl3TGpBd01EVWlmWDA9In19",
            "funds": [],
            "contract_addr": "terra1nsuqsk6kh58ulczatwev87ttq2z6r3pusulg9r24mfj2fvtzd4uq3exn26"
          }
        }
      }
```
A very important distinction to make here is that we do not fill the `funds` field. We are swapping ASTRO (which we obtained from message 2) into Luna (which we borrowed), means our cyclic arbitrage is complete and we can use the obtained Luna from this third swap to repay the borrowed Luna amount with the flashloan (the contract does this for us). However, the ASTRO token we are swapping for Luna is **not** a `native_token` but rather a CW-20 token. This unfortunately requires a different message. So if we decode the `msg` field here we see: 
```json
{
   "send":{
      "amount":"702670777",
      "contract":"terra1e6t37fgjkxrzdx2s95fyq6jdra5s82720vhtmxvx4yhcvnsrey4ssmrya6",
      "msg":"eyJzd2FwIjp7ImJlbGllZl9wcmljZSI6IjIzLjI2NjYyOCIsIm1heF9zcHJlYWQiOiIwLjAwMDUifX0="
   }
}
``` 
Which is a so-called "SendMsg" and it holds its own `msg` field, which is decoded into: 
```json
{
   "swap":{
      "belief_price":"23.266628",
      "max_spread":"0.0005"
   }
}
```
{% hint style="warning" %}
**Important**: when swapping a CW20 token, the `contract_addr` field we use in our messages is the CW20 token address of this specific token, in our example: `terra1nsuqsk6kh58ulczatwev87ttq2z6r3pusulg9r24mfj2fvtzd4uq3exn26`. This address is not the AMM pool address!
{% endhint %}
So where do we find the AMM pool address we want to swap this token on? Well, its baked in the "SendMsg" namely the `contract` field. 

## Executing the message
This section is only necessary if you are trying to use the flashloans via some blockchain client  and are not using our provided [flashloan page](https://app.whitewhale.money/flashloan).


Now that we obtained the full flashloan message, we can send it to the Flashloan router contract, the address of this contract on specific chains can be found [here](/smart-contracts//deployments/). 
We send it by wrapping it in a `MsgExecuteContract` type, which is a wasm-type well known within the cosmos ecosystem. Every client that interacts with wasm-contracts (which the flashloan router contract is) holds a method to send this `MsgExecuteContract` to a specific contract. 
It roughly looks like this: 
```typescript
/** MsgExecuteContract submits the given message data to a smart contract */
export interface MsgExecuteContract {
    /** Sender is the that actor that signed the messages */
    sender: string;
    /** Contract is the address of the smart contract */
    contract: string;
    /** Msg json encoded message to be passed to the contract */
    msg: Uint8Array;
    /** Funds coins that are transferred to the contract on execution */
    funds: Coin[];
}
```
Our designed flashloan message goes in the `msg` field and has to be properly encoded. If you have trouble finding the right encoding, contact us and we are happy to help you out!