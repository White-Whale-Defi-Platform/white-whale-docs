# Migaloo (migaloo-1)

```json
{
  "contracts": [
    {
      "wasm": "fee_collector.wasm",
      "code_id": "373",
      "version": "1.1.4",
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
      "code_id": "374",
      "version": "1.0.6"
    },
    {
      "wasm": "incentive_factory.wasm",
      "code_id": "375",
      "version": "1.0.1",
      "contract_address": "migaloo1rqfr752hn6auzm3vzzyr2pd8rt6fapf208vm8qfpejstt69uxfwqcdrdq3"
    },
    {
      "wasm": "stableswap_3pool.wasm",
      "code_id": "386",
      "version": "1.2.3"
    },
    {
      "wasm": "terraswap_factory.wasm",
      "code_id": "384",
      "version": "1.2.1",
      "contract_address": "migaloo1z89funaazn4ka8vrmmw4q27csdykz63hep4ay8q2dmlspc6wtdgq92u369"
    },
    {
      "wasm": "terraswap_pair.wasm",
      "code_id": "385",
      "version": "1.3.4"
    },
    {
      "wasm": "terraswap_router.wasm",
      "code_id": "379",
      "version": "1.1.1",
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
      "code_id": "402",
      "version": "1.2.6"
    },
    {
      "wasm": "vault_router.wasm",
      "code_id": "381",
      "version": "1.1.6",
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

```json 
{
  "chain": "migaloo-1",
  "pool_factory_addr": "migaloo1z89funaazn4ka8vrmmw4q27csdykz63hep4ay8q2dmlspc6wtdgq92u369",
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
      "pair": "uguppy-ash",
      "assets": [
        {
          "native_token": {
            "denom": "factory/migaloo1etlu2h30tjvv8rfa4fwdc43c92f6ul5w9acxzk/uguppy"
          }
        },
        {
          "native_token": {
            "denom": "factory/migaloo1erul6xyq0gk6ws98ncj7lnq9l4jn4gnnu9we73gdz78yyl2lr7qqrvcgup/ash"
          }
        }
      ],
      "pool_address": "migaloo16yra8pf3ntm6ljjnja2w046zka3wm68fvd3x08htfdpn2mumqwkst7mllv",
      "lp_asset": {
        "native_token": {
          "denom": "factory/migaloo16yra8pf3ntm6ljjnja2w046zka3wm68fvd3x08htfdpn2mumqwkst7mllv/uLP"
        }
      },
      "incentive_contract": "migaloo1mh36nwy4et6fvku9e73m87g9dnhr7z3xge67d9g8f2yl7cn6lpuqyf3cnc",
      "pool_code_id": "31",
      "lp_code_id": "33"
    },
    {
      "pair": "uguppy-uwhale",
      "assets": [
        {
          "native_token": {
            "denom": "factory/migaloo1etlu2h30tjvv8rfa4fwdc43c92f6ul5w9acxzk/uguppy"
          }
        },
        {
          "native_token": {
            "denom": "uwhale"
          }
        }
      ],
      "pool_address": "migaloo14p3r422qp04p345mnqe5umjy3vqx75hpxf54f8enf59wf27fksvqltavjp",
      "lp_asset": {
        "native_token": {
          "denom": "factory/migaloo14p3r422qp04p345mnqe5umjy3vqx75hpxf54f8enf59wf27fksvqltavjp/uLP"
        }
      },
      "incentive_contract": "migaloo1ur4j7x270ascx74k5j65r6zd2dyq0y407jdewk2nse9gpzg9mrds5czrtn",
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
      "pair": "ophir-uwhale",
      "assets": [
        {
          "native_token": {
            "denom": "factory/migaloo1t862qdu9mj5hr3j727247acypym3ej47axu22rrapm4tqlcpuseqltxwq5/ophir"
          }
        },
        {
          "native_token": {
            "denom": "uwhale"
          }
        }
      ],
      "pool_address": "migaloo1p5adwk3nl9pfmjjx6fu9mzn4xfjry4l2x086yq8u8sahfv6cmuyspryvyu",
      "lp_asset": {
        "native_token": {
          "denom": "factory/migaloo1p5adwk3nl9pfmjjx6fu9mzn4xfjry4l2x086yq8u8sahfv6cmuyspryvyu/uLP"
        }
      },
      "incentive_contract": "migaloo1gjuv6570dupd7l5t6tz6m45jhnjv0x73qh7d629a4d4aze2lktjs85aj8y",
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
      "pair": "SAYVE-uwhale",
      "assets": [
        {
          "native_token": {
            "denom": "ibc/106B438A78C581C5291E114B21588C41F98532E04D5369CFEE5825D95D465278"
          }
        },
        {
          "native_token": {
            "denom": "uwhale"
          }
        }
      ],
      "pool_address": "migaloo1ke0krjh5v3emzv5wdut6q7l0gednv7cx7naxqweae44jz8cxxq9srhy6dz",
      "lp_asset": {
        "native_token": {
          "denom": "factory/migaloo1ke0krjh5v3emzv5wdut6q7l0gednv7cx7naxqweae44jz8cxxq9srhy6dz/uLP"
        }
      },
      "incentive_contract": "migaloo1kwdf63gwzhdwyy7hmmn67p3dex57e5ek4na8g27hvd7kn9cj7nmqgsxyz7",
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
    },
    {
      "pair": "uplnk-uwhale",
      "assets": [
        {
          "native_token": {
            "denom": "ibc/E49A6D116739E0920F8F2D68A8F0A8E07DC272FA1421F70CAD738463AA296724"
          }
        },
        {
          "native_token": {
            "denom": "uwhale"
          }
        }
      ],
      "pool_address": "migaloo195rkvthzyndrguzxhulca4wmgten7aja49vvj4pq9wfm7azd3ahq84r3d2",
      "lp_asset": {
        "native_token": {
          "denom": "factory/migaloo195rkvthzyndrguzxhulca4wmgten7aja49vvj4pq9wfm7azd3ahq84r3d2/uLP"
        }
      },
      "incentive_contract": "migaloo1sf6nld2a56urwvxf8aj4964c5v3awt0hxjnz88dx9f9r4c2cjtxqr3842d",
      "pool_code_id": "31",
      "lp_code_id": "33"
    },
    {
      "pair": "guppy-gash",
      "assets": [
        {
        "native_token": {
          "denom": "factory/migaloo1etlu2h30tjvv8rfa4fwdc43c92f6ul5w9acxzk/uguppy"
        }
        },
        {
          "native_token": {
            "denom": "factory/migaloo1r9x8fz4alekzr78k42rpmr9unpa7egsldpqeynmwl2nfvzexue9sn8l5rg/gash"
          }
        }
      ],
      "pool_address": "migaloo1huj5syg78rm3nuslzf9py73ccegcth2lkfpf5pvaq6q68pakldmsahxmfl",
      "lp_asset": {
        "native_token": {
          "denom": "factory/migaloo1huj5syg78rm3nuslzf9py73ccegcth2lkfpf5pvaq6q68pakldmsahxmfl/uLP"
        }
      },
      "incentive_contract": "migaloo10knl076uc8sjqsz6k49j94phv5aqqp0v7u8aaqjx6s3pdrmtsmzskjepd6",
      "pool_code_id": "31",
      "lp_code_id": "33"
    },
    {
      "pair": "uwhale-wBTC.axl",
      "assets": [
        {
        "native_token": {
          "denom": "uwhale"
        }
        },
        {
          "native_token": {
            "denom": "ibc/B65E189D3168DB40C88C6A6C92CA3D3BB0A8B6310325D4C43AB5702F06ECD60B"
          }
        }
      ],
      "pool_address": "migaloo1j2dtdu2kjf7l555fkej9cv5cmp79c6g5q8p67gt3yhvm2auzclvsq429y3",
      "lp_asset": {
        "native_token": {
          "denom": "factory/migaloo1j2dtdu2kjf7l555fkej9cv5cmp79c6g5q8p67gt3yhvm2auzclvsq429y3/uLP"
        }
      },
      "incentive_contract": "migaloo17m88zthuym6rajrfl8gjnh9j3hzu3zhkmmsrys9qp6y28v58vgus3hwksm",
      "pool_code_id": "31",
      "lp_code_id": "33"
    },
    {
      "pair": "ampwhaleT-ampWhale",
      "assets": [
        {
        "native_token": {
          "denom": "ibc/EA459CE57199098BA5FFDBD3194F498AA78439328A92C7D136F06A5220903DA6"
        }
        },
        {
          "native_token": {
            "denom": "factory/migaloo1436kxs0w2es6xlqpp9rd35e3d0cjnw4sv8j3a7483sgks29jqwgshqdky4/ampWHALE"
          }
        }
      ],
      "pool_address": "migaloo1ugv3g8lckm70np3u50u5wetnv2dfda073gyazy2v50t5c3wza3xqj5drtk",
      "lp_asset": {
        "native_token": {
          "denom": "factory/migaloo1ugv3g8lckm70np3u50u5wetnv2dfda073gyazy2v50t5c3wza3xqj5drtk/uLP"
        }
      },
      "incentive_contract": "",
      "pool_code_id": "31",
      "lp_code_id": "33"
    },
    {
      "pair": "bonewhaleT-boneWhale",
      "assets": [
        {
        "native_token": {
          "denom": "ibc/E54A0C1E4A2A79FD4F92765F68E38939867C3DA36E2EA6BBB2CE81C43F4C8ADC"
        }
        },
        {
          "native_token": {
            "denom": "factory/migaloo1mf6ptkssddfmxvhdx0ech0k03ktp6kf9yk59renau2gvht3nq2gqdhts4u/boneWhale"
          }
        }
      ],
      "pool_address": "migaloo1azqqmeg7zcj9vdtqpc65dmr2fkmkf3x6dcyhnau6d6er0w2r3arq470dzj",
      "lp_asset": {
        "native_token": {
          "denom": "factory/migaloo1azqqmeg7zcj9vdtqpc65dmr2fkmkf3x6dcyhnau6d6er0w2r3arq470dzj/uLP"
        }
      },
      "incentive_contract": "",
      "pool_code_id": "31",
      "lp_code_id": "33"
    },
    {
      "pair": "uwhale-wBTC",
      "assets": [
        {
        "native_token": {
          "denom": "uwhale"
        }
        },
        {
          "native_token": {
            "denom": "ibc/6E5BF71FE1BEBBD648C8A7CB7A790AEF0081120B2E5746E6563FC95764716D61"
          }
        }
      ],
      "pool_address": "migaloo1axtz4y7jyvdkkrflknv9dcut94xr5k8m6wete4rdrw4fuptk896su44x2z",
      "lp_asset": {
        "native_token": {
          "denom": "factory/migaloo1axtz4y7jyvdkkrflknv9dcut94xr5k8m6wete4rdrw4fuptk896su44x2z/uLP"
        }
      },
      "incentive_contract": "",
      "pool_code_id": "31",
      "lp_code_id": "33"
    },
    {
      "pair": "shark-uwhale",
      "assets": [
        
        {
          "native_token": {
            "denom": "factory/migaloo1eqntnl6tzcj9h86psg4y4h6hh05g2h9nj8e09l/shark"
          }
        },
        {
        "native_token": {
          "denom": "uwhale"
        }
        },
      ],
      "pool_address": "migaloo14emfp5urhu0nnnk5warexg3fdfl8gltru9y3ylzx6cay6utdgpdsyh99r7",
      "lp_asset": {
        "native_token": {
          "denom": "factory/migaloo14emfp5urhu0nnnk5warexg3fdfl8gltru9y3ylzx6cay6utdgpdsyh99r7/uLP"
        }
      },
      "incentive_contract": "",
      "pool_code_id": "31",
      "lp_code_id": "33"
    }
  ]
}
```

```json
{
  "chain": "migaloo-1",
  "vault_factory_addr": "migaloo1g2xwx805epc897rwyrykskjque07yxfmc4qq2p4ef5dwd6znl30qkgw8w7",
  "vaults": [
    {
      "vault": "migaloo16ku76pxpt2uhsvj2aemrehgz69aru5d76a0pqk4fpj8s2wt3lnhqtnvghe",
      "asset": {
        "native_token": {
          "denom": "uwhale"
        }
      },
      "lp_asset": {
        "native_token": {
          "denom": "factory/migaloo16ku76pxpt2uhsvj2aemrehgz69aru5d76a0pqk4fpj8s2wt3lnhqtnvghe/uLP"
        }
      },
      "vault_code_id": "44",
      "lp_code_id": "33"
    }
  ]
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