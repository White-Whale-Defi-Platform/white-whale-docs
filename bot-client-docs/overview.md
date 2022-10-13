# Bot Client Docs 
White Whale Arbitrage Bot Client Documentation

## Overview

The White Whale protocol is designed as an interchain liquidity platform within the Cosmos Ecosystem. Read everything about the protocol at our website: https://whitewhale.money/.
An important part of the White Whale mission is making arbitrage more accessible to the bigger crowd and the development of open-sourced arbitrage bots is one of the strategies to achieve this. 
These docs are designed as a manual for running the arbitrage bots and will contain additional information regarding the off-chain usage of the on-chain protocol (smart contracts) as well.

## Quick Links

+ [The White Whale Protocol](https://whitewhale.money)
+ [The White Whale Protocol App](https://app.whitewhale.money)

## Prerequisites 

The White Whale Arbitrage bot is built in [TypeScript](https://www.typescriptlang.org/) and makes use of the [CosmJS](https://cosmos.github.io/cosmjs/) package

## Setup

+ Install [NodeJS]() and make sure its added to Path
+ Clone the White Whale Bot repository to your machine

## Configuration
The bot uses an environment file (.env) as configuration. This file needs to be provided in the root directory of the code in order for the bot to function properly. A typical working directory would look like this (after first a first build). 
```
root
├── node_modules
├── out
├── src
├── .env
├── .gitignore
├── package.json
├── package-lock.json
├── README.md
└── tsconfig.json
```

### Properties
There are multiple properties to be set in the .env file. You will be prompted if one or more are missing. 
WALLET_MNEMONIC
The mnemonic key that will be used for signing transactions and paying fees.
WALLET_MNEMONIC="white whale is awesome we wish we had open sourced arbitrage bots way earlier when it was still a bull market and make some money"
Make sure to never share or expose the MNEMONIC. Nobody from the White Whale team will ever ask your MNEMONIC and you should never share it.
USE_MEMPOOL
Denotes whether or not to use the memory pool to gain an information advantage over the on-chain state of the pools. This tries to project transactions from the memory pool to the current state of the blockchain before they are actually processed by the validators. 
The use of the memory pool might lead to failing transactions and is an advanced feature. Transactions that will trigger the bot aren't verified yet and therefore might be faulty.
CHAIN_PREFIX
Denotes the prefix of the addresses used on the chosen blockchain. Example values: 
juno, terra, osmo. 
CHAIN_PREFIX="terra"
BASE_DENOM
Denotes the currency which is used as base currency for the arbitrage opportunities. In addition, fees will be paid using the denom set in this option. 
BASE_DENOM="uluna"
RPC_URL
This sets the RPC endpoint that will be used to query and broadcast. Please note, the bot uses a websocket subscription to a websocket endpoint. It is assumed the websocket endpoint is available on the same URL. 
RPC_URL="https://rpc-terra.whitewhale.money"
POOLS
The POOLS setting is used to provide a list of pools that will be checked for arbitrage opportunity. In addition to stating the pool address, the used trading fee of that pool address is also provided in this environment variable. Each pool is stated as:
{"pool": "terra1fd68ah02gr2y8ze7tm9te7m70zlmc7vjyyhs6xlhsdmqqcjud4dql4wpxr", "fee":0.3}
The pools are contained in one string value and separated by a comma, space and \n combination. When combined the POOLS variable therefore looks like this:

### FACTORIES_TO_ROUTERS_MAPPING
This variable sets a mapping between pool factories and pool routers. Factories are used by protocols to create new pools on-chain and hold all created pools by the factory. Routers are used for swaps that have to go trough multiple pools to achieve the requested asked asset. The mapping is used to backwards engineer the affected pools from an on-chain router message. 
The mappings are separated the the same way as the POOL variables are separated. 
```python
FACTORIES_TO_ROUTERS_MAPPING ='{"factory":"terra1f4cr4sr5eulp3f2us8unu6qv8a5rhjltqsg7ujjx6f2mrlqh923sljwhn3","router":"terra1p37jrwlaqpklzlu4rwjyjrmzuezdgk3pyuyk2zclc4rda6awkm3qnj6f0a"}, 
{"factory":"terra14x9fr055x5hvr48hzy2t4q7kvjvfttsvxusa4xsdcy702mnzsvuqprer8r","router":"terra1j8hayvehh3yy02c2vtw5fdhz9f4drhtee8p5n5rguvg3nyd6m83qd2y90a"}'
```