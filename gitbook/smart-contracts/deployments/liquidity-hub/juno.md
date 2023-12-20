# Juno (juno-1)

### Contracts, deployed contract addresses, CODEID and Versions
```json
{
  "contracts": [
    {
      "wasm": "fee_collector.wasm",
      "code_id": "3210",
      "version": "1.1.1",
      "contract_address": "juno1dk7uekpslkla89cdh83tgjejhara7c4aasdnc9a2hq9d0652pqmsdr4ldy"
    },
    {
      "wasm": "fee_distributor.wasm",
      "code_id": "3308",
      "version": "0.9.1",
      "contract_address": "juno184ghwgprva7dlr2hwhzgvt6mem6zx78fygk0cpw7klssmzyf67tqdtwt3h"
    },
    {
      "wasm": "frontend_helper.wasm",
      "code_id": "3211",
      "version": "1.0.0",
      "contract_address": "juno150j5gxsepfcaa7lrre3nue23shddw99fuv6kf4m2pvv9ay8glltszmk67f"
    },
    {
      "wasm": "incentive_factory.wasm",
      "code_id": "3653",
      "version": "1.0.1",
      "contract_address": "juno1gg3y2f3kn337qhxwsumpd7wt4avl7knadp7vne4278whw0n3qf5quksw06"
    },
    {
      "wasm": "incentive.wasm",
      "code_id": "3654",
      "version": "1.0.6"
    },
    {
      "wasm": "terraswap_factory.wasm",
      "code_id": "3214",
      "version": "1.2.0",
      "contract_address": "juno14m9rd2trjytvxvu4ldmqvru50ffxsafs8kequmfky7jh97uyqrxqs5xrnx"
    },
    {
      "wasm": "terraswap_pair.wasm",
      "code_id": "3226",
      "version": "1.3.1"
    },
    {
      "wasm": "terraswap_router.wasm",
      "code_id": "3216",
      "version": "1.1.0",
      "contract_address": "juno128lewlw6kv223uw4yzdffl8rnh3k9qs8vrf6kef28579w8ygccyq7m90n2"
    },
    {
      "wasm": "terraswap_token.wasm",
      "code_id": "1440",
      "version": "1.0.2"
    },
    {
      "wasm": "vault_factory.wasm",
      "code_id": "3218",
      "version": "1.1.2",
      "contract_address": "juno1qnfsrwx4c0qnvcnscwm7r55nxr8rpfckq6v8yvuvg7zuqj0uk2hsrssj2n"
    },
    {
      "wasm": "vault.wasm",
      "code_id": "3217",
      "version": "1.2.2"
    },
    {
      "wasm": "vault_router.wasm",
      "code_id": "3219",
      "version": "1.1.5",
      "contract_address": "juno1qa7vdlm6zgq3radal5sltyl4t4qd32feug9qs50kcxda46q230pqzny48s"
    },
    {
      "wasm": "whale_lair.wasm",
      "code_id": "3307",
      "version": "0.9.1",
      "contract_address": "juno1n8slcc79dmwuzdxhsesvhcncaqfg9h4czdm5t5ey8x25ajmn3xzqyde4wv"
    }
  ],
  "date": "2022-08-24T11:04:29+0000",
  "chain_id": "juno-1",
  "deployer_address": "juno1dpx7ytug647wefe7ajxmg5ejt68gxcfv4h7g8t"
}
```

