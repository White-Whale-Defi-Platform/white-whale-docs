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
      "code_id": "441",
      "version": "0.9.1",
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
      "code_id": "447",
      "version": "1.2.1",
      "contract_address": "osmo1vuzkc4nzzav7g6t20f2vp0ed4sm3vaqnkpzy7yq3kujxs2g2hawqwnwy5w"
    },
    {
      "wasm": "terraswap_pair.wasm",
      "code_id": "448",
      "version": "1.3.3"
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
      "pool_code_id": "448",
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
      "pool_code_id": "448",
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
      "pool_code_id": "448",
      "lp_code_id": "450"
    }
  ]
}
```