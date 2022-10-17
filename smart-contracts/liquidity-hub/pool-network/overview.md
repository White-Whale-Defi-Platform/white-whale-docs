# Pool Network

The pool network is a WW-controlled collection of Automated Market Maker (AMM) pools of WW-selected tokens (WW pools) relevant 
to the chain of the pool network (e.g., Atom-Luna and Atom-Juno LPs on both Terra and Juno chains). The token price exchange 
in each pool in the local pool network loosely represents the "interchain price" for the token because when the price changes 
of one pool on one network (e.g., Juno) then the Interchain Command will take action to balance the price of the same pool on 
the other network(s) (e.g., Terra). These WW pools allow bots to arb the local dexes versus the "interchain price" that 
effectively decreases price disparities. Currently, users can find price disparities of up to 20% for the same token trading on different Cosmos blockchains.

White Whale's pool network is based on [Terraswap](https://github.com/terraswap/terraswap), a Uniswap-inspired automated 
market-maker (AMM) protocol.

The code for the pool network can be found [here](https://github.com/White-Whale-Defi-Platform/migaloo-core/tree/main/contracts/liquidity_hub/pool-network). 

## Contracts

| Name                                     | Description                                                                |
| ---------------------------------------- |----------------------------------------------------------------------------|
| [`terraswap_factory`](terraswap_factory) | Factory used to create pools (pairs)                                       |
| [`terraswap_pair`](terraswap_pair)       | Pair (pool) contract                                                       |
| [`terraswap_router`](terraswap_router)   | Allows multi-hob swaps                                                     |
| [`terraswap_token`](terraswap_token)     | CW20 (ERC20 equivalent) token implementation. Used for creating LP tokens. |

## Running the Pool Network

You will need Rust 1.64.0+ with wasm32-unknown-unknown target installed.

You can run unit tests on each contract directory via:

```
cargo test
```

To compile each individual contract, you can run:

```
cargo build
cargo wasm
```

Or for a production-ready (optimized) build, run the following from the `migaloo-core` repository:

```
scripts/build_release.sh
```

The optimized contracts are generated in the artifacts/ directory.