```json
{
  "chain": "juno-1",
  "pool_factory_addr": "juno14m9rd2trjytvxvu4ldmqvru50ffxsafs8kequmfky7jh97uyqrxqs5xrnx",
  "pools": [
    {
      "pair": "ujuno-LOOP",
      "assets": [
        {
          "native_token": {
            "denom": "ujuno"
          }
        },
        {
          "token": {
            "contract_addr": "juno1qsrercqegvs4ye0yqg93knv73ye5dc3prqwd6jcdcuj8ggp6w0us66deup"
          }
        }
      ],
      "pool_address": "juno158mcxa5ajpjfxgy60asrg3m0823m2el5n333xdypcw8h5uwhuvyqkyc4a7",
      "lp_asset": {
        "token": {
          "contract_addr": "juno1zmsgdpdej4g4m4fc5y5p6wr8gn6peh9vx5dk5vf7v7w32jjmcetshl0yw4"
        }
      },
      "incentive_contract": "juno1mhq2reglyzq63n7cnvrc5fefa6ztyxa56nmehsaan4yamu84ntcs70jetd",
      "pool_code_id": "3226",
      "lp_code_id": "1440"
    },
    {
      "pair": "boneWhale-uwhale",
      "assets": [
        {
          "native_token": {
            "denom": "ibc/01BAE2E69D02670B22758FBA74E4114B6E88FC1878936C919DA345E6C6C92ABF"
          }
        },
        {
          "native_token": {
            "denom": "ibc/3A6ADE78FB8169C034C29C4F2E1A61CE596EC8235366F22381D981A98F1F5A5C"
          }
        }
      ],
      "pool_address": "juno160uh2xtegzvc7ekte5x377aud0y40hw75m9l92h7pkqk3l3eg9vqltel48",
      "lp_asset": {
        "token": {
          "contract_addr": "juno1a68d46fyzyq50t3geqe5c50kmswhrezyec8hz6sfngts6k4e77nqqd3yd0"
        }
      },
      "incentive_contract": "juno18a3qpkw5xh8m6r3lkughhv3ccqapjqgzq8923vw8tz6aqepxj5sqxet2gh",
      "pool_code_id": "3226",
      "lp_code_id": "1440"
    },
    {
      "pair": "uatom-uluna",
      "assets": [
        {
          "native_token": {
            "denom": "ibc/C4CFF46FD6DE35CA4CF4CE031E643C8FDC9BA4B99AE598E9B0ED98FE3A2319F9"
          }
        },
        {
          "native_token": {
            "denom": "ibc/107D152BB3176FAEBF4C2A84C5FFDEEA7C7CB4FE1BBDAB710F1FD25BCD055CBF"
          }
        }
      ],
      "pool_address": "juno1k9cw9yghf04cqlu290n4zlveker5cev5ahweqkh07y7zc3xq9hrshjruk8",
      "lp_asset": {
        "token": {
          "contract_addr": "juno1fkejwm7alyfnjngtpgtxvreqfcz8uwer2jgwjn40suvgq20tm8ss73cj05"
        }
      },
      "incentive_contract": "juno1k7sqayt87x8vdeyj8unqtxgrg0s60kut4w95zzgn8ks6puf6udmq4gzt2n",
      "pool_code_id": "3226",
      "lp_code_id": "1440"
    },
    {
      "pair": "ampWHALE-uwhale",
      "assets": [
        {
          "native_token": {
            "denom": "ibc/2F7C2A3D5D42553ED46F57D8B0DE3733B1B5FF571E2C6A051D34525904B4C0AF"
          }
        },
        {
          "native_token": {
            "denom": "ibc/3A6ADE78FB8169C034C29C4F2E1A61CE596EC8235366F22381D981A98F1F5A5C"
          }
        }
      ],
      "pool_address": "juno1dwmrkyhed4szdxxk6l0c98hseancjtdet58n77tfhv2as8cdjdlq7vps00",
      "lp_asset": {
        "token": {
          "contract_addr": "juno1cvnwcgkhxaj70gjg7x57fh447m2wj5yx7p2puu4mqgtf62qphtds88mdsd"
        }
      },
      "incentive_contract": "juno198znyptksrfsrv0lvwcz65g07fx89hew6qq8gl58wtn3gualfa9s5jtzem",
      "pool_code_id": "3226",
      "lp_code_id": "1440"
    },
    {
      "pair": "urac-uwhale",
      "assets": [
        {
          "native_token": {
            "denom": "ibc/D8D6271EC54E3A96C6B9FB6C2BA9E99692B07CEB42754638029657072EA48337"
          }
        },
        {
          "native_token": {
            "denom": "ibc/3A6ADE78FB8169C034C29C4F2E1A61CE596EC8235366F22381D981A98F1F5A5C"
          }
        }
      ],
      "pool_address": "juno1qv337g245ger3cx294m3vu74z74ku7lpf4944qxf8nhx29s8568q4uwrmk",
      "lp_asset": {
        "native_token": {
          "denom": "factory/juno1qv337g245ger3cx294m3vu74z74ku7lpf4944qxf8nhx29s8568q4uwrmk/uLP"
        }
      },
      "incentive_contract": "juno1f0qafvc7jhqcx5qdcnh9y05gfucpxuefztqgnd66hr594nvqmamql3uap2",
      "pool_code_id": "3226",
      "lp_code_id": "1440"
    },
    {
      "pair": "uwhale-uusdc",
      "assets": [
        {
          "native_token": {
            "denom": "ibc/3A6ADE78FB8169C034C29C4F2E1A61CE596EC8235366F22381D981A98F1F5A5C"
          }
        },
        {
          "native_token": {
            "denom": "ibc/EAC38D55372F38F1AFD68DF7FE9EF762DCF69F26520643CF3F9D292A738D8034"
          }
        }
      ],
      "pool_address": "juno1g7ctm7dynjsduf597d8nvt36kwvhfutmzrczdnm00tsz48uryvzqp7p32h",
      "lp_asset": {
        "token": {
          "contract_addr": "juno1lqc9u7lv52jpqgewhtl4w2yjch0234ewfz2z3ykl0z2q67xyfrnsjqw95j"
        }
      },
      "incentive_contract": "juno13wl6hktnurvt6y529a8knzn0w0ml5ff6szlwhkfrwzjhl0zm2nlqgwwec9",
      "pool_code_id": "3226",
      "lp_code_id": "1440"
    },
    {
      "pair": "uatom-uusdc",
      "assets": [
        {
          "native_token": {
            "denom": "ibc/C4CFF46FD6DE35CA4CF4CE031E643C8FDC9BA4B99AE598E9B0ED98FE3A2319F9"
          }
        },
        {
          "native_token": {
            "denom": "ibc/EAC38D55372F38F1AFD68DF7FE9EF762DCF69F26520643CF3F9D292A738D8034"
          }
        }
      ],
      "pool_address": "juno1v6stcdrvwrthfvcwvlmmzht32ft9g9nw85tthcjqer242xg3nvdq8fjasx",
      "lp_asset": {
        "token": {
          "contract_addr": "juno12caca3ymhxr7a73wtdefye86djs69704ktzkv02xkf59se8hx72qwyxq72"
        }
      },
      "incentive_contract": "juno1r8t9e6agehtyack3vsskx885jepynf9jku48g2z96rgaz2u6jshs2gs28f",
      "pool_code_id": "3226",
      "lp_code_id": "1440"
    },
    {
      "pair": "uatom-ujuno",
      "assets": [
        {
          "native_token": {
            "denom": "ibc/C4CFF46FD6DE35CA4CF4CE031E643C8FDC9BA4B99AE598E9B0ED98FE3A2319F9"
          }
        },
        {
          "native_token": {
            "denom": "ujuno"
          }
        }
      ],
      "pool_address": "juno1p9z8xe96fyvg3h5gtvnpjjv2u47q6l7sdhg6asmyfgc6q8l8ttgqfvxnxh",
      "lp_asset": {
        "token": {
          "contract_addr": "juno1g3549wm0tffdzdpasufjr0nccu9ynzpzway5g3u6ucmhfd4ds05swswasc"
        }
      },
      "incentive_contract": "juno1krkuxv305q946x9vx5mvs406lp7zcxgyr09kdlr7xqvkgasdg6aqe88w35",
      "pool_code_id": "3226",
      "lp_code_id": "1440"
    },
    {
      "pair": "ujuno-uusdc",
      "assets": [
        {
          "native_token": {
            "denom": "ujuno"
          }
        },
        {
          "native_token": {
            "denom": "ibc/EAC38D55372F38F1AFD68DF7FE9EF762DCF69F26520643CF3F9D292A738D8034"
          }
        }
      ],
      "pool_address": "juno1wkjy5wl0pd5xxvwtrx37r7ydkt3dkwvghs00tvvqyd3xnjukah7qpj0vj7",
      "lp_asset": {
        "token": {
          "contract_addr": "juno19mkjyvydnq440a3ms4fccpltrzmxlvlz6nvz6qul0mgxvse42n2q9qkf72"
        }
      },
      "incentive_contract": "juno12zk3vhpukhqucpkv9xd2j9xrxlqc0v5yuw0sdd7n3jg2cts4rdaqaf02vr",
      "pool_code_id": "3226",
      "lp_code_id": "1440"
    },
    {
      "pair": "ujuno-RAW",
      "assets": [
        {
          "native_token": {
            "denom": "ujuno"
          }
        },
        {
          "token": {
            "contract_addr": "juno15u3dt79t6sxxa3x3kpkhzsy56edaa5a66wvt3kxmukqjz2sx0hes5sn38g"
          }
        }
      ],
      "pool_address": "juno1xpt9mkncxadadn5t8s4t74nmw5zlarghmpme26857s07xz388d6sukvtnz",
      "lp_asset": {
        "token": {
          "contract_addr": "juno1zetjfu8j0ndt4d3mgewhatgpfrj8pwhev2tdp3sa9dwwmqlgdxws4257we"
        }
      },
      "incentive_contract": "juno1qs4qn7cqqqjcfp02qdw5fv7jmjy6lj4s05pd99a6z7ey6arhrlwsu9lf8y",
      "pool_code_id": "3226",
      "lp_code_id": "1440"
    },
    {
      "pair": "SGNL-ujuno",
      "assets": [
        {
          "token": {
            "contract_addr": "juno14lycavan8gvpjn97aapzvwmsj8kyrvf644p05r0hu79namyj3ens87650k"
          }
        },
        {
          "native_token": {
            "denom": "ujuno"
          }
        }
      ],
      "pool_address": "juno1pkyvelj5vfp6r8dq2utruw86vw9fvkjrd5c2x7m43m6cext8lzxs4k57dt",
      "lp_asset": {
        "native_token": {
          "denom": "factory/juno1pkyvelj5vfp6r8dq2utruw86vw9fvkjrd5c2x7m43m6cext8lzxs4k57dt/uLP"
        }
      },
      "incentive_contract": "juno1fgh87cfgm6nkezsjfsswtsfedvf2u2k63wynkvcw6900pv80rn0qxv0u9r",
      "pool_code_id": "3226",
      "lp_code_id": "1440"
    },
    {
      "pair": "bJuno-ujuno",
      "assets": [
        {
          "token": {
            "contract_addr": "juno1mvkgcr5uce2rnpzr4qrzf50hx4qreuwzlt7fzsjrhjud3xnjmttq5mkh2m"
          }
        },
        {
          "native_token": {
            "denom": "ujuno"
          }
        }
      ],
      "pool_address": "juno12w6f755zx9l0vflfvql2jvl2jlyv348esyh7utvx727nwpy2jg5qsjemyx",
      "lp_asset": {
        "token": {
          "contract_addr": "juno1qdj9shhfasyjuvncawstvmcqp2afxet0x36jaaxt0udp6gq27ftq9xr5d4"
        }
      },
      "incentive_contract": "juno1nwrtue0vjftecegzyarhxdtedh0263akfle3522x0dx5jr0decms3vpd4t",
      "pool_code_id": "3226",
      "lp_code_id": "1440"
    },
    {
      "pair": "ampJUNO-ujuno",
      "assets": [
        {
          "token": {
            "contract_addr": "juno1a0khag6cfzu5lrwazmyndjgvlsuk7g4vn9jd8ceym8f4jf6v2l9q6d348a"
          }
        },
        {
          "native_token": {
            "denom": "ujuno"
          }
        }
      ],
      "pool_address": "juno137593pljsgltp9863sawquejpxzmtpvuafg0c7tpqqer3hkz48eslwrl4l",
      "lp_asset": {
        "token": {
          "contract_addr": "juno1th5zf95xevutfgqc2a4cexqpeykx0y0q87jzexhd7pmzdxnpg4qs8tg3t5"
        }
      },
      "incentive_contract": "juno1zzs9fv6qz8sjn0v36d22900txv9c7m7u9vlt66t07kwjvl6srcyqq2q63z",
      "pool_code_id": "3226",
      "lp_code_id": "1440"
    }
  ]
}
```

