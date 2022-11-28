<!-- Documents examples of flashloan usages -->
# Calling Flashloans

The White Whale Flashloan operation is a specific property of each of the [Vaults](/smart-contracts/liquidity-hub/vault-network/vault.md) deployed by White Whale. However, these flashloan messages are only executable by smart-contracts by design. So, to enable users (off-chain clients) to use flashloans without writing smart contracts, White Whale deployed a "Generalized Flashloan Router" [contract](../smart-contracts/liquidity-hub/vault-network/vault-router.md). This contract (also called vault-router) is able to perform all the required flashloan operations without the user to specify each step. 
A very important property of this contract is that it is able to "route" the requested asset by the user to the right vault, thus, we only need **one** flashloan router contract for all vaults deployed on a chain and a user simply has to provide the requested asset.

We will first briefly describe the message that a user needs to send to this flashloan router contract and then show a step-by-step example of how to obtain such a message for a specific use case.

## Flashloan Router
The flashloan router [contract](../smart-contracts/liquidity-hub/vault-network/vault-router.md) requires a specific ExecuteMsg to be executed properly, this Msg is called "Flashloan". The message is described briefly in [this](../smart-contracts/liquidity-hub/vault-network/vault-router.md#flashloan) section, however we will explain it with more details in this section. 



