# Guide to Creating Osmosis Pool Interfaces

## Introduction

For White Whale pools to appear on the osmosis frontend, there needs to be deployed a contract that implements 
the [following interface](https://docs.osmosis.zone/osmosis-core/modules/cosmwasmpool#cosmwasm-pool-contract-interface).

This interface contract essentially translates White Whale's pool contract queries and messages to the one the Osmosis 
Pool Manager can handle.

This guide outlines the detailed process of creating such interface contract for the White Whale's ecosystem on Osmosis, 
ensuring a comprehensive and accurate setup. By following these steps, you can create and manage interface contracts
effectively.

## Prerequisites

- You must have a pool deployed on the White Whale Dex on the Osmosis chain. To learn how to do that, follow [this guide](create-pools.md).
- Once the pool has been deployed, you can proceed on this guide.

## 1. Preparation

### Install osmosisd

- Make sure you have `osmosisd` installed on your system.
- Get Osmosis mainnet details. Check [this env](https://github.com/White-Whale-Defi-Platform/white-whale-core/blob/main/scripts/deployment/deploy_env/mainnets/osmosis.env) file used by white-whale-core.

### Get some USDC on Osmosis

- At the time of this writing, it costs 20 USDC to deploy a pool on Osmosis. Load your wallet with that amount.

## 2. Create the pool 

- The current ww pool interface contract has code id `641`. Please double, triple check that by querying one of established 
ww interface contracts, which can be found [here](../deployments/liquidity-hub/osmosis.md). You can query the contract 
details like this `$BINARY query wasm contract $contract --node $RPC -o json | jq`.

{% hint style="warning" %}
**Note**: The following step is **critical**. Messing this one up (using the wrong interface contract for example), would 
likely break Osmosis Frontend. Nobody wants that. Make sure you follow the instructions given.
{% endhint %}

- Once you verified the code id, you can run the following command `$BINARY tx cosmwasmpool create-pool 641 '{"white_whale_pool": "osmo1..."}' $TXFLAG --from wallet`,
 where `white_whale_pool` in the instantiate message of the contract is the ww pool address you want to associate the 
interface with. This command can be triggered by any wallet, it doesn't need to be whitelisted anywhere.

## 3. Update the osmosis interface on the pool

- Once that's done, you can inspect the TX HASH to see the pool id on the Osmosis pool manager, as well as the interface contract address.
- Grab that interface address and call `UpdatePairConfig` on the pool factory. This is a sample message:

```json
{
  "update_pair_config": {
    "pair_addr": "osmo1...",
    "cosmwasm_pool_interface": "osmo1..."
  }
}
```

## 4. Update the docs

- Update the [Osmosis deployments](../deployments/liquidity-hub/osmosis.md) to include the interface you just created.

## Conclusion

By following this guide and utilizing the provided instructions, you can ensure the accurate creation and documentation 
of the osmosis interface contract.

For more information, check the [Osmosis official documentation](https://docs.osmosis.zone/osmosis-core/modules/cosmwasmpool).