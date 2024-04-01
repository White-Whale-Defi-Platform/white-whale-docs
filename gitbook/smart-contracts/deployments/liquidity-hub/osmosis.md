# Osmosis (osmosis-1)

```json
{
  "contracts": [
    {
      "wasm": "fee_collector.wasm",
      "code_id": "440",
      "version": "1.1.4",
      "contract_address": "osmo1q95ewh2ymqnj8n5rt80myr4yf7srqd0kqmjqrdxf9a2etl5gnavq5hehr3"
    },
    {
      "wasm": "fee_distributor.wasm",
      "code_id": "473",
      "version": "0.9.2",
      "contract_address": "osmo1ec7fqky6cq9xds6hq0e46f25ldnkkvjjkml7644y8la59ucqmtfsyyhh75"
    },
    {
      "wasm": "frontend_helper.wasm",
      "code_id": "442",
      "version": "1.0.0",
      "contract_address": "osmo14fxftxez7wt8hxw9prnzmpu4n5h0vf6vgjx0t4pq2q98gdnra5hsr6kkql"
    },
    {
      "wasm": "incentive.wasm",
      "code_id": "443",
      "version": "1.0.6"
    },
    {
      "wasm": "incentive_factory.wasm",
      "code_id": "444",
      "version": "1.0.1",
      "contract_address": "osmo1qw870ecwrxh62kgn3alur65juhesu22x63x9s6ss8wukdxpfuvaqr4jncv"
    },
    {
      "wasm": "stableswap_3pool.wasm",
      "code_id": "446",
      "version": "1.2.2"
    },
    {
      "wasm": "terraswap_factory.wasm",
      "code_id": "506",
      "version": "1.2.3",
      "contract_address": "osmo1vuzkc4nzzav7g6t20f2vp0ed4sm3vaqnkpzy7yq3kujxs2g2hawqwnwy5w"
    },
    {
      "wasm": "terraswap_pair.wasm",
      "code_id": "502",
      "version": "1.3.5"
    },
    {
      "wasm": "terraswap_router.wasm",
      "code_id": "449",
      "version": "1.1.1",
      "contract_address": "osmo1l3chahmh0ettepept8hpmhgg8hssshf8ymhn53fw65dzxckrl6yq40syqq"
    },
    {
      "wasm": "terraswap_token.wasm",
      "code_id": "450",
      "version": "1.0.2"
    },
    {
      "wasm": "vault_factory.wasm",
      "code_id": "451",
      "version": "1.1.3",
      "contract_address": "osmo1c2zsgzl2cjua4e7f0yxkfy48n7ezhspv7htahdrhsxuqhgy97sas4lscwq"
    },
    {
      "wasm": "vault.wasm",
      "code_id": "452",
      "version": "1.2.6"
    },
    {
      "wasm": "vault_router.wasm",
      "code_id": "453",
      "version": "1.1.6",
      "contract_address": "osmo1ldkya0zakj380tlkd7dry0wj689t0r4x0kyxf6qn4pvvaat0l9tqsly68j"
    },
    {
      "wasm": "whale_lair.wasm",
      "code_id": "439",
      "version": "0.9.1",
      "contract_address": "osmo1mfqvxmv2gx62hglaegdv3useqjj44kxrl69nlt4tkysy9dx8g25sq40kez"
    }
  ],
  "date": "2024-01-23T15:01:19+0000",
  "chain_id": "osmosis-1",
  "deployer_address": "osmo1v767q4apajgksqlg5ejdakn8auszecje5t6rdx"
}
```