### Pool Incentives 

```json
{
  "pool_incentives": [
    {
      "pool": "juno158mcxa5ajpjfxgy60asrg3m0823m2el5n333xdypcw8h5uwhuvyqkyc4a7",
      "pool_label": "ujuno-LOOP",
      "incentive_contract": "juno1mhq2reglyzq63n7cnvrc5fefa6ztyxa56nmehsaan4yamu84ntcs70jetd"
    },
    {
      "pool": "juno160uh2xtegzvc7ekte5x377aud0y40hw75m9l92h7pkqk3l3eg9vqltel48",
      "pool_label": "ibc/01BA...2ABF-ibc/3A6A...5A5C",
      "incentive_contract": "juno18a3qpkw5xh8m6r3lkughhv3ccqapjqgzq8923vw8tz6aqepxj5sqxet2gh"
    },
    {
      "pool": "juno1k9cw9yghf04cqlu290n4zlveker5cev5ahweqkh07y7zc3xq9hrshjruk8",
      "pool_label": "ibc/C4CF...19F9-ibc/107D...5CBF",
      "incentive_contract": "juno1k7sqayt87x8vdeyj8unqtxgrg0s60kut4w95zzgn8ks6puf6udmq4gzt2n"
    },
    {
      "pool": "juno1dwmrkyhed4szdxxk6l0c98hseancjtdet58n77tfhv2as8cdjdlq7vps00",
      "pool_label": "ibc/2F7C...C0AF-ibc/3A6A...5A5C",
      "incentive_contract": "juno198znyptksrfsrv0lvwcz65g07fx89hew6qq8gl58wtn3gualfa9s5jtzem"
    },
    {
      "pool": "juno1g7ctm7dynjsduf597d8nvt36kwvhfutmzrczdnm00tsz48uryvzqp7p32h",
      "pool_label": "ibc/3A6A...5A5C-ibc/EAC3...8034",
      "incentive_contract": "juno13wl6hktnurvt6y529a8knzn0w0ml5ff6szlwhkfrwzjhl0zm2nlqgwwec9"
    },
    {
      "pool": "juno1v6stcdrvwrthfvcwvlmmzht32ft9g9nw85tthcjqer242xg3nvdq8fjasx",
      "pool_label": "ibc/C4CF...19F9-ibc/EAC3...8034",
      "incentive_contract": "juno1r8t9e6agehtyack3vsskx885jepynf9jku48g2z96rgaz2u6jshs2gs28f"
    },
    {
      "pool": "juno1p9z8xe96fyvg3h5gtvnpjjv2u47q6l7sdhg6asmyfgc6q8l8ttgqfvxnxh",
      "pool_label": "ibc/C4CF...19F9-ujuno",
      "incentive_contract": "juno1krkuxv305q946x9vx5mvs406lp7zcxgyr09kdlr7xqvkgasdg6aqe88w35"
    },
    {
      "pool": "juno1wkjy5wl0pd5xxvwtrx37r7ydkt3dkwvghs00tvvqyd3xnjukah7qpj0vj7",
      "pool_label": "ujuno-ibc/EAC3...8034",
      "incentive_contract": "juno12zk3vhpukhqucpkv9xd2j9xrxlqc0v5yuw0sdd7n3jg2cts4rdaqaf02vr"
    },
    {
      "pool": "juno1xpt9mkncxadadn5t8s4t74nmw5zlarghmpme26857s07xz388d6sukvtnz",
      "pool_label": "ujuno-RAW",
      "incentive_contract": "juno1qs4qn7cqqqjcfp02qdw5fv7jmjy6lj4s05pd99a6z7ey6arhrlwsu9lf8y"
    },
    {
      "pool": "juno12w6f755zx9l0vflfvql2jvl2jlyv348esyh7utvx727nwpy2jg5qsjemyx",
      "pool_label": "bJuno-ujuno",
      "incentive_contract": "juno1nwrtue0vjftecegzyarhxdtedh0263akfle3522x0dx5jr0decms3vpd4t"
    },
    {
      "pool": "juno137593pljsgltp9863sawquejpxzmtpvuafg0c7tpqqer3hkz48eslwrl4l",
      "pool_label": "ampJUNO-ujuno",
      "incentive_contract": "juno1zzs9fv6qz8sjn0v36d22900txv9c7m7u9vlt66t07kwjvl6srcyqq2q63z"
    }
  ],
  "date": "2023-06-29T13:55:41+0000",
  "initial_block_height": "8920163",
  "final_block_height": "8920186",
  "chain_id": "juno-1",
  "deployer_address": "juno1dpx7ytug647wefe7ajxmg5ejt68gxcfv4h7g8t"
}
```

