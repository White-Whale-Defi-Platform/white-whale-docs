# White Whale Arbitrage Documentation


## Setup

+ Install [NodeJS]() and make sure its added to Path
+ Install your favorite IDE that supports TypeScript (Like VSCode)
+ Clone the White Whale Bot [repository](https://github.com/White-Whale-Defi-Platform/migaloo-bots) to your machine
+ Open the repository folder in your IDE as root folder
+ In Console type `npm install` to make sure the required packages are added to the project
+ In Console type `npm run build` to build the project for the first time
+ You are ready to go

## Project Folder Outline
The bot uses an environment file (.env) for the required configuration settings. This file needs to be provided in the root directory of the code in order for the bot to function properly. A typical working directory would look like this (after first a first build with `npm run build`). 
```bash
root
├── node_modules
├── out
├── src
├── .env  #-- you have to add this file yourself
├── .gitignore
├── package.json
├── package-lock.json
├── README.md
└── tsconfig.json
```

## The Configuration File (`.env `)
There are multiple properties that are required to be set for the bot to function properly.  Also, there are a few properties that are optional and influence the bots behaviour, although they are not required, it is adviced to include them in the `.env` anyways and make sure they are switched off. Below a full list of configuration settings used by the bot, all settings are to be formatted as `string`.  

|Setting |Optional  | Description                        |
|--------|----------|------------------------------------|
|test    | test     | test                               | 
|test    | test     | test                               | 

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

### Example Config 

```
WALLET_MNEMONIC="white whale is awesome we wish we had open sourced arbitrage bots way earlier when it was still a bull market and make some money"

USE_MEMPOOL="0"

BASE_DENOM="uluna"

CHAIN_PREFIX="terra"

RPC_URL="https://rpc-terra.whitewhale.money"

POOLS='{"pool": "terra1fd68ah02gr2y8ze7tm9te7m70zlmc7vjyyhs6xlhsdmqqcjud4dql4wpxr", "fee":0.3}, 
{"pool": "terra1zrs8p04zctj0a0f9azakwwennrqfrkh3l6zkttz9x89e7vehjzmqzg8v7n", "fee": 0.3}, 
{"pool": "terra190alph3r79rm2ypefamglwk53ln2qr3ud09sa3mnxexxf0p8xv3qzume3r", "fee": 0.25}, 
{"pool": "terra1ck8nkz35sa8mmqez3lqrm77vh36n2gd2f0dxjde4uemkwsjt22pqgk49zj", "fee": 0.3}, 
{"pool": "terra1h3wqh8fdsd8rr6rlz3yfp9sm8849wrec8vqsmkwksx0ndkqaxkjqellq28", "fee": 0.3}, 
{"pool": "terra13rj43lsucnel7z8hakvskr7dkfj27hd9aa06pcw4nh7t66fgt7qshrpmaw", "fee": 0.3}, 
{"pool": "terra1e6t37fgjkxrzdx2s95fyq6jdra5s82720vhtmxvx4yhcvnsrey4ssmrya6", "fee": 0.3}, 
{"pool": "terra1frfcj4xhvx0emkup4vel5jun9zun0797j5yhn7ant3r4jzy9mkxqzcwev6", "fee": 0.3}, 
{"pool": "terra1p2xgcr2ewnetug8ahqms5y3k6rxyh2xglnzzx500ylh4420h9ucqz8w7x5", "fee": 0.3}, 
{"pool": "terra17l9xj8f6m8smumhn8wgpgnswr3mu60wfkcm6pjc69drxp0t398rs7335vn", "fee": 0.3}, 
{"pool": "terra1qzux5j9he9nv95kq3unkuzy0hddf080um2t243raatg3f6requwsaahpqp", "fee": 0.3}, 
{"pool": "terra1w579ysjvpx7xxhckxewk8sykxz70gm48wpcuruenl29rhe6p6raslhj0m6", "fee": 0.3}, 
{"pool": "terra1u3wd9gu7weezw6vwfaaa4q589zjlazg6wt6gyer3lc42tgqrpggqv90c2c", "fee": 0.3}, 
{"pool": "terra1gwnwqdwz7taadacdw45q7kwz3q7h0hfrc4f3xpxas4j869tqexxsxze6gz", "fee": 0.25}, 
{"pool": "terra1jynmf6gteg4rd03ztldan5j2dp78su4tc3hfvkve8dl068c2yppsk5uszc", "fee": 0.3}, 
{"pool": "terra1zdpq84j8ex29wz9tmygqtftplrw87x8wmuyfh0rsy60uq7nadtsq5pjr7y", "fee": 0.3}'

FACTORIES_TO_ROUTERS_MAPPING ='{"factory":"terra1f4cr4sr5eulp3f2us8unu6qv8a5rhjltqsg7ujjx6f2mrlqh923sljwhn3","router":"terra1p37jrwlaqpklzlu4rwjyjrmzuezdgk3pyuyk2zclc4rda6awkm3qnj6f0a"}, 
{"factory":"terra14x9fr055x5hvr48hzy2t4q7kvjvfttsvxusa4xsdcy702mnzsvuqprer8r","router":"terra1j8hayvehh3yy02c2vtw5fdhz9f4drhtee8p5n5rguvg3nyd6m83qd2y90a"}'

```

### Your First Run 

After following the instructions described in  and  we can start the bot for the first time. It will look for arbitrage opportunities on the provided pools on a 2-hop basis, meaning a trade exists of two pools directly connected to each other and thus holding two of the same assets. For this initial basic run we assume the option USE_MEMPOOL is set to "0". 
In the root folder:
for Linux users: type npm start in console
for Windows users: type npm run build && node out/index.js in console
The bot will start running and initialising the entered configuration file, example output:

The bot will now receive an Event from the connected node (the RPC endpoint) when an new block is created. At that point the bot will update the states of the pools and see if there's an arbitrage opportunity available. On each new block it will print the height of the block, the optimal tradesize found and the corresponding profit:

```
new block:  1940869 updating states
optimal tradesize:  1929960  with profit:  1999

//please note: tradesize and profit are in uluna 
```