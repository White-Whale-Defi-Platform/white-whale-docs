# Migaloo (migaloo-1)

```json
{
  "contracts": [
    {
      "wasm": "fee_collector.wasm",
      "code_id": "24",
      "version": "1.1.1",
      "contract_address": "migaloo14dcwvg4zplrc28g5q3802n2mmnp3fsp2yh7mn7gkxssnrjqp4ycq76wy6h"
    },
    {
      "wasm": "fee_distributor.wasm",
      "code_id": "25",
      "version": "0.9.1",
      "contract_address": "migaloo13e3ywqudfz92pq2sxwuwf35rdtp3hvz7xu0danyk38dchevywraswfgnqx"
    },
    {
      "wasm": "frontend_helper.wasm",
      "code_id": "26",
      "version": "1.0.0"
    },
    {
      "wasm": "incentive.wasm",
      "code_id": "27",
      "version": "1.0.1"
    },
    {
      "wasm": "incentive_factory.wasm",
      "code_id": "28",
      "version": "1.0.0"
    },
    {
      "wasm": "stableswap_3pool.wasm",
      "code_id": "29",
      "version": "1.2.1"
    },
    {
      "wasm": "terraswap_factory.wasm",
      "code_id": "30",
      "version": "1.2.0",
      "contract_address": "migaloo1z89funaazn4ka8vrmmw4q27csdykz63hep4ay8q2dmlspc6wtdgq92u369"
    },
    {
      "wasm": "terraswap_pair.wasm",
      "code_id": "31",
      "version": "1.3.1"
    },
    {
      "wasm": "terraswap_router.wasm",
      "code_id": "32",
      "version": "1.1.0",
      "contract_address": "migaloo1tma28exp38q92c69r8uujhphxy95xa4awq2cudqqg3nhzkhnrg5s4r60en"
    },
    {
      "wasm": "terraswap_token.wasm",
      "code_id": "33",
      "version": "1.0.2"
    },
    {
      "wasm": "vault_factory.wasm",
      "code_id": "46",
      "version": "1.1.3",
      "contract_address": "migaloo1g2xwx805epc897rwyrykskjque07yxfmc4qq2p4ef5dwd6znl30qkgw8w7"
    },
    {
      "wasm": "vault.wasm",
      "code_id": "44",
      "version": "1.2.3"
    },
    {
      "wasm": "vault_router.wasm",
      "code_id": "45",
      "version": "1.1.5",
      "contract_address": "migaloo19pze0n07guzj6yla2708q2feh38q9n8gxmkk8fjnuprfh6y9ngjqs90hcy"
    },
    {
      "wasm": "whale_lair.wasm",
      "code_id": "37",
      "version": "0.9.1",
      "contract_address": "migaloo1692nylpkryu7q00eukt93egtqu657z33nf0tedp0ps6htm8aty6qjdlpvh"
    }
  ]
}
```

### Pools on Migaloo 

```json 
{
  "pools": [
    {
      "pair": "boneWhale-uwhale",
      "assets": [
        "{\"token\":{\"native_token\":\"factory/migaloo1mf6ptkssddfmxvhdx0ech0k03ktp6kf9yk59renau2gvht3nq2gqdhts4u/boneWhale\"}}",
        "{\"token\":{\"native_token\":\"uwhale\"}}"
      ],
      "pool_address": "migaloo1dg5jrt89nddtymjx5pzrvdvdt0m4zl3l2l3ytunl6a0kqd7k8hss594wy6",
      "lp_address": "factory/migaloo1dg5jrt89nddtymjx5pzrvdvdt0m4zl3l2l3ytunl6a0kqd7k8hss594wy6/uLP",
      "pool_code_id": "31",
      "lp_code_id": "33"
    },
    {
      "pair": "ampWHALE-uwhale",
      "assets": [
        "{\"token\":{\"native_token\":\"factory/migaloo1436kxs0w2es6xlqpp9rd35e3d0cjnw4sv8j3a7483sgks29jqwgshqdky4/ampWHALE\"}}",
        "{\"token\":{\"native_token\":\"uwhale\"}}"
      ],
      "pool_address": "migaloo1ull9s4el2pmkdevdgrjt6pwa4e5xhkda40w84kghftnlxg4h3knqpm5u3n",
      "lp_address": "factory/migaloo1ull9s4el2pmkdevdgrjt6pwa4e5xhkda40w84kghftnlxg4h3knqpm5u3n/uLP",
      "pool_code_id": "31",
      "lp_code_id": "33"
    },
    {
      "pair": "ASH-uwhale",
      "assets": [
        "{\"token\":{\"native_token\":\"factory/migaloo1erul6xyq0gk6ws98ncj7lnq9l4jn4gnnu9we73gdz78yyl2lr7qqrvcgup/ash\"}}",
        "{\"token\":{\"native_token\":\"uwhale\"}}"
      ],
      "pool_address": "migaloo1u4npx7xvprwanpru7utv8haq99rtfmdzzw6p3hpfc38n7zmzm42q8ydga3",
      "lp_address": "factory/migaloo1u4npx7xvprwanpru7utv8haq99rtfmdzzw6p3hpfc38n7zmzm42q8ydga3/uLP",
      "pool_code_id": "31",
      "lp_code_id": "33"
    }
  ]
}
```

### Vaults on Migaloo
```json
{
  "vaults": [
    {
      "asset": {
        "native_token": {
          "denom": "uwhale"
        }
      },
      "vault_address": "migaloo16ku76pxpt2uhsvj2aemrehgz69aru5d76a0pqk4fpj8s2wt3lnhqtnvghe",
      "lp_asset": {
        "native_token": {
          "denom": "factory/migaloo16ku76pxpt2uhsvj2aemrehgz69aru5d76a0pqk4fpj8s2wt3lnhqtnvghe/uLP"
        }
      },
      "vault_code_id": "44",
      "lp_code_id": "33"
    }
  ],
  "date": "2023-07-04T13:24:26+0000",
  "chain_id": "migaloo-1",
  "vault_factory_addr": "migaloo1g2xwx805epc897rwyrykskjque07yxfmc4qq2p4ef5dwd6znl30qkgw8w7",
  "vault_router_addr": "migaloo19pze0n07guzj6yla2708q2feh38q9n8gxmkk8fjnuprfh6y9ngjqs90hcy"
}
```