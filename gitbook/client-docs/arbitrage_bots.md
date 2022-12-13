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
### **General Settings**
| Setting          | Required | Values| Description                                                                                                                                                                                                                                                                                              |
|------------------|----------|-----------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| WALLET_MNEMONIC  | yes      | 24-words forming the mnemonic key | The mnemonic used to sign transactions and pay the gas fee                                                                                                                                                                                                                                               |  |
| USE_MEMPOOL      | yes      | "1"/"0"                           | States whether the bot should use mempool to project potential transactions on the actual blockstate and calculate potential arbitrage that arises. **note:** this incurs extra risk of failed transactions and lost gas fees. Defaulted to "1"                                                                            |  |
| GAS_UNIT_USAGES  | yes      | "number,number"                   | Denotes the amount of gas units the bot will use for transactions. The first number corresponds to a 2-message arbitrage transaction and the second to a 3-or-more-message arbitrage transaction. **note:** will only be used when using USE_MEMPOOL=1, else the client will estimate gas units and fees |  |
| PROFIT_THRESHOLD | yes      | "number"                          | States the minimal profit threshold as a multiplier of the paid transaction fees, differentiated between a 2-message arbitrage and a 3-or-more-message arbitrage transaction                                                                                                                             |  |
| SLACK_TOKEN      | no       | "tokenstring"                     | A OAuth2 Slack token that will be used to log certain events to Slack if provided                                                                                                                                                                                                                        |  |
| SLACK_CHANNEL    | no       | "channel"                         | The specific Slack channel to log to if provided                                                                                                                                                                                                                                                         |  |
| USE_SKIP         | no       | "1"/"0"                           | Whether or not to use Skip Protocol for bidding on blockspace to use the bot as MEV arbitrage bot. Defaulted to "0"                                                                                                                                                                                      |  |
| SKIP_BID_RATE    | no       | "number"                          | The fraction of profit to be used as height of the bid for the blockspace. E.g. 0.1 means 10% of the calculated expected profit is used to bid on the transaction using Skip Protocol. Requires `USE_SKIP`="1"                                                                                           |  |

### **Chain Specific Settings**
| Setting                      | Required | Values                    | Description                                                                                                                                     |
|------------------------------|----------|---------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------|
| BASE_DENOM                   | yes      | "denom"                   | Denom from which the bot will arb from and to. Also the denom that will be used to pay the transaction fees with                                |
| CHAIN_PREFIX                 | yes      | "prefix"                  | Prefix used by the specific chain the bot will run on. E.g. for the Terra chain this means "terra", for Juno chain this means "juno"            |
| RPC_URL                      | yes      | "url"                     | The RPC-endpoint to be used for the bot, this can be either a publicly available endpoint or your own private endpoint                          |
| GAS_UNIT_PRICE               | yes      | "number"                  | The price in `BASE_DENOM` per gas unit                                                                                                          |
| POOLS                        | yes      | "{pool},{pool},..,{pool}" | The list of pools that will be used to arb with. This setting is explained in more detail below                                                 |
| FACTORIES_TO_ROUTERS_MAPPING | yes      | "{mapping},{mapping}"     | A list of mappings from specific pair-factories with their corresponding trade router contracts. This setting is explained in more detail below |
| SKIP_URL                     | no       | "skipurl"                 | The endpoint provided by Skip Protocol to broadcast transactions to. Requires `USE_SKIP`="1"                                                    |
| SKIP_BID_WALLET              | no       | "walletaddress"           | The Skip Protocol auction wallet to send the bid to. Requires `USE_SKIP`="1"                                                                    |

{% hint style="danger" %} Important: Do not expose the `MNEMONIC` setting described above. Be careful with sharing `.env` files. White Whale will never ask for your MNEMONIC {% endhint %}

### `POOLS` setting
The pools variable represents a list of pools that will be used for arbitrage. However, for each of the pools we have to denote the trading fees that are applied by the DEX. Some DEXes use 0.3% fee and some use 0.4% fee. There's currently not a generic method to derive those fees, therefore we have to enter it manually. There's also a distinction between fees deducted from the incoming asset amount (Uniswap default) and fees deducted from the returned asset amount (Astroport default). Each pool in the lists has to be in the following format:
```json
{"pool": "terra1zdpq84j8ex29wz9tmygqtftplrw87x8wmuyfh0rsy60uq7nadtsq5pjr7y","inputfee": 0,"outputfee": 0.3}'
``` 
In which:
* `pool` denotes the address of the pool
* `inputfee` denotes the deducted fee on the input asset
* `outputfee` denotes the deducted fee on the returned asset
Each pool object in the list is separated by a `,`, multiple entries therefore look like this:
```json
POOLS='{"pool": "terra1fd68ah02gr2y8ze7tm9te7m70zlmc7vjyyhs6xlhsdmqqcjud4dql4wpxr","inputfee": 0,"outputfee": 0.3},
{"pool": "terra1zrs8p04zctj0a0f9azakwwennrqfrkh3l6zkttz9x89e7vehjzmqzg8v7n","inputfee": 0,"outputfee": 0.3},
{"pool": "terra190alph3r79rm2ypefamglwk53ln2qr3ud09sa3mnxexxf0p8xv3qzume3r","inputfee": 0,"outputfee": 0.25}'
```
### `FACTORIES_TO_ROUTERS_MAPPING` setting
This variable sets a mapping between pool factories and pool routers. Factories are used by protocols to create new pools on-chain and hold all created pools by the factory. Routers are used for swaps that have to go trough multiple pools to achieve the requested asked asset. The mapping is used to backwards engineer the affected pools from an on-chain router message. 
The mappings are separated the the same way as the POOL variables are separated, an example:
```json
FACTORIES_TO_ROUTERS_MAPPING='{"factory":"terra1f4cr4sr5eulp3f2us8unu6qv8a5rhjltqsg7ujjx6f2mrlqh923sljwhn3","router":"terra1p37jrwlaqpklzlu4rwjyjrmzuezdgk3pyuyk2zclc4rda6awkm3qnj6f0a"}, 
{"factory":"terra14x9fr055x5hvr48hzy2t4q7kvjvfttsvxusa4xsdcy702mnzsvuqprer8r","router":"terra1j8hayvehh3yy02c2vtw5fdhz9f4drhtee8p5n5rguvg3nyd6m83qd2y90a"}'
```

A full example of a `.env` file can be found [here](/client-docs/configexample.md)

### Your First Run 
After following the instructions described above we can start the bot for the first time. It will look for arbitrage opportunities on the provided pools on a 2-hop basis as well as a 3-hop basis. 
In the root folder:
{% tabs %}
{% tab title="Linux" %}
```bash 
npm start
```
in console
{% endtab %}
{% tab title="Windows" %}
```bash
npm run build "&&" node out/index.js
```
in console
{% endtab %}
{% endtabs %}

The bot will start running and initialising the entered configuration file, example output:
Every 150 blocks it will log a sign of life, if `SLACK_TOKEN` is provided this will happen to the provided `SLACK_CHANNEL`, if not it will log to `stdout`. Every trade attempt will also be logged.