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
      "version": "1.0.0",
      "contract_address": "migaloo1yk896ldldnfd4y4f3xgxwnpapmyezgdqw5czp4zz6nnvetl70lkq42mp8u"
    },
    {
      "wasm": "incentive.wasm",
      "code_id": "61",
      "version": "1.0.2"
    },
    {
      "wasm": "incentive_factory.wasm",
      "code_id": "28",
      "version": "1.0.0",
      "contract_address": "migaloo1rqfr752hn6auzm3vzzyr2pd8rt6fapf208vm8qfpejstt69uxfwqcdrdq3"
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
      "pair": "ampWHALE-arbWHALE",
      "assets": [
        {
          "native_token": {
            "denom": "factory/migaloo1436kxs0w2es6xlqpp9rd35e3d0cjnw4sv8j3a7483sgks29jqwgshqdky4/ampWHALE"
          }
        },
        {
          "native_token": {
            "denom": "factory/migaloo1ey4sn2mkmhew4pdrzk90l9acluvas25qlhuvsfgssw42ugz8yjlqx92j9l/arbWHALE"
          }
        }
      ],
      "pool_address": "migaloo12z46dq46hprpyv8j4k7xtqk8gdx7leqzgan2pjpdaktx4ukj53lqar6tsf",
      "lp_asset": {
        "native_token": {
          "denom": "factory/migaloo12z46dq46hprpyv8j4k7xtqk8gdx7leqzgan2pjpdaktx4ukj53lqar6tsf/uLP"
        }
      },
      "incentive_contract": "null",
      "pool_code_id": "31",
      "lp_code_id": "33"
    },
    {
      "pair": "ampWHALE-uwhale",
      "assets": [
        {
          "native_token": {
            "denom": "factory/migaloo1436kxs0w2es6xlqpp9rd35e3d0cjnw4sv8j3a7483sgks29jqwgshqdky4/ampWHALE"
          }
        },
        {
          "native_token": {
            "denom": "uwhale"
          }
        }
      ],
      "pool_address": "migaloo1ull9s4el2pmkdevdgrjt6pwa4e5xhkda40w84kghftnlxg4h3knqpm5u3n",
      "lp_asset": {
        "native_token": {
          "denom": "factory/migaloo1ull9s4el2pmkdevdgrjt6pwa4e5xhkda40w84kghftnlxg4h3knqpm5u3n/uLP"
        }
      },
      "incentive_contract": "migaloo1qkuqpqx98zwp8pvh3a2tl536l7cmhcw2qlp0fj35tz9pt80864zsvff3l7",
      "pool_code_id": "31",
      "lp_code_id": "33"
    },
    {
      "pair": "urac-uwhale",
      "assets": [
        {
          "native_token": {
            "denom": "factory/migaloo1eqntnl6tzcj9h86psg4y4h6hh05g2h9nj8e09l/urac"
          }
        },
        {
          "native_token": {
            "denom": "uwhale"
          }
        }
      ],
      "pool_address": "migaloo1crsvm4qddplxhag29nd2zyw6k6jzh06hlcctya4ynfvuhhu3yt4q0pn4t3",
      "lp_asset": {
        "native_token": {
          "denom": "factory/migaloo1crsvm4qddplxhag29nd2zyw6k6jzh06hlcctya4ynfvuhhu3yt4q0pn4t3/uLP"
        }
      },
      "incentive_contract": "migaloo1twdet2vswqnf8tpg3wh269s686xejpad3hrtdc8l43yuvs8whfps8tttne",
      "pool_code_id": "31",
      "lp_code_id": "33"
    },
    {
      "pair": "ash-uwhale",
      "assets": [
        {
          "native_token": {
            "denom": "factory/migaloo1erul6xyq0gk6ws98ncj7lnq9l4jn4gnnu9we73gdz78yyl2lr7qqrvcgup/ash"
          }
        },
        {
          "native_token": {
            "denom": "uwhale"
          }
        }
      ],
      "pool_address": "migaloo1u4npx7xvprwanpru7utv8haq99rtfmdzzw6p3hpfc38n7zmzm42q8ydga3",
      "lp_asset": {
        "native_token": {
          "denom": "factory/migaloo1u4npx7xvprwanpru7utv8haq99rtfmdzzw6p3hpfc38n7zmzm42q8ydga3/uLP"
        }
      },
      "incentive_contract": "migaloo180qwhupk30f68ygp7lz4vwcppsfkjr9n4ytsz03c04fsku0hrccspalpxt",
      "pool_code_id": "31",
      "lp_code_id": "33"
    },
    {
      "pair": "boneWhale-uwhale",
      "assets": [
        {
          "native_token": {
            "denom": "factory/migaloo1mf6ptkssddfmxvhdx0ech0k03ktp6kf9yk59renau2gvht3nq2gqdhts4u/boneWhale"
          }
        },
        {
          "native_token": {
            "denom": "uwhale"
          }
        }
      ],
      "pool_address": "migaloo1dg5jrt89nddtymjx5pzrvdvdt0m4zl3l2l3ytunl6a0kqd7k8hss594wy6",
      "lp_asset": {
        "native_token": {
          "denom": "factory/migaloo1dg5jrt89nddtymjx5pzrvdvdt0m4zl3l2l3ytunl6a0kqd7k8hss594wy6/uLP"
        }
      },
      "incentive_contract": "migaloo1ns355ukd2aww4wrpwxp9cdkmx6rsc4gkwea58ng92pfwkrtpltlssyeghn",
      "pool_code_id": "31",
      "lp_code_id": "33"
    },
    {
      "pair": "ampMNTA-uwhale",
      "assets": [
        {
          "native_token": {
            "denom": "ibc/0102CC6E28D29F57444C645C86AE2F4E8789C3A85445A3B185E51F0A23862E87"
          }
        },
        {
          "native_token": {
            "denom": "uwhale"
          }
        }
      ],
      "pool_address": "migaloo1wxnc6vd83pxudrfjf0ql8v73x3xute65fefxm7x5qxsehy5g0pzskclu2r",
      "lp_asset": {
        "native_token": {
          "denom": "factory/migaloo1wxnc6vd83pxudrfjf0ql8v73x3xute65fefxm7x5qxsehy5g0pzskclu2r/uLP"
        }
      },
      "incentive_contract": "migaloo1nplqhfd64jru7cj5ng2f3kh9g70gr3l3yut7wsu85z4q599hag5s0enjy8",
      "pool_code_id": "31",
      "lp_code_id": "33"
    },
    {
      "pair": "uwhale-uusdc",
      "assets": [
        {
          "native_token": {
            "denom": "uwhale"
          }
        },
        {
          "native_token": {
            "denom": "ibc/80E8F826480B995AE28C1EE86106C1BE2034FF1966579D29951CF61885458040"
          }
        }
      ],
      "pool_address": "migaloo1nha6qlam4p92cf9j64qv9he40xyf3akl2m9w5dukftmf2ryrxz5qy650zh",
      "lp_asset": {
        "native_token": {
          "denom": "factory/migaloo1nha6qlam4p92cf9j64qv9he40xyf3akl2m9w5dukftmf2ryrxz5qy650zh/uLP"
        }
      },
      "incentive_contract": "null",
      "pool_code_id": "31",
      "lp_code_id": "33"
    },
    {
      "pair": "uwhale-uusdc",
      "assets": [
        {
          "native_token": {
            "denom": "uwhale"
          }
        },
        {
          "native_token": {
            "denom": "ibc/BC5C0BAFD19A5E4133FDA0F3E04AE1FBEE75A4A226554B2CBB021089FF2E1F8A"
          }
        }
      ],
      "pool_address": "migaloo1xv4ql6t6r8zawlqn2tyxqsrvjpmjfm6kvdfvytaueqe3qvcwyr7shtx0hj",
      "lp_asset": {
        "native_token": {
          "denom": "factory/migaloo1xv4ql6t6r8zawlqn2tyxqsrvjpmjfm6kvdfvytaueqe3qvcwyr7shtx0hj/uLP"
        }
      },
      "incentive_contract": "migaloo18t2kn6j5l0dw3lfsnllclum9j9ktr63mrlpqjlkeugj8msj9xasqks7m5p",
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


# Migaloo testnet (narwhal-1)

```json
{
  "contracts": [
    {
      "wasm": "fee_collector.wasm",
      "code_id": "209",
      "version": "1.1.4",
      "contract_address": "migaloo1e3tccaxd3l7g3kq4z7ttae646luzh68sszdx7p8u9nqfxzf2585qt9mur5"
    },
    {
      "wasm": "fee_distributor.wasm",
      "code_id": "210",
      "version": "0.9.1",
      "contract_address": "migaloo19k5skr08s9ztwtfyrpl7kx777stuusjyy3ftqlag5aezfg8guhyseykyg6"
    },
    {
      "wasm": "frontend_helper.wasm",
      "code_id": "211",
      "version": "1.0.0",
      "contract_address": "migaloo18t2l4gasku8gj658ag94h0rdr6yxalxxysm3adnkykmasguafkkqrqyh37"
    },
    {
      "wasm": "incentive.wasm",
      "code_id": "212",
      "version": "1.0.6"
    },
    {
      "wasm": "incentive_factory.wasm",
      "code_id": "213",
      "version": "1.0.1",
      "contract_address": "migaloo1404cq7mmpky48yct7u0fskx68fka7w8juuv2yl5cpn38vylkh9xs3t0y53"
    },
    {
      "wasm": "stableswap_3pool.wasm",
      "code_id": "214",
      "version": "1.2.2"
    },
    {
      "wasm": "terraswap_factory.wasm",
      "code_id": "215",
      "version": "1.2.0",
      "contract_address": "migaloo13zayyqtuam0wq5e057m6cq3ye8gw2f8t8svm9xlcc0m200x9wp5qx54gm5"
    },
    {
      "wasm": "terraswap_pair.wasm",
      "code_id": "216",
      "version": "1.3.3"
    },
    {
      "wasm": "terraswap_router.wasm",
      "code_id": "217",
      "version": "1.1.1",
      "contract_address": "migaloo13ur49a5c7ej6vy2t3wj6h9vjp4ketvc6c9e7m2h0zd6tcydxzqtqqkkwdp"
    },
    {
      "wasm": "terraswap_token.wasm",
      "code_id": "218",
      "version": "1.0.2"
    },
    {
      "wasm": "vault.wasm",
      "code_id": "219",
      "version": "1.2.6"
    },
    {
      "wasm": "vault_factory.wasm",
      "code_id": "220",
      "version": "1.1.3",
      "contract_address": "migaloo1zj4h6jvsv07rw6x74jax028leywdekfhahzm0544qevlwvpzc0gs2yt96t"
    },
    {
      "wasm": "vault_router.wasm",
      "code_id": "221",
      "version": "1.1.6",
      "contract_address": "migaloo1c7c8jh4nfkp52pdhl8r2rjvs8fkhlzmv3ku9v7d9ygrewpkkvfxsq5tgqt"
    },
    {
      "wasm": "whale_lair.wasm",
      "code_id": "222",
      "version": "0.9.1",
      "contract_address": "migaloo1zmudfkljvltcrh5h8n2sppm0rj7qew02w7xsupr3levdzd9mhspqecxc5a"
    }
  ],
  "date": "2023-12-12T13:29:04+0000",
  "initial_block_height": "null",
  "final_block_height": "4916900",
  "chain_id": "narwhal-1",
  "deployer_address": "migaloo1ut7pkdz4hgy689v98vf3dj650frynyaj285zge"
}
```

### Pools 

```json
{
  "pools": [
    {
      "pair": "uwhale-willyk",
      "assets": [
        "{\"token\":{\"native_token\":\"uwhale\"}}",
        "{\"token\":{\"token\":\"migaloo1se4zqd573xe5afhf6gg06f8jsrhts77tha8nsw8u4qyqdfz0l2jsyccl6x\"}}"
      ],
      "pool_address": "migaloo13kua4jtwkfcx3ngz829axpvrjcns5za3qclvprfqwldk8ucfrsusp3nudu",
      "lp_address": "migaloo1x50n9q55wkthlphtr8evplwkjx0vxnh4jngen76gq0njl0kna3aqx7px7p",
      "pool_code_id": "216",
      "lp_code_id": "218"
    },
    {
      "pair": "uwhale-willyo",
      "assets": [
        "{\"token\":{\"native_token\":\"uwhale\"}}",
        "{\"token\":{\"token\":\"migaloo1cykfsqqk4ywgzzqm83thsujsln3lpngaz9ugsxufx398s2vq79dqkn2nlt\"}}"
      ],
      "pool_address": "migaloo1kj4dfhfkgw7ek9gfxw8elnycpzdv5n6amhnxca5ys9udqapaplrqyp66mu",
      "lp_address": "migaloo1xdvymjx3m6lxk5kh8hu6t0qugrtxwzyz4pspg8z4lkxss84j6raqeesc5v",
      "pool_code_id": "216",
      "lp_code_id": "218"
    }
  ]
}
```

### Tokens
```json
{
  "test_tokens": [
    {
      "token_address": "migaloo1se4zqd573xe5afhf6gg06f8jsrhts77tha8nsw8u4qyqdfz0l2jsyccl6x",
      "code_id": "218",
      "symbol": "willyk",
      "decimals": "6",
      "amount": "1000000000000000000000",
      "minted_to": "migaloo1ut7pkdz4hgy689v98vf3dj650frynyaj285zge",
      "tx_hash": "FD38632CDE4A6C604ABFD68DD07C7C6DE6A1631E72B0A70EB95DCA2F7ECBEAC1"
    },
    {
      "token_address": "migaloo1cykfsqqk4ywgzzqm83thsujsln3lpngaz9ugsxufx398s2vq79dqkn2nlt",
      "code_id": "218",
      "symbol": "willyo",
      "decimals": "6",
      "amount": "1000000000000000000000",
      "minted_to": "migaloo1ut7pkdz4hgy689v98vf3dj650frynyaj285zge",
      "tx_hash": "6EA9AF79188FBC772CB06EAE13639B1DD6E5E11D0F7DB702AF58B04FC2E8A7E6"
    },
    {
      "token_address": "migaloo1f8d5n66wshja6vj38avckruwgheu7m7n7frjeurtlgd3h20sr39qtw9c7x",
      "code_id": "218",
      "symbol": "willyo",
      "decimals": "6",
      "amount": "1000000000000000000000",
      "minted_to": "migaloo1ut7pkdz4hgy689v98vf3dj650frynyaj285zge",
      "tx_hash": "45BA0690F5AE283DB9617040AFE80BC9E24619C560CABBCBFEE2D99D23D178E7"
    }
  ],
  "date": "2023-12-12T13:34:33+0000",
  "chain_id": "narwhal-1",
  "minted_to": "migaloo1ut7pkdz4hgy689v98vf3dj650frynyaj285zge"
}
```

### Incentives

```json
{
  "pool_incentives": [
    {
      "pool": "migaloo13kua4jtwkfcx3ngz829axpvrjcns5za3qclvprfqwldk8ucfrsusp3nudu",
      "pool_label": "uwhale-willyk",
      "incentive_contract": "migaloo1kf4uncj48rvrp94hmwtl3cup4gayapq7awcayw92urrq5x59q7tsppzmcv"
    },
    {
      "pool": "migaloo1kj4dfhfkgw7ek9gfxw8elnycpzdv5n6amhnxca5ys9udqapaplrqyp66mu",
      "pool_label": "uwhale-willyo",
      "incentive_contract": "migaloo1cgxsz3g6ryhehn0fnqcf99lektyd26x5uu52mv86wtyu54mdr8zqvz7gzz"
    }
  ],
  "date": "2023-12-12T13:43:04+0000",
  "initial_block_height": "4917049",
  "final_block_height": "4917054",
  "chain_id": "narwhal-1",
  "deployer_address": "migaloo1ut7pkdz4hgy689v98vf3dj650frynyaj285zge"
}
```

### Vaults

```json
{
  "vaults": [
    {
      "asset": "uwhale",
      "vault_address": "migaloo1r9kshk9m4k5k0sdggkm3zlpy7h7304tkw7s6c3ddxaz0xfp34z5skzy63a",
      "lp_address": "migaloo1ymkc5f204ul48wc642a8c32c8cqprvc6dczlnldtfs3t5hv8tk4qk53885",
      "vault_code_id": "219",
      "lp_code_id": "218"
    }
  ],
  "date": "2023-12-12T13:46:56+0000",
  "chain_id": "narwhal-1",
  "vault_factory_addr": "migaloo1zj4h6jvsv07rw6x74jax028leywdekfhahzm0544qevlwvpzc0gs2yt96t"
}
```