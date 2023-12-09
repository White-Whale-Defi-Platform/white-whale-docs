# Terra Classic (columbus-5)

```json
{
  "contracts": [
    {
      "wasm": "fee_collector.wasm",
      "code_id": "7968",
      "version": "1.1.2",
      "contract_address": "terra1mlw8qmxjxwru5ctp4hkxhsxtzzxr0pkvsytkqwg32axfyhnxca2qv8gxgx"
    },
    {
      "wasm": "fee_distributor.wasm",
      "code_id": "7969",
      "version": "0.9.2",
      "contract_address": "terra1d2p6vqyynhn2eraf74qtedaugfuknt32wnsm8e4uskfqv2jersdqkstzer"
    },
    {
      "wasm": "frontend_helper.wasm",
      "code_id": "7928",
      "version": "1.0.0",
      "contract_address": "terra1pew7zvqmg8lq4v8hd4gtr6832exrzcsu8wz6eh9388kx5lpt75sq8j5vsk"
    },
    {
      "wasm": "incentive.wasm",
      "code_id": "7927",
      "version": "1.0.3"
    },
    {
      "wasm": "incentive_factory.wasm",
      "code_id": "7926",
      "version": "1.0.0",
      "contract_address": "terra1zuyalae3t5qg4gkumff0mj5he6auv73n467jknj4p6pr00wqmnjqdxv6cx"
    },
    {
      "wasm": "stableswap_3pool.wasm",
      "code_id": "7904",
      "version": "1.2.1"
    },
    {
      "wasm": "terraswap_factory.wasm",
      "code_id": "7905",
      "version": "1.2.0",
      "contract_address": "terra1wyqd3gk7pdknt5xtapdgzlr658a9tn3jryn0rzxwnvv6f0jhlcesl758m0"
    },
    {
      "wasm": "terraswap_pair.wasm",
      "code_id": "7906",
      "version": "1.3.1"
    },
    {
      "wasm": "terraswap_router.wasm",
      "code_id": "7907",
      "version": "1.1.0",
      "contract_address": "terra1prptgzfnpahp7fl9f7um7npkt9xw3mve9cfnxkglu60x840qaw9qpk2cqn"
    },
    {
      "wasm": "terraswap_token.wasm",
      "code_id": "7908",
      "version": "1.0.2"
    },
    {
      "wasm": "vault_factory.wasm",
      "code_id": "7910",
      "version": "1.1.3",
      "contract_address": "terra1ay6nmzavhylwr4nwvsxjhl0we2ahdfn66m5z7jczc62rl499tddq8mr2hm"
    },
    {
      "wasm": "whale_lair.wasm",
      "code_id": "7909",
      "version": "0.9.1",
      "contract_address": "terra1fatrd72lsf5hv59aeg9w00lg8yqz2fqthxxh9u9k63sngzm5nrdszt0w9u"
    }
  ],
  "date": "2023-08-28T11:03:19+0000",
  "initial_block_height": "null",
  "final_block_height": "14301231",
  "chain_id": "columbus-5",
  "deployer_address": "terra1rudglghm48d2k2u9eljh3h4m5pdv2s3h60s3hx"
}

```

```json
{
  "pools": [
    {
      "pair": "uluna-uwhale",
      "assets": [
        "{\"token\":{\"native_token\":\"uluna\"}}",
        "{\"token\":{\"native_token\":\"ibc/077EE5F87CE5CD419436D26533329BDC7BEE6850AD64BC316486B0DCCB13C0EB\"}}"
      ],
      "pool_address": "terra1t02akvjklp7h8swg7vhdjryegj9z7q83hjhyq8xssc4v0qv7a67s6um6up",
      "lp_address": "terra1cfjnwpjswp9a94y5he2tz0e9rhlcd8rslydsrrfes6xafrx0wzrsaerydc",
      "pool_code_id": "7906",
      "lp_code_id": "7908"
    },
    {
      "pair": "uluna-uusd",
      "assets": [
        "{\"token\":{\"native_token\":\"uluna\"}}",
        "{\"token\":{\"native_token\":\"uusd\"}}"
      ],
      "pool_address": "terra1wm3jtcq0fuftvmfq0skmqyxnl3x3j42x8ae56q7eg7v6jsf5eg4qmz36ts",
      "lp_address": "terra1tlg8cvzfhc9z5d4lyr8c6gvy555a8wtat3mj3nmf69nl3ypndj7sfvr0au",
      "pool_code_id": "7906",
      "lp_code_id": "7908"
    }
  ],
  "date": "2023-01-05T15:59:41+0000",
  "chain_id": "columbus-5",
  "pool_factory_addr": ""
}
```

```json
{
  "pool_incentives": [
    {
      "pool": "terra1t02akvjklp7h8swg7vhdjryegj9z7q83hjhyq8xssc4v0qv7a67s6um6up",
      "pool_label": "uluna-ibc/077E...C0EB",
      "incentive_contract": "terra174njy7232hrzx80cfrktl6s24f2xcusyu3mf986yfatrmrv3ryask45wl9"
    },
    {
      "pool": "terra1wm3jtcq0fuftvmfq0skmqyxnl3x3j42x8ae56q7eg7v6jsf5eg4qmz36ts",
      "pool_label": "uluna-uusd",
      "incentive_contract": "terra1w088w23xywkfndukqgcj3d9j73tsr459l370suycmvsj6yedr6qqfn2w7g"
    }
  ],
  "date": "2023-09-05T12:10:43+0000",
  "initial_block_height": "14415269",
  "final_block_height": "14415394",
  "chain_id": "columbus-5",
  "deployer_address": "terra1rudglghm48d2k2u9eljh3h4m5pdv2s3h60s3hx"
}
```

# Terra Classic testnet (rebel-2)

