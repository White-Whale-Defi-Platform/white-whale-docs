# Sei (pacific-1)

```json
{
  "contracts": [
    {
      "wasm": "fee_collector.wasm",
      "code_id": "117",
      "version": "1.1.1",
      "contract_address": "sei1kgq4e2469nhdghnyn7xgrzppsxhth772z4dvxrcl60q2gksls8uqy6vl5t"
    },
    {
      "wasm": "fee_distributor.wasm",
      "code_id": "118",
      "version": "0.9.1"
    },
    {
      "wasm": "frontend_helper.wasm",
      "code_id": "119",
      "version": "1.0.0"
    },
    {
      "wasm": "incentive.wasm",
      "code_id": "120",
      "version": "1.0.3"
    },
    {
      "wasm": "incentive_factory.wasm",
      "code_id": "121",
      "version": "1.0.1"
    },
    {
      "wasm": "stableswap_3pool.wasm",
      "code_id": "122",
      "version": "1.2.1"
    },
    {
      "wasm": "terraswap_factory.wasm",
      "code_id": "124",
      "version": "1.2.0",
      "contract_address": "sei1tcx434euh2aszzfsjxqzvjmc4cww54rxvfvv8v7jz353rg779l2st699q0"
    },
    {
      "wasm": "terraswap_pair.wasm",
      "code_id": "125",
      "version": "1.3.1"
    },
    {
      "wasm": "terraswap_router.wasm",
      "code_id": "126",
      "version": "1.1.0",
      "contract_address": "sei1f5utu2sx9f43cxl6c37ur5z57x6n3qmvpzse38hmhz6mspp4krsqccyu80"
    },
    {
      "wasm": "terraswap_token.wasm",
      "code_id": "127",
      "version": "1.0.2"
    },
    {
      "wasm": "vault.wasm",
      "code_id": "129",
      "version": "1.2.3"
    },
    {
      "wasm": "vault_factory.wasm",
      "code_id": "130",
      "version": "1.1.3",
      "contract_address": "sei1xmklc5umaeu52mas5rp7x9u8k7wdw9eqnh64v67ku7vd87cy9gash82279"
    },
    {
      "wasm": "vault_router.wasm",
      "code_id": "131",
      "version": "1.1.5",
      "contract_address": "sei1mtgsxpjw8h8873udcg6l7y5rupp40v63p7jeg7essznucfgjpdzshnhcvc"
    },
    {
      "wasm": "whale_lair.wasm",
      "code_id": "132",
      "version": "0.9.1"
    }
  ],
  "date": "2023-08-16T15:21:23+0000",
  "initial_block_height": "null",
  "final_block_height": "null",
  "chain_id": "pacific-1",
  "deployer_address": "sei1n9x0jnrve7e7t3lcc08qm27uzv59266z87yv5m"
}
```

### Pools on Sei

```json 
{
  "pools": [
    {
      "pair": "uwhale-usei",
      "assets": [
        "{\"token\":{\"native_token\":\"ibc/6ACE79F5ABD607D2075FAD4ABE284CBC5BB6A96C16555FFB901644E9D17411AC\"}}",
        "{\"token\":{\"native_token\":\"usei\"}}"
      ],
      "pool_address": "sei155lc2utpd66unfhyh533yu729ltmrd8eeqw0qq5r7jws9pfc9k0sp65zul",
      "lp_address": "sei1zq2mleg8r9l9sa7x350wtvqety0l5crvv9a6znz634cwdjpec36slquzlx",
      "pool_code_id": "125",
      "lp_code_id": "127"
    }
  ]
}
```

### Vaults on Sei

```json
{
  "vaults": [
    {
      "asset": {
        "native_token": {
          "denom": "usei"
        }
      },
      "vault_address": "sei153ww606x9h6ft7nq5h4fl4jq3n2sx4936m53xtrmag236j8n2rnqv6hgd3",
      "lp_asset": {
        "token": {
          "contract_addr": "sei1j9qyhqf29hgze9p2gdh5uyq44v8yy5cnwf7mdln8ud5sva0khy4syjrwjl"
        }
      },
      "vault_code_id": "129",
      "lp_code_id": "127"
    }
  ]
}
```

# Sei testnet (sei-devnet-1)

```json
{
  "contracts": [
    {
      "wasm": "fee_collector.wasm",
      "code_id": "19",
      "version": "1.0.5",
      "contract_address": "sei12xk7d7lksh6z94vvt4qqur765trqdcn7w86mfak62qjz63zvmhvsl7qf07"
    },
    {
      "wasm": "terraswap_factory.wasm",
      "code_id": "20",
      "version": "1.1.2",
      "contract_address": "sei17q90gwd9279une6fagsxqrak87fmc3gtusv9dglwc0ezcxufrtdsrqwxz7"
    },
    {
      "wasm": "terraswap_pair.wasm",
      "code_id": "21",
      "version": "1.2.0"
    },
    {
      "wasm": "terraswap_token.wasm",
      "code_id": "22",
      "version": "1.0.2"
    },
    {
      "wasm": "terraswap_router.wasm",
      "code_id": "23",
      "version": "1.0.7",
      "contract_address": "sei1lxansfc8vkujy997e3xksd3ugsppv6a9jt32pjtgaxr0zkcnkznqernkea"
    },
    {
      "wasm": "vault_factory.wasm",
      "code_id": "24",
      "version": "1.0.9",
      "contract_address": "sei1v8leqn5fv0hk056hkky8ym8gytuehe962cy4nt2mrg4lyt05p9nspcsapx"
    },
    {
      "wasm": "vault_router.wasm",
      "code_id": "25",
      "version": "1.1.3",
      "contract_address": "sei1s0krs8d405sxmthhngrs4uvjv830ugckayg0evvzpc6gw4lpha2s6e4m5k"
    },
    {
      "wasm": "vault.wasm",
      "code_id": "26",
      "version": "1.2.0"
    }
  ]
}
```

```json
{
  "pools": [
    {
      "pair": "usei-TOKEN",
      "assets": [
        "{\"native_token\":{\"denom\":\"usei\"}}",
        "{\"token\":{\"contract_addr\":\"sei1ntq7vz509nt4fx3yngltgt4svrggsgaept7tzpsmzeh8mek5utwsgdrean\"}}"
      ],
      "pool_address": "sei1leewphkx87lq2yuz8pmxw4yqlenfm25ruahj75p6vhf2cfk7p82qxgp7yk",
      "lp_address": "sei1jqdzmf3dd9zurkyn0t2uj8sp7775n8nuuq2cnrjnlckwfrjhzeuse7ngpa",
      "pool_code_id": "21",
      "lp_code_id": "22"
    }
  ],
  "date": "2022-12-23T18:37:07+0000",
  "chain_id": "sei-devnet-1",
  "pool_factory_addr": "sei17q90gwd9279une6fagsxqrak87fmc3gtusv9dglwc0ezcxufrtdsrqwxz7"
}
```

```json
{
  "vaults": [
    {
      "asset": "usei",
      "vault_address": "sei1xrgwrv62crglmnakhrx3y8zge0rzzsmk5pkc03f6du3ma5jmp5cs8l2hfy",
      "lp_address": "sei1xc3n6fauf3gaug26jh5qtfuv256x6why6tcsfyztwh59gm85j30qsp2pwy",
      "vault_code_id": "26",
      "lp_code_id": "22"
    }
  ],
  "date": "2022-12-23T18:33:13+0000",
  "chain_id": "sei-devnet-1",
  "vault_factory_addr": "sei1v8leqn5fv0hk056hkky8ym8gytuehe962cy4nt2mrg4lyt05p9nspcsapx"
}
```