```json
{
  "chain": "osmosis-1",
  "pool_factory_addr": "osmo1vuzkc4nzzav7g6t20f2vp0ed4sm3vaqnkpzy7yq3kujxs2g2hawqwnwy5w",
  "pools": [
    {
      "pair": "LAB-uosmo",
      "assets": [
        {
          "native_token": {
            "denom": "factory/osmo17fel472lgzs87ekt9dvk0zqyh5gl80sqp4sk4n/LAB"
          }
        },
        {
          "native_token": {
            "denom": "uosmo"
          }
        }
      ],
      "pool_address": "osmo12zk0xmacanpz9huy8huth2wee98smf9kktg4lltu9zrk3x9w58aq7k64cz",
      "lp_asset": {
        "native_token": {
          "denom": "factory/osmo12zk0xmacanpz9huy8huth2wee98smf9kktg4lltu9zrk3x9w58aq7k64cz/uLP"
        }
      },
      "incentive_contract": "osmo1ux4t64n28drgq8xcv42lswfjeqfn3syzutjs80t3c97al7caan4s8h5nsn",
      "pool_code_id": "502",
      "lp_code_id": "450"
    },
    {
      "pair": "ampOSMO-uosmo",
      "assets": [
        {
          "native_token": {
            "denom": "factory/osmo1dv8wz09tckslr2wy5z86r46dxvegylhpt97r9yd6qc3kyc6tv42qa89dr9/ampOSMO"
          }
        },
        {
          "native_token": {
            "denom": "uosmo"
          }
        }
      ],
      "pool_address": "osmo1692tluwzzmnx56tm5v7r0n8v5fg32nrd9nuukp9jz458ap7wmcls9cz20m",
      "lp_asset": {
        "native_token": {
          "denom": "factory/osmo1692tluwzzmnx56tm5v7r0n8v5fg32nrd9nuukp9jz458ap7wmcls9cz20m/uLP"
        }
      },
      "incentive_contract": "osmo1u5vvxk38gpkt3dlfrsq7s47ugjg6ar8zswyz52379jxdswef8s6qelq0tx",
      "pool_code_id": "502",
      "lp_code_id": "450"
    },
    {
      "pair": "sail-uwhale",
      "assets": [
        {
          "native_token": {
            "denom": "factory/osmo1rckme96ptawr4zwexxj5g5gej9s2dmud8r2t9j0k0prn5mch5g4snzzwjv/sail"
          }
        },
        {
          "native_token": {
            "denom": "ibc/EDD6F0D66BCD49C1084FB2C35353B4ACD7B9191117CE63671B61320548F7C89D"
          }
        }
      ],
      "pool_address": "osmo1w8e2wyzhrg3y5ghe9yg0xn0u7548e627zs7xahfvn5l63ry2x8zstaraxs",
      "lp_asset": {
        "native_token": {
          "denom": "factory/osmo1w8e2wyzhrg3y5ghe9yg0xn0u7548e627zs7xahfvn5l63ry2x8zstaraxs/uLP"
        }
      },
      "incentive_contract": "osmo1jszerakl59dafwkxek2ue28wpd6gec6d7gj6xtrqp2ettpv5sqcq4fu6lx",
      "pool_code_id": "502",
      "lp_code_id": "450"
    },
    {
      "pair": "boneOsmo-uosmo",
      "assets": [
        {
          "native_token": {
            "denom": "factory/osmo1s3l0lcqc7tu0vpj6wdjz9wqpxv8nk6eraevje4fuwkyjnwuy82qsx3lduv/boneOsmo"
          }
        },
        {
          "native_token": {
            "denom": "uosmo"
          }
        }
      ],
      "pool_address": "osmo166yrd7anjg3h7epjsjghlf2uu403phjflk4gygmlelykwlustwysxvgv4c",
      "lp_asset": {
        "native_token": {
          "denom": "factory/osmo166yrd7anjg3h7epjsjghlf2uu403phjflk4gygmlelykwlustwysxvgv4c/uLP"
        }
      },
      "incentive_contract": "osmo1fzmaeuptmzv2l5la7trmv7ez6uhsr3tde0l2vqm4sazcfg7jd78slvhzek",
      "pool_code_id": "502",
      "lp_code_id": "450"
    },
    {
      "pair": "uwhale-wbtc",
      "assets": [
        {
          "native_token": {
            "denom": "ibc/EDD6F0D66BCD49C1084FB2C35353B4ACD7B9191117CE63671B61320548F7C89D"
          }
        },
        {
          "native_token": {
            "denom": "factory/osmo1z0qrq605sjgcqpylfl4aa6s90x738j7m58wyatt0tdzflg2ha26q67k743/wbtc"
          }
        }
      ],
      "pool_address": "osmo1ycg9k5dj3pd0szt4f7ladzam8u6rvs472z6ckx4p82u00cetdnzqxw4vwm",
      "lp_asset": {
        "native_token": {
          "denom": "factory/osmo1ycg9k5dj3pd0szt4f7ladzam8u6rvs472z6ckx4p82u00cetdnzqxw4vwm/uLP"
        }
      },
      "incentive_contract": "osmo1a5zsvtgkzyufaetavqzqksk2zjl2dm3up5erpfuapd4m429qja3qxhdwhr",
      "pool_code_id": "502",
      "lp_code_id": "450"
    },
    {
      "pair": "shark-uosmo",
      "assets": [
        {
          "native_token": {
            "denom": "ibc/64D56DF9EC69BE554F49EBCE0199611062FF1137EF105E2F645C1997344F3834"
          }
        },
        {
          "native_token": {
            "denom": "uosmo"
          }
        }
      ],
      "pool_address": "osmo1nkjck7774semslqk6f8n058m4gwcw5spqtza0hrjf8e2kshn4x6svjrc0m",
      "lp_asset": {
        "native_token": {
          "denom": "factory/osmo1nkjck7774semslqk6f8n058m4gwcw5spqtza0hrjf8e2kshn4x6svjrc0m/uLP"
        }
      },
      "incentive_contract": "osmo1c9gunhvzpffr3sms0f97qtwefjw9jzlntp9w6873nkhjflewn36srjl0sk",
      "pool_code_id": "502",
      "lp_code_id": "450"
    },
    {
      "pair": "ROAR-uosmo",
      "assets": [
        {
          "native_token": {
            "denom": "ibc/98BCD43F190C6960D0005BC46BB765C827403A361C9C03C2FF694150A30284B0"
          }
        },
        {
          "native_token": {
            "denom": "uosmo"
          }
        }
      ],
      "pool_address": "osmo13c5k2wxq3cx5xanqnqjdyrwvgw0qs8ea7k8c9dzdddlthg55suhqpvjnq7",
      "lp_asset": {
        "native_token": {
          "denom": "factory/osmo13c5k2wxq3cx5xanqnqjdyrwvgw0qs8ea7k8c9dzdddlthg55suhqpvjnq7/uLP"
        }
      },
      "incentive_contract": "osmo17w06dzncqlsz9m2assacrzmrqvmlc7y79updfzd0834q2jty9w6qwdvg9q",
      "pool_code_id": "502",
      "lp_code_id": "450"
    },
    {
      "pair": "uwhale-uosmo",
      "assets": [
        {
          "native_token": {
            "denom": "ibc/EDD6F0D66BCD49C1084FB2C35353B4ACD7B9191117CE63671B61320548F7C89D"
          }
        },
        {
          "native_token": {
            "denom": "uosmo"
          }
        }
      ],
      "pool_address": "osmo18r35luyyfqp7jter6jc93vzhft5zjgvsgt2tgx76qez2lpjpzfxqwx4ynk",
      "lp_asset": {
        "native_token": {
          "denom": "factory/osmo18r35luyyfqp7jter6jc93vzhft5zjgvsgt2tgx76qez2lpjpzfxqwx4ynk/uLP"
        }
      },
      "incentive_contract": "osmo1xrs9qtmvvv69xh34r9gtd0w0v8y99n8ywn89saryd923e5aay4aqev2zxn",
      "pool_code_id": "502",
      "lp_code_id": "450"
    }
  ]
}
```

