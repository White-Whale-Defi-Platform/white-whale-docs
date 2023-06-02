# How to update one or more of the Fees associated with a pool 

Pools deployed by White Whale Liquidity Hub all have the capability to set a custom fee on the creation of the pool. For more info on the types of Fees, [refer here](../liquidity-hub/pool-network/terraswap-pair.md#fees)

The majority of the pools are deployed with the same Fee configurations where possible to ensure same fees are charged on every pool but this is only a convenience, anyone creating a pool can either request their own custom fees; or at a further point may want to raise or lower fees. 
This small document covers how an admin can update the fees for a given pool or a number of pools: 

## Performing an update 
The only way to update fees on a pool is through a config update which is exposed via `ExecuteMsg::UpdateConfig` on each deployed pool. 
The `UpdateConfig` execute message allows an admin to change any important details such as the charged. 

This is an example of what the pool configs look like, for up to date info, [refer to](../liquidity-hub/pool-network/terraswap-pair.md#config)

```json
{
  "owner": "juno1...",
  "fee_collector_addr": "juno1...",
  "pool_fees": {
    "protocol_fee": {
      "share": "0.001"
    },
    "swap_fee": {
      "share": "0.002"
    },
    "burn_fee": {
      "share": "0.001"
    }
  },
  "feature_toggle": {
    "withdrawals_enabled": true,
    "deposits_enabled": true,
    "swaps_enabled": true
  }
}
```

> Currently at the time of writing, the majority of chain deployments have 3 chargeable fees. These are [Protocol Fees](../liquidity-hub/pool-network/terraswap-pair.md#protocol-fees), [Swap Fees](../liquidity-hub/pool-network/terraswap-pair.md#protocol-fees) and [Burn Fees](../liquidity-hub/pool-network/terraswap-pair.md#burned-fees) which each serve different purposes. 
> Generally when updating one fee, all should be updated unless you want to simply remove a type of fee. 

### Example of removing burn fee on a pool
Lets say for example we want to update the fees for 5 pools and we want to remove the `burn_fee` from them so that there is no longer burned tokens on a swap. 
You can send an UpdateConfig message request from the right wallet depending on permissions to update only the burn fee 

```json
{
  "pool_fees": {
    "burn_fee": {
      "share": "0.001"
    }
  },
}
```

### Example of removing flash fee on a vault

Its important to state again here that a flashloan vault in the current WhiteWhale design is similar to a Pool in the sense that both return a token which is used to track the user share of a pool. 
They have other similarities in how they deal with fees in that while there is no swap fee there is a `flash loan fee`. For full info on the types of fees on a vault refer to [Vault Fees](../liquidity-hub/vault-network/vault.md#fees)

In the case of a vault we have fees again stored in the [config](../liquidity-hub/vault-network/vault.md#config)

The process for updating a Vaults fees is identical to updating or a pool in that we must call [UpdateConfig](../liquidity-hub/vault-network/vault.md#update-config)

Updating only the flash_loan_fee would look something like this :

```json
{
  "fees": {
    "flash_loan_fee": {
      "share": "0"
    },
  }
}
```

### Updating multiple 
Coming back to the example of 

> Lets say for example we want to update the fees for 5 pools

Where its pools or vaults the process remains the same highlighted above but this then must be performed on each pool/vault you wish to update. 
Considering the amount of growing deployments and vaults this number can grow and it would be wise to do it via a script which simply sends the same JSON to each one. 