### Vaults 

```json
{
  "chain": "juno-1",
  "vault_factory_addr": "juno1qnfsrwx4c0qnvcnscwm7r55nxr8rpfckq6v8yvuvg7zuqj0uk2hsrssj2n",
  "vaults": [
    {
      "vault": "juno1gz9qhtcafjc0c9hnvrn2au253yaae6qunymt5yrgvagxejr2n2lquk6ss8",
      "asset": {
        "native_token": {
          "denom": "ujuno"
        }
      },
      "lp_asset": {
        "token": {
          "contract_addr": "juno1menz0s2rgu62c0lrrfw7zswrs2deeh9emnawt5jjgdfgvja4uqmq50hfhp"
        }
      },
      "vault_code_id": "3217",
      "lp_code_id": "1440"
    }
  ]
}
```

# Juno testnet (uni-5)

```json
{
  "contracts": [
    {
      "wasm": "fee_collector.wasm",
      "code_id": "3421",
      "version": "1.0.5",
      "contract_address": "juno1gqtcknu8kze4668g4w892c6zdlgz23d9alw9nxkh0upctn4mlghsq9t4mn"
    },
    {
      "wasm": "terraswap_factory.wasm",
      "code_id": "3422",
      "version": "1.1.2",
      "contract_address": "juno15cdzmhx47yyqejzh0mcrqpzvexzzqzgusgjfkhrnpjc592xtuvqsxazy23"
    },
    {
      "wasm": "terraswap_pair.wasm",
      "code_id": "3423",
      "version": "1.2.0"
    },
    {
      "wasm": "terraswap_router.wasm",
      "code_id": "3424",
      "version": "1.0.7",
      "contract_address": "juno1krumlux5aa2ar7chnd3ju4zsw3s6u6kz6lge9sax9a3s6nhqr6dqeyngmk"
    },
    {
      "wasm": "terraswap_token.wasm",
      "code_id": "3425",
      "version": "1.0.2"
    },
    {
      "wasm": "vault_factory.wasm",
      "code_id": "3426",
      "version": "1.0.9",
      "contract_address": "juno1r26wpz55fdctn8seqh4kqmewuhc7yr5r62s4lvlqa3sy2tq697gsnm9grs"
    },
    {
      "wasm": "vault_router.wasm",
      "code_id": "3427",
      "version": "1.1.3",
      "contract_address": "juno16pxxzw0n0ta8q5ftyj0fhd0kq4v60yx7au0hkg87dlc5e8wgz7xsymalfn"
    },
    {
      "wasm": "vault.wasm",
      "code_id": "3428",
      "version": "1.2.0"
    }
  ],
  "date": "2022-12-15T15:54:19+0000",
  "initial_block_height": "586199",
  "final_block_height": "1246719",
  "chain_id": "uni-5",
  "deployer_address": "juno1ut7pkdz4hgy689v98vf3dj650frynyaj3p7r6t"
}
```