```json
{
  "pool_interfaces": [
    {
      "pair": "ampOSMO-uosmo",
      "pool_address": "osmo1692tluwzzmnx56tm5v7r0n8v5fg32nrd9nuukp9jz458ap7wmcls9cz20m",
      "interface": "osmo14zdnsp658g6tf7s5863ygeuj9ce5g00szud3tup6sqpwhuxmdwusc2eq7v",
      "pool_id": "1461", 
      "code_id": "641"
    },
    {
      "pair": "sail-uwhale",
      "pool_address": "osmo1w8e2wyzhrg3y5ghe9yg0xn0u7548e627zs7xahfvn5l63ry2x8zstaraxs",
      "interface": "osmo1suf8z9ypyv3kk4egr7plde00dfetw7rcm4m9ecut7x3720z8l46q23663a",
      "pool_id": "1462", 
      "code_id": "641"
    },
    {
      "pair": "uwhale-uosmo",
      "pool_address": "osmo18r35luyyfqp7jter6jc93vzhft5zjgvsgt2tgx76qez2lpjpzfxqwx4ynk",
      "interface": "osmo184utpa0q2x5d79ctpewwvskea50x7tr3fkgj7ge2r0uavhqexququsj3xq",
      "pool_id": "1463", 
      "code_id": "641"
    },
    {
      "pair": "ampOSMO-uosmo (duplicated)",
      "pool_address": "osmo1692tluwzzmnx56tm5v7r0n8v5fg32nrd9nuukp9jz458ap7wmcls9cz20m",
      "interface": "osmo1g883rt8ytjlhawxey39m3w90nyaxg2vfmlfh6jvnv9ec3py2hgxq9qdz53",
      "pool_id": "1514",
      "code_id": "641"
    },
    {
      "pair": "ROAR-uosmo",
      "pool_address": "osmo13c5k2wxq3cx5xanqnqjdyrwvgw0qs8ea7k8c9dzdddlthg55suhqpvjnq7",
      "interface": "osmo1hnlw8ajwhgg7rsyke2t34uknp4jjcmm23zeygsu7n8cwjqnt2jsqju3nz4",
      "pool_id": "1575",
      "code_id": "641"
    },
    {
      "pair": "shark-uosmo",
      "pool_address": "osmo1nkjck7774semslqk6f8n058m4gwcw5spqtza0hrjf8e2kshn4x6svjrc0m",
      "interface": "osmo1w2sdnptx8jt4vuugcauv6tj3c2syjay5rx2mxalngn7m2cywllsq6xt64k",
      "pool_id": "1584", 
      "code_id": "641"
    },
    {
      "pair": "LAB-uosmo",
      "pool_address": "osmo12zk0xmacanpz9huy8huth2wee98smf9kktg4lltu9zrk3x9w58aq7k64cz",
      "interface": "osmo1javcdeqdnlujsrl4kduwfcs2cw5hd4jz9vh2wdpqyz6kp2tn8e9qt0rz8g",
      "pool_id": "1642",
      "code_id": "641"
    },
    {
      "pair": "boneOsmo-uosmo",
      "pool_address": "osmo166yrd7anjg3h7epjsjghlf2uu403phjflk4gygmlelykwlustwysxvgv4c",
      "interface": "osmo1ku2e3x8ku4drw07gvp2a4ncnf3w2rshdj5fs69w5wu2the3lvnuqzf6cml",
      "pool_id": "1643",
      "code_id": "641"
    },
    {
      "pair": "uwhale-wbtc",
      "pool_address": "osmo1ycg9k5dj3pd0szt4f7ladzam8u6rvs472z6ckx4p82u00cetdnzqxw4vwm",
      "interface": "osmo1xkxyx8s4ghzkzwt52ela4v4gp2fj0n4yewall0f24xnzgm8hyqaqlurefp",
      "pool_id": "1644",
      "code_id": "641"
    }
  ]
}
```
