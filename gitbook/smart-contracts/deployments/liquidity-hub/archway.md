# Archway (archway-1)

```json
{
  "contracts": [
    {
      "wasm": "fee_collector.wasm",
      "code_id": "558",
      "version": " 1.1.6",
      "contract_address": "archway1zk6y3a4sqk8w8h0wtv04px5x4h9vnmcassxlkvl55hj29v23ugjs8e90gk"
    },
    {
      "wasm": "fee_distributor.wasm",
      "code_id": "559",
      "version": " 0.9.4",
      "contract_address": "archway19sd5pzm9davt53735nc020ewemtw8dq5znp4sdtynlwmveqy3jfqltvnws"
    },
    {
      "wasm": "frontend_helper.wasm",
      "code_id": "560",
      "version": " 1.0.1",
      "contract_address": "archway1yuxk5envmnvn8c36gakhzd650jsfjpj5pf5vm3wa0uf4ltj3r6hqzdp8dg"
    },
    {
      "wasm": "incentive.wasm",
      "code_id": "561",
      "version": " 1.0.7"
    },
    {
      "wasm": "incentive_factory.wasm",
      "code_id": "562",
      "version": " 1.0.2",
      "contract_address": "archway1wc6wu89rl42fhyru4gff7jwy5cf3m0qz22yn7szvt8ac3m8al3rsp68vug"
    },
    {
      "wasm": "stableswap_3pool.wasm",
      "code_id": "563",
      "version": " 1.2.5"
    },
    {
      "wasm": "terraswap_factory.wasm",
      "code_id": "564",
      "version": " 1.2.4",
      "contract_address": "archway1tfkye8su787r5xm3ncp5klve6lqwwc74pt6w9g07lw2550stjqcswjdtsl"
    },
    {
      "wasm": "terraswap_pair.wasm",
      "code_id": "565",
      "version": " 1.3.7"
    },
    {
      "wasm": "terraswap_router.wasm",
      "code_id": "566",
      "version": " 1.1.2",
      "contract_address": "archway1y0eyqu78q8zz93swaplvg90la0qkk0fueht3yxu6huc96yktrmcqntwe67"
    },
    {
      "wasm": "terraswap_token.wasm",
      "code_id": "567",
      "version": " 1.0.3"
    },
    {
      "wasm": "vault.wasm",
      "code_id": "568",
      "version": " 1.2.7"
    },
    {
      "wasm": "vault_factory.wasm",
      "code_id": "569",
      "version": " 1.1.4",
      "contract_address": "archway132netq0uv85fqfq9dln93qy3gpukhzytk344u2a6phukmfa02c6qud97lr"
    },
    {
      "wasm": "vault_router.wasm",
      "code_id": "570",
      "version": " 1.1.7",
      "contract_address": "archway1xkvfz9t6gn68k9n3nqq6k5eqz07sgh0hrfdskemq5ucg9k8ltznqspykh7"
    },
    {
      "wasm": "whale_lair.wasm",
      "code_id": "571",
      "version": " 0.9.2",
      "contract_address": "archway1a2hawz66n3nuh8964t0kw6yvcvqww2rnucsvacga2g4360nxs2tsyzftg8"
    }
  ],
  "date": "2024-07-29T15:29:34+0000",
  "initial_block_height": "null",
  "final_block_height": "5704684",
  "chain_id": "archway-1",
  "deployer_address": "archway1v767q4apajgksqlg5ejdakn8auszecjefm4h3r"
}
```

```json
{
  "chain": "archway-1",
  "pool_factory_addr": "archway1tfkye8su787r5xm3ncp5klve6lqwwc74pt6w9g07lw2550stjqcswjdtsl",
  "pools": [
    {
      "pair": "boneARCH-aarch",
      "assets": [
        {
          "token": {
            "contract_addr": "archway12yurzx8zynv3ck7uh4tucre48tqsm4fac4hfk9p3l24qs2cn08dqr684cg"
          }
        },
        {
          "native_token": {
            "denom": "aarch"
          }
        }
      ],
      "pool_address": "archway1jq9y6ty3cckpp8nsq7xwu54ttudvmdsmj87y0f3zmlzm5qll75ssr7pgkj",
      "lp_asset": {
        "token": {
          "contract_addr": "archway18zjxz24skc48vs3vya9rtky8qt2rgzmv85cz24t5trj4jngyk84qx3rk8s"
        }
      },
      "incentive_contract": "null",
      "pool_code_id": "565",
      "lp_code_id": "567"
    },
    {
      "pair": "uwhale-aarch",
      "assets": [
        {
          "native_token": {
            "denom": "ibc/3F882513A0CCD1C4110ACB7C6C761AC7B48974C9D2D439CD6F652F9B44362518"
          }
        },
        {
          "native_token": {
            "denom": "aarch"
          }
        }
      ],
      "pool_address": "archway1vkqtkdflv5ueyen92c4v9q0e2vgkvyz4wgpdjns3yjuez0pmcnxqp76zpu",
      "lp_asset": {
        "token": {
          "contract_addr": "archway17dgwtpfg5n6fytmc5m3qkpp3caxms4crvvz6sam0exa0wllqnyjq4t8w39"
        }
      },
      "incentive_contract": "null",
      "pool_code_id": "565",
      "lp_code_id": "567"
    }
  ]
}
```