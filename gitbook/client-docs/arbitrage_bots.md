# White Whale Arbitrage Documentation

## Version
These docs are updated to be used alongside [bot version v1.2.0](https://github.com/White-Whale-Defi-Platform/white-whale-bots/releases/tag/v1.2.0).

## Setup

+ Install [NodeJS]() and make sure its added to Path
+ Install your favorite IDE that supports TypeScript (Like VSCode)
+ Clone the White Whale Bot [repository](https://github.com/White-Whale-Defi-Platform/white-whale-bots) to your machine
+ Open the repository folder in your IDE as root folder
+ In Console type `npm install` to make sure the required packages are added to the project
+ In Console type `npm run build` to build the project for the first time
+ You are ready to go

## Project Folder Outline
The bot uses an environment file (.env) for the required configuration settings. This file needs to be provided in the root directory of the code in order for the bot to function properly. A typical working directory would look like this (after first a first build with `npm run build`). 
```bash
root
├── .github
├── docs
├── node_modules
├── out
├── src
├── .dockerignore
├── .env.injective.example
├── .env.juno.example
├── .env.terra.example
├── .env  #-- you have to add this file yourself
├── .eslintrc
├── .gitattributes
├── .gitignore
├── docker-compose.yml
├── Dockerfile
├── LICENSE
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
| USE_MEMPOOL      | yes      | "1" \|\| "0"                            | States whether the bot should use mempool to project potential transactions on the actual blockstate and calculate potential arbitrage that arises. **note:** this incurs extra risk of failed transactions and lost gas fees. Defaulted to "1"                                                                            |  |
| GAS_USAGE_PER_HOP  | yes      | "number"                   | Denotes the amount of gas units the bot will use for each hop in a transaction's path. <br />**note:** will only be used when using USE_MEMPOOL=1 or USE_SKIP=1, else the client will estimate gas units and fees |  |
| MAX_PATH_HOPS  | yes      | "number"                   | Denotes the number of pools allowed in one path. E.g. 4 means we will allow paths up to 4 pools to be used in arbitrage |  |
| PROFIT_THRESHOLD | yes      | "number"                          | States the minimal profit threshold the bot will trade, denominated in BASE_DENOM |  |



### **Skip Specific Settings**
{% hint style="info" %}
Note: only relevant when `USE_SKIP = "1"` from general settings
{% endhint %}

| Setting                      | Required | Values                    | Description                                                                                                                                     |
|------------------------------|----------|---------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------|
| USE_SKIP         | no       | "1" \|\| "0"                            | Whether or not to use Skip Protocol for bidding on blockspace to use the bot as MEV arbitrage bot. Defaulted to "0". See [skip specific settings](#skip-specific-settings) for further setup                                                                                                                                                                                      |  |
| SKIP_URL      | yes       | "tokenstring"                     | The skip url to send transaction bundles to for this specific chain. This url is provided by skip.                                                                                                                                                                                                                        |  |
| SKIP_BID_WALLET    | yes       | "channel"                         | The auction house wallet for this specific blockchain. This walletaddress is provided by skip.                                                                                                                                                                                                                                                         |  |
| SKIP_BID_RATE    | yes       | "channel"                         | The bid rate to use with respect to the expected profit of a trade                                                                                                                                                                                                                                                       |  |


### **Logging Specific Settings**
| Setting                      | Required | Values                    | Description                                                                                                                                     |
|------------------------------|----------|---------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------|
| SLACK_TOKEN      | no       | "tokenstring"                     | A OAuth2 Slack token that will be used to log certain events to Slack if provided                                                                                                                                                                                                                        |  |
| SLACK_CHANNEL    | no       | "channel"                         | The specific Slack channel to log to if provided                                                                                                                                                                                                                                                         |  |
| TELEGRAM_CHAT_ID    | no       | "chatid"                         | The specific Telegram chat to log to if provided                                                                                                                                                                                                                                                         |  |
| TELEGRAM_BOT_TOKEN    | no       | "tokenstring"                         | The token for the telegram bot logger                                                                                                                                                                                                                                                         |  |
| DISCORD_WEBHOOK_URL    | no       | "webhookstring"                         | Discord webhook url to use for logging into discord                                                                                                                                                                                                                                                         |  |
| EXTERNAL_EXEMPT_CODES    | no       | "webhookstring"                         | Specific SKIP errors to ignore, only relevant if `USE_SKIP`="1"                                                                                                                                                                                                                                                         |  |
| SIGN_OF_LIFE    | no       | "number"                         | The frequency in minutes for which the bot will send a sign-of-life message                                                                                                                                                                                                                                                         |  |
### **Chain Specific Settings**
| Setting                      | Required | Values                    | Description                                                                                                                                     |
|------------------------------|----------|---------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------|
| BASE_DENOM                   | yes      | "denom"                   | Denom from which the bot will arb from and to. Also the denom that will be used to pay the transaction fees with                                |
| CHAIN_PREFIX                 | yes      | "prefix"                  | Prefix used by the specific chain the bot will run on. E.g. for the Terra chain this means "terra", for Juno chain this means "juno"            |
| RPC_URL                      | yes      | "["url",...]" \|\| "url"  | The RPC-endpoint/s to be used for the bot, this can be either a publicly available endpoint or your own private endpoint **note:** Not required if USE_RPC_URL_SCRAPER = "1"                        |
| USE_RPC_URL_SCRAPER          | no       | "1" \|\| "0"              | Query RPCs from the chainregistry and add to RPC_URL. Urls set in `RPC_URL` are used first.                                                      |
| IGNORE_ADDRESSES             | no       | "["address",...]"         | Add addresses whose trades you want to ignore. Used against mempool spammer.                                                                    |
| GAS_UNIT_PRICE               | yes      | "number"                  | The price in `BASE_DENOM` per gas unit                                                                                                          |
| POOLS                        | yes      | "{pool},{pool},..,{pool}" | The list of pools that will be used to arb with. This setting is explained in more detail below                                                 |
| FACTORIES_TO_ROUTERS_MAPPING | no       | "{mapping},{mapping}"     | A list of mappings from specific pair-factories with their corresponding trade router contracts. This setting is explained in more detail below |
| FLASHLOAN_FEE                | yes      | "number"                  | The flashloan fee white whale charges on taking a loan in percentages, currently 0.15%.                                                         |
                                                           

{% hint style="danger" %} Important: Do not expose the `MNEMONIC` setting described above. Be careful with sharing `.env` files. White Whale will never ask for your MNEMONIC {% endhint %}

### `POOLS` setting
The pools variable represents a list of pools that will be used for arbitrage. However, for each of the pools we have to denote the trading fees that are applied by the DEX. Some DEXes use 0.3% fee and some use 0.4% fee. There's currently not a generic method to derive those fees, therefore we have to enter it manually. There's also a distinction between fees deducted from the incoming asset amount (Uniswap default) and fees deducted from the returned asset amount (Astroport default). Furthermore, DEXs can charge a "protocol fee", which is part of the trading fees, but this fee is not a reward to the LP providers, but goes to the protocol and thus leaves the pool. This ratio of protcol fee vs. LPfee is denoted in the property `LPratio`, which denotes the ratio of the total trading fees that is kept as a reward for the LP providers. </br>
Each pool in the lists has to be in the following format:
```json
{"pool": "terra1zdpq84j8ex29wz9tmygqtftplrw87x8wmuyfh0rsy60uq7nadtsq5pjr7y","inputfee": 0,"outputfee": 0.3, "LPratio":0.5}'
``` 
In which:
* `pool` denotes the address of the pool
* `inputfee` denotes the deducted fee on the input asset
* `outputfee` denotes the deducted fee on the returned asset
* `LPratio` denotes the ratio of `inputfee` and `outputfee` that is kept in the pool as LP rewards
Each pool object in the list is separated by a `,`, multiple entries therefore look like this:
```json
POOLS='{"pool": "terra1fd68ah02gr2y8ze7tm9te7m70zlmc7vjyyhs6xlhsdmqqcjud4dql4wpxr","inputfee": 0,"outputfee": 0.3, "LPratio":0.5},
{"pool": "terra1zrs8p04zctj0a0f9azakwwennrqfrkh3l6zkttz9x89e7vehjzmqzg8v7n","inputfee": 0,"outputfee": 0.3, "LPratio":0.2},
{"pool": "terra190alph3r79rm2ypefamglwk53ln2qr3ud09sa3mnxexxf0p8xv3qzume3r","inputfee": 0,"outputfee": 0.25, "LPratio":0.2}'
```
### `FACTORIES_TO_ROUTERS_MAPPING` setting
This variable sets a mapping between pool factories and pool routers. Factories are used by protocols to create new pools on-chain and hold all created pools by the factory. Routers are used for swaps that have to go trough multiple pools to achieve the requested asked asset. The mapping is used to backwards engineer the affected pools from an on-chain router message. 
The mappings are separated the the same way as the POOL variables are separated, an example:
```json
FACTORIES_TO_ROUTERS_MAPPING='{"factory":"terra1f4cr4sr5eulp3f2us8unu6qv8a5rhjltqsg7ujjx6f2mrlqh923sljwhn3","router":"terra1p37jrwlaqpklzlu4rwjyjrmzuezdgk3pyuyk2zclc4rda6awkm3qnj6f0a"}, 
{"factory":"terra14x9fr055x5hvr48hzy2t4q7kvjvfttsvxusa4xsdcy702mnzsvuqprer8r","router":"terra1j8hayvehh3yy02c2vtw5fdhz9f4drhtee8p5n5rguvg3nyd6m83qd2y90a"}'
```

A full example of a `.env` file can be found [here](configexample.md)

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

Every `SIGN_OF_LIFE` minutes it will log a sign of life to the format depending on the [Logging Specific Settings](#logging-specific-settings). 