```json
{
  "contracts": [
    {
      "wasm": "fee_collector.wasm",
      "code_id": "654",
      "version": "1.1.1",
      "contract_address": "terra10z5c9fkx4262kjr3h69xmuug279dx64tkw5dxpgz79l7lqkzq3mstknhwq"
    },
    {
      "wasm": "fee_distributor.wasm",
      "code_id": "639",
      "version": "0.9.1",
      "contract_address": "terra1l2pnsghruf0fdv37200qzl7038jly7xvektz8l6neqvn3ppmac4qnas7wr"
    },
    {
      "wasm": "frontend_helper.wasm",
      "code_id": "640",
      "version": "1.0.0",
      "contract_address": "terra1adc4snchrn92zu6y3nxmxxzp0jlg287d7nx00q0j6hfxnjhpzs4q4pujj8"
    },
    {
      "wasm": "incentive.wasm",
      "code_id": "641",
      "version": "1.0.3"
    },
    {
      "wasm": "incentive_factory.wasm",
      "code_id": "642",
      "version": "1.0.0",
      "contract_address": "terra1g8k0n2xgzaeaw79vx2tcyq0cdaew64206h3wq8yscmfna57cygrsk29tpc"
    },
    {
      "wasm": "stableswap_3pool.wasm",
      "code_id": "643",
      "version": "1.2.1"
    },
    {
      "wasm": "terraswap_factory.wasm",
      "code_id": "644",
      "version": "1.2.0",
      "contract_address": "terra1p2mttks887azh0py7nz9zguptp755tdxfhewez60ck9z7j4rrp2sgvch8s"
    },
    {
      "wasm": "terraswap_pair.wasm",
      "code_id": "645",
      "version": "1.3.1"
    },
    {
      "wasm": "terraswap_router.wasm",
      "code_id": "653",
      "version": "1.1.0",
      "contract_address": "terra1xzcqkjjktls23lv8lasqmygujje5z0wglwjgh4tvx2ta7t08zgsqq5nn6y"
    },
    {
      "wasm": "terraswap_token.wasm",
      "code_id": "647",
      "version": "1.0.2"
    },
    {
      "wasm": "vault.wasm",
      "code_id": "661",
      "version": "1.2.3"
    },
    {
      "wasm": "vault_factory.wasm",
      "code_id": "649",
      "version": "1.1.3",
      "contract_address": "terra1mzswuxkycf2pmvcxnzf4y7g5eaelzqqc9d3twkech5yrpw8ztd0q7wdmf7"
    },
    {
      "wasm": "vault_router.wasm",
      "code_id": "662",
      "version": "1.1.5",
      "contract_address": "terra1jzjvng7k00005pd84kkcrlgz2gr4kyd8z7t6zg02nnjw7yag2wgqq352lt"
    },
    {
      "wasm": "whale_lair.wasm",
      "code_id": "651",
      "version": "0.9.1",
      "contract_address": "terra12qrx84qut6ht0yvjw2cqa4vhrpah3ys5e35gpyq9duw8vhetw2cs04zl7x"
    }
  ],
  "date": "2023-08-25T15:03:06+0000",
  "initial_block_height": "null",
  "final_block_height": "15855019",
  "chain_id": "rebel-2",
  "deployer_address": "terra1rmzydhhpgqpr3v8sfu82ewj7fj9rl6sfnnrcu8"
}

```

```json
{
  "pools": [
    {
      "pair": "uluna-willyn",
      "assets": [
        "{\"token\":{\"native_token\":\"uluna\"}}",
        "{\"token\":{\"token\":\"terra18qcy2t7tnyshe4zcx0jujkt22lyxtluvdg0pfjlrjp95snasql0shfjqh9\"}}"
      ],
      "pool_address": "terra1g3vdgpjdrertcqvg7fgwzzcv29ty4fqdt5lnf5wv97q0705f2cvsszw0gw",
      "lp_address": "terra1kpshsc7dsue2grfkqw05d9vzcwtqc5wa8dxqr459k2knr89nwejqw742ck",
      "pool_code_id": "31",
      "lp_code_id": "33"
    },
    {
      "pair": "willyn-willyf",
      "assets": [
        "{\"token\":{\"token\":\"terra18qcy2t7tnyshe4zcx0jujkt22lyxtluvdg0pfjlrjp95snasql0shfjqh9\"}}",
        "{\"token\":{\"token\":\"terra175mstg9t3et44qyzlruq38v5y2qkyj78r2708w8l3gtxmfkmn3nqnx9xqg\"}}"
      ],
      "pool_address": "terra1cn26pl8lmm9v5qlvmrxw74cdtfqjagqsyfq4hmwatraye0nvsc2su7tw62",
      "lp_address": "terra182zctypedlngpp79kdyly0006prefmf7cmvf86pcrwrn7rqarrkqaezdyr",
      "pool_code_id": "31",
      "lp_code_id": "33"
    },
    {
      "pair": "willyf-willyf",
      "assets": [
        "{\"token\":{\"token\":\"terra175mstg9t3et44qyzlruq38v5y2qkyj78r2708w8l3gtxmfkmn3nqnx9xqg\"}}",
        "{\"token\":{\"token\":\"terra1r9f8c768dg6kt48fjuxh494m5fm075dcjwm0c9cxmpa37y49xzesqmu6fv\"}}"
      ],
      "pool_address": "terra1qq4q844eevmv9k8an47gq6s04er4sd4wnkhv0s7aftwuc304guuqlwzhpl",
      "lp_address": "terra1prfue6fhreqsu7ry2cuw294kc35u68refsdkq6r5d4m5nm235xjqay0y87",
      "pool_code_id": "31",
      "lp_code_id": "33"
    }
  ]
}
```