```json
{
  "pools": [
    {
      "pair": "ujunox-ujunoxone",
      "assets": [
        "{\"native_token\":{\"denom\":\"ujunox\"}}",
        "{\"token\":{\"contract_addr\":\"juno1yysq5rsdar0sck0tqtftqmcqeqxws4qc0x3epu2y4yxvgks7chjq6r8739\"}}"
      ],
      "pool_address": "juno1dfuq7zkgd2d4ke3rgekfzfkt4km806k9kje68xdxrd5438yrs80qam4g5g",
      "lp_address": "juno1yprgcsjnm4z7x4sc906waph025fxc47gy82599us8tq0066np49s733red",
      "pool_code_id": "1689",
      "lp_code_id": "1691"
    },
    {
      "pair": "ujunox-ujunoxone",
      "assets": [
        "{\"native_token\":{\"denom\":\"ujunox\"}}",
        "{\"token\":{\"contract_addr\":\"juno1yysq5rsdar0sck0tqtftqmcqeqxws4qc0x3epu2y4yxvgks7chjq6r8739\"}}"
      ],
      "pool_address": "juno10v69hvmsmyd89ch35zrl6rct52jaafe2d0s09wmqx5d0f4w95w9qezl02t",
      "lp_address": "juno14t6v0vtevrrxg3ln3t3e0da4j3ddwxmaf639p8g4984p69r69puqtg8dfx",
      "pool_code_id": "1689",
      "lp_code_id": "1691"
    },
    {
      "pair": "ujunox-ujunotwo",
      "assets": [
        "{\"native_token\":{\"denom\":\"ujunox\"}}",
        "{\"token\":{\"contract_addr\":\"juno1q88phj9y6melq749ltpv0wer9wdm76axp2enem9m4u2sq5r0qnhsaapqcy\"}}"
      ],
      "pool_address": "juno19rhjul46h5xtm4w3jqchhve9gy06vkuaz42dj9vk47nceypjgwmq38llyr",
      "lp_address": "juno1ak2wpvu84ycyn2my0jel79863gczxnwt2etysla7qfpmuy8ycyaqrdrwua",
      "pool_code_id": "1689",
      "lp_code_id": "1691"
    },
    {
      "pair": "ujunox-ujunotwo",
      "assets": [
        "{\"native_token\":{\"denom\":\"ujunox\"}}",
        "{\"token\":{\"contract_addr\":\"juno1q88phj9y6melq749ltpv0wer9wdm76axp2enem9m4u2sq5r0qnhsaapqcy\"}}"
      ],
      "pool_address": "juno1p25at0hk655vlx62xvaavzvefcfl63kzc0h8a2n7vqquth4zqm0shj2pr4",
      "lp_address": "juno1n84ukyw5nm57a5t9ft3vff3fez4je087e9n9c46dlzunr3kqhf3qcap8ws",
      "pool_code_id": "1689",
      "lp_code_id": "1691"
    },
    {
      "pair": "ujunox-uLP",
      "assets": [
        "{\"native_token\":{\"denom\":\"ujunox\"}}",
        "{\"token\":{\"contract_addr\":\"juno1yprgcsjnm4z7x4sc906waph025fxc47gy82599us8tq0066np49s733red\"}}"
      ],
      "pool_address": "juno1qhhr6g4kzretuy3ktlkyaaz43x7cenzuzuhxdpu0gxde7vncym2seud68s",
      "lp_address": "juno17cz3zyzltna46lqzzua3jlr6rvm6usladjn7tghvujl9fcqaa5eq3nudhj",
      "pool_code_id": "1689",
      "lp_code_id": "1691"
    }
  ],
  "date": "2022-11-02T15:31:36+0000",
  "chain_id": "uni-5",
  "pool_factory_addr": "juno16v8v0v25yex4w0w5kr5y78uenpe2w83vu03efvcexsz3y98vntuq7pts74"
}
```

```json
{
  "vaults": [
    {
      "asset": "ujunox",
      "vault_address": "juno1370d2esr2ydetzrtuq77r5g2lsdtwe2288pdev6knvvdk22mn8as0h63ry",
      "lp_address": "juno1wd4t46g3666nga3sfjc74alws7lmk7vxrfjkk4klsakzdajz4dyq9l7gkc",
      "vault_code_id": "3428",
      "lp_code_id": "3425"
    }
  ],
  "date": "2022-12-15T16:09:30+0000",
  "chain_id": "uni-5",
  "vault_factory_addr": "juno1r26wpz55fdctn8seqh4kqmewuhc7yr5r62s4lvlqa3sy2tq697gsnm9grs",
  "vault_router_addr": "juno16pxxzw0n0ta8q5ftyj0fhd0kq4v60yx7au0hkg87dlc5e8wgz7xsymalfn"
}