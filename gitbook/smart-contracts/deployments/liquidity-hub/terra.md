# Terra (phoenix-1)

```json
{
  "contracts": [
    {
      "wasm": "fee_collector.wasm",
      "code_id": "2293",
      "version": "1.1.4",
      "contract_address": "terra1w8402njz8936ag4rlcmvek4zcns6hlkaapsd4qwz5us0ewwyghrsx7k47w"
    },
    {
      "wasm": "fee_distributor.wasm",
      "code_id": "2605",
      "version": "0.9.2",
      "contract_address": "terra1xm0yh8cv8rww6g87h3q0megt6ntxqzw6p6hgh5l4jrhed4fe7hnq9cvzm5"
    },
    {
      "wasm": "frontend_helper.wasm",
      "code_id": "1595",
      "version": "1.0.0",
      "contract_address": "terra1tslnzaadfhwdj67dzfvxhhy2agp0w69dt5uk5nfeaecevdqkh52sufhfrd"
    },
    {
      "wasm": "incentive_factory.wasm",
      "code_id": "1791",
      "version": "1.0.1",
      "contract_address": "terra1qsfcuketm4slntdp92kg3ltnn57j7dzq3wg3yqjr8xhsnae6fn3sjmle9y"
    },
    {
      "wasm": "incentive.wasm",
      "code_id": "2647",
      "version": "1.0.6"
    },
    {
      "wasm": "stableswap_3pool.wasm",
      "code_id": "2607",
      "version": "1.2.3"
    },
    {
      "wasm": "terraswap_factory.wasm",
      "code_id": "2608",
      "version": "1.2.3",
      "contract_address": "terra1f4cr4sr5eulp3f2us8unu6qv8a5rhjltqsg7ujjx6f2mrlqh923sljwhn3"
    },
    {
      "wasm": "terraswap_pair.wasm",
      "code_id": "2609",
      "version": "1.3.5"
    },
    {
      "wasm": "terraswap_router.wasm",
      "code_id": "1934",
      "version": "1.1.1",
      "contract_address": "terra1p37jrwlaqpklzlu4rwjyjrmzuezdgk3pyuyk2zclc4rda6awkm3qnj6f0a"
    },
    {
      "wasm": "terraswap_token.wasm",
      "code_id": "726",
      "version": "1.0.2"
    },
    {
      "wasm": "vault_factory.wasm",
      "code_id": "2610",
      "version": "1.1.3",
      "contract_address": "terra1vcn8h6fc26nv4f20p6g870a00nqzdpjwvshud9ku3qfaqhv7l69s9l29y2"
    },
    {
      "wasm": "vault.wasm",
      "code_id": "2613",
      "version": "1.2.6"
    },
    {
      "wasm": "vault_router.wasm",
      "code_id": "2612",
      "version": "1.1.6",
      "contract_address": "terra1c8tpvta3umr4mpufvxmq39gyuw2knpyxyfgq8thpaeyw2r6a80qsg5wa00"
    },
    {
      "wasm": "whale_lair.wasm",
      "code_id": "1680",
      "version": "0.9.1",
      "contract_address": "terra1qa5a8fkynmthlrh9wsae4sqnuxdrespsls7c7acayqqvs5s63eksm53snj"
    }
  ],
  "date": "2022-08-23T15:43:25+0000",
  "chain_id": "phoenix-1",
  "deployer_address": "terra1z5m4yq93glzzxfjhppgj7qzep2ndf9jk6xkhp3"
}
```

```json
{
  "chain": "phoenix-1",
  "pool_factory_addr": "terra1f4cr4sr5eulp3f2us8unu6qv8a5rhjltqsg7ujjx6f2mrlqh923sljwhn3",
  "pools": [
    {
      "pair": "ampROAR-ROAR",
      "assets": [
        {
          "native_token": {
            "denom": "factory/terra1vklefn7n6cchn0u962w3gaszr4vf52wjvd4y95t2sydwpmpdtszsqvk9wy/ampROAR"
          }
        },
        {
          "token": {
            "contract_addr": "terra1lxx40s29qvkrcj8fsa3yzyehy7w50umdvvnls2r830rys6lu2zns63eelv"
          }
        }
      ],
      "pool_address": "terra1d8ap3zyd6tfnruuuwvs0t927lr4zwptruhulfwnxjpqzudvyn8usfgl8ze",
      "lp_asset": {
        "native_token": {
          "denom": "factory/terra1d8ap3zyd6tfnruuuwvs0t927lr4zwptruhulfwnxjpqzudvyn8usfgl8ze/uLP"
        }
      },
      "incentive_contract": "terra1zudg2pz9qcr2dazx70tth0kudvel0zcx69zc9k64nh6uaj3w0lgqgt4s3g",
      "pool_code_id": "2609",
      "lp_code_id": "726"
    },
    {
      "pair": "wbtc-satoshi-uluna",
      "assets": [
        {
          "native_token": {
            "denom": "ibc/05D299885B07905B6886F554B39346EA6761246076A1120B1950049B92B922DD"
          }
        },
        {
          "native_token": {
            "denom": "uluna"
          }
        }
      ],
      "pool_address": "terra1xhhr7x8yhv9p336t3squh5f8t2827ttrevnwrwwvqrp88nkt665qy0w07c",
      "lp_asset": {
        "native_token": {
          "denom": "factory/terra1xhhr7x8yhv9p336t3squh5f8t2827ttrevnwrwwvqrp88nkt665qy0w07c/uLP"
        }
      },
      "incentive_contract": "terra1me4wdxxtv4e4ctrgjc9ks9npmxhtfppcq9czecun8gwkervw060sc5eu23",
      "pool_code_id": "2609",
      "lp_code_id": "726"
    },
    {
      "pair": "uwhale-uatom",
      "assets": [
        {
          "native_token": {
            "denom": "ibc/36A02FFC4E74DF4F64305130C3DFA1B06BEAC775648927AA44467C76A77AB8DB"
          }
        },
        {
          "native_token": {
            "denom": "ibc/27394FB092D2ECCD56123C74F36E4C1F926001CEADA9CA97EA622B25F41E5EB2"
          }
        }
      ],
      "pool_address": "terra1ma4ar7ygensq2pplw0ss9v289tzmc728f3qv84u43k5n8mp6ex7q7uv93s",
      "lp_asset": {
        "token": {
          "contract_addr": "terra1wy6c9dxvr3998cgueewh77nsg0lsykssgg7dldyp8prvc35n0sls0gxcy4"
        }
      },
      "incentive_contract": "null",
      "pool_code_id": "2609",
      "lp_code_id": "726"
    },
    {
      "pair": "uatom-ujuno",
      "assets": [
        {
          "native_token": {
            "denom": "ibc/27394FB092D2ECCD56123C74F36E4C1F926001CEADA9CA97EA622B25F41E5EB2"
          }
        },
        {
          "native_token": {
            "denom": "ibc/4CD525F166D32B0132C095F353F4C6F033B0FF5C49141470D1EFDA1D63303D04"
          }
        }
      ],
      "pool_address": "terra1p2xgcr2ewnetug8ahqms5y3k6rxyh2xglnzzx500ylh4420h9ucqz8w7x5",
      "lp_asset": {
        "token": {
          "contract_addr": "terra1avfsch3ee82wyrpwlawecyz6zktr9jln0zaxp58xuvmxyl5g305q3rwuj3"
        }
      },
      "incentive_contract": "terra1ckguuv8s8rg0rd5cdn0y3fynwrpqf32jxvjdyzclu49se3tv6nvs6gpu62",
      "pool_code_id": "2609",
      "lp_code_id": "726"
    },
    {
      "pair": "uatom-uusdc",
      "assets": [
        {
          "native_token": {
            "denom": "ibc/27394FB092D2ECCD56123C74F36E4C1F926001CEADA9CA97EA622B25F41E5EB2"
          }
        },
        {
          "native_token": {
            "denom": "ibc/B3504E092456BA618CC28AC671A71FB08C6CA0FD0BE7C8A5B5A3E2DD933CC9E4"
          }
        }
      ],
      "pool_address": "terra17l9xj8f6m8smumhn8wgpgnswr3mu60wfkcm6pjc69drxp0t398rs7335vn",
      "lp_asset": {
        "token": {
          "contract_addr": "terra17ly9laewec70qu6tl0e3qrwh2vhz9akpf2jd7mxqram63xg2n0rsj36xvr"
        }
      },
      "incentive_contract": "terra1jjkwz5fluaa87a4w5xd2yku8c6vrqsuhrt9yaax3pyhfl5ftp9wsy6na3x",
      "pool_code_id": "2609",
      "lp_code_id": "726"
    },
    {
      "pair": "uatom-uluna",
      "assets": [
        {
          "native_token": {
            "denom": "ibc/27394FB092D2ECCD56123C74F36E4C1F926001CEADA9CA97EA622B25F41E5EB2"
          }
        },
        {
          "native_token": {
            "denom": "uluna"
          }
        }
      ],
      "pool_address": "terra1frfcj4xhvx0emkup4vel5jun9zun0797j5yhn7ant3r4jzy9mkxqzcwev6",
      "lp_asset": {
        "token": {
          "contract_addr": "terra1adp223mw8937arxcfl36acjjyn2dcf7wzp8h09jek5k0gw3vch8sqlq6su"
        }
      },
      "incentive_contract": "terra1zwk4ajwy9v7tugqvfyldl8f3sj8uev7naafpelfd4jftx9czsxxsm0ncw5",
      "pool_code_id": "2609",
      "lp_code_id": "726"
    },
    {
      "pair": "boneWhale-uwhale",
      "assets": [
        {
          "native_token": {
            "denom": "ibc/517E13F14A1245D4DE8CF467ADD4DA0058974CDCC880FA6AE536DBCA1D16D84E"
          }
        },
        {
          "native_token": {
            "denom": "ibc/36A02FFC4E74DF4F64305130C3DFA1B06BEAC775648927AA44467C76A77AB8DB"
          }
        }
      ],
      "pool_address": "terra1j9jmsplecj9ay2py27953p84nfmv7f6ce75ms5fleyhd0aecpc7q0hgmsa",
      "lp_asset": {
        "token": {
          "contract_addr": "terra1le46uu9qjk53aktjs8dev96sl9sd2ujvcpspk75pdeg0txfvhyuswm6653"
        }
      },
      "incentive_contract": "terra1avs33y34j9t23e6ujuzpa5x58ru0cfk4c5nglm5l0etn7vaq6h8qhszt66",
      "pool_code_id": "2609",
      "lp_code_id": "726"
    },
    {
      "pair": "uwhale-uusdc",
      "assets": [
        {
          "native_token": {
            "denom": "ibc/36A02FFC4E74DF4F64305130C3DFA1B06BEAC775648927AA44467C76A77AB8DB"
          }
        },
        {
          "native_token": {
            "denom": "ibc/B3504E092456BA618CC28AC671A71FB08C6CA0FD0BE7C8A5B5A3E2DD933CC9E4"
          }
        }
      ],
      "pool_address": "terra1qdu4g5zxxtmwsd95v8vjslq5874nkcull7ejycm0gy2v7p5qc67qenkf8t",
      "lp_asset": {
        "token": {
          "contract_addr": "terra1necjy4mmes4fvsvjvne5kkl3zhszg7s3s3jayfgzudsshnpv69kss5m2k2"
        }
      },
      "incentive_contract": "terra1hnd5e4w9q7afmj3ql7nam5qna978qapmts839hfuvuueeq6f5lgqykrejn",
      "pool_code_id": "2609",
      "lp_code_id": "726"
    },
    {
      "pair": "ampWHALE-uwhale",
      "assets": [
        {
          "native_token": {
            "denom": "ibc/B3F639855EE7478750CC8F82072307ED6E131A8EFF20345E1D136B50C4E5EC36"
          }
        },
        {
          "native_token": {
            "denom": "ibc/36A02FFC4E74DF4F64305130C3DFA1B06BEAC775648927AA44467C76A77AB8DB"
          }
        }
      ],
      "pool_address": "terra1ntx595elf3ukxcd0wy76h24rzztcv2p6n3wmfd358ks95prv42fs9mn63n",
      "lp_asset": {
        "token": {
          "contract_addr": "terra16z3ksy6aqjkug8l3u48q0kvdaqk3dgaytl7ykt6vg2he9d6z9rgslr4k7l"
        }
      },
      "incentive_contract": "terra19a63jwphxh2f8j8r5cn74kyrrjlu35gk4h4y7uj9zam8lquqrnzsjtxlhl",
      "pool_code_id": "2609",
      "lp_code_id": "726"
    },
    {
      "pair": "uluna-uwhale",
      "assets": [
        {
          "native_token": {
            "denom": "uluna"
          }
        },
        {
          "native_token": {
            "denom": "ibc/36A02FFC4E74DF4F64305130C3DFA1B06BEAC775648927AA44467C76A77AB8DB"
          }
        }
      ],
      "pool_address": "terra1zushwxgqdkg22mtv9p946yp53r6den6lv427esjaadua3ftzyjpsqgtl5z",
      "lp_asset": {
        "native_token": {
          "denom": "factory/terra1zushwxgqdkg22mtv9p946yp53r6den6lv427esjaadua3ftzyjpsqgtl5z/uLP"
        }
      },
      "incentive_contract": "terra12gzs5fezplmeg0gpz5wxw28fmssu398a362r95u2uj3cmdfqm3gqcsz96k",
      "pool_code_id": "2609",
      "lp_code_id": "726"
    },
    {
      "pair": "uwhale-ROAR",
      "assets": [
        {
          "native_token": {
            "denom": "ibc/36A02FFC4E74DF4F64305130C3DFA1B06BEAC775648927AA44467C76A77AB8DB"
          }
        },
        {
          "token": {
            "contract_addr": "terra1lxx40s29qvkrcj8fsa3yzyehy7w50umdvvnls2r830rys6lu2zns63eelv"
          }
        }
      ],
      "pool_address": "terra1g8clplgv3ah405qjrf9yhkgur9zqlqayt8ftrvkuzsm5am7pr9ls7s26rx",
      "lp_asset": {
        "token": {
          "contract_addr": "terra1j7zej67gl6kjmgc2tl2hggp4xcvchnrn5reffc489u6ffsvm7aeq5k4sas"
        }
      },
      "incentive_contract": "terra1y967zn8xhlx3k67c8quaatqxaugw9kmvu2pu4tddk2rjxhcfegaqvdvtv7",
      "pool_code_id": "2609",
      "lp_code_id": "726"
    },
    {
      "pair": "uluna-uusdc",
      "assets": [
        {
          "native_token": {
            "denom": "uluna"
          }
        },
        {
          "native_token": {
            "denom": "ibc/B3504E092456BA618CC28AC671A71FB08C6CA0FD0BE7C8A5B5A3E2DD933CC9E4"
          }
        }
      ],
      "pool_address": "terra1ck8nkz35sa8mmqez3lqrm77vh36n2gd2f0dxjde4uemkwsjt22pqgk49zj",
      "lp_asset": {
        "token": {
          "contract_addr": "terra1rlmjwapg7y3p39aucq2rq5rffyns7z94twm8acl59na4d9aehu9sl2dfkc"
        }
      },
      "incentive_contract": "terra1guwyktv5uhjkvmnmtvrwevgpgcl3f4zzy74959whju8qglrc66fqgrqs40",
      "pool_code_id": "2609",
      "lp_code_id": "726"
    },
    {
      "pair": "uluna-ASTRO",
      "assets": [
        {
          "native_token": {
            "denom": "uluna"
          }
        },
        {
          "token": {
            "contract_addr": "terra1nsuqsk6kh58ulczatwev87ttq2z6r3pusulg9r24mfj2fvtzd4uq3exn26"
          }
        }
      ],
      "pool_address": "terra1e6t37fgjkxrzdx2s95fyq6jdra5s82720vhtmxvx4yhcvnsrey4ssmrya6",
      "lp_asset": {
        "token": {
          "contract_addr": "terra19glrs2vtgxaxww39cq5acxapgv2v8hyw562zmsk7ucn4yznmyv3sljewv9"
        }
      },
      "incentive_contract": "terra1valpnysajk756uwesegkfeq6gqt9ld8ez8ke247ghhpfh4wjjgase0hhl8",
      "pool_code_id": "2609",
      "lp_code_id": "726"
    },
    {
      "pair": "uluna-LunaX",
      "assets": [
        {
          "native_token": {
            "denom": "uluna"
          }
        },
        {
          "token": {
            "contract_addr": "terra14xsm2wzvu7xaf567r693vgfkhmvfs08l68h4tjj5wjgyn5ky8e2qvzyanh"
          }
        }
      ],
      "pool_address": "terra1qzux5j9he9nv95kq3unkuzy0hddf080um2t243raatg3f6requwsaahpqp",
      "lp_asset": {
        "token": {
          "contract_addr": "terra1lt586fhwyuccktk58v8k96ugzp9szurhqvmlnjxhyn6yapa6v2jsmc468d"
        }
      },
      "incentive_contract": "terra1u8qcwwxychcpf6m0gtecyu46m8fjvzu8t7wdhxa7k3vwtlw6vmrq96cg0k",
      "pool_code_id": "2609",
      "lp_code_id": "726"
    },
    {
      "pair": "ampLUNA-uluna",
      "assets": [
        {
          "token": {
            "contract_addr": "terra1ecgazyd0waaj3g7l9cmy5gulhxkps2gmxu9ghducvuypjq68mq2s5lvsct"
          }
        },
        {
          "native_token": {
            "denom": "uluna"
          }
        }
      ],
      "pool_address": "terra1tsx0dmasjvd45k6tdywzv77d5t9k3lpzyuleavuah77pg3lwm9cq4469pm",
      "lp_asset": {
        "token": {
          "contract_addr": "terra10un5hr6asmn7g0ggh9sz0x3v8f9evh5cvawk8xs65rghundc25mq7g5par"
        }
      },
      "incentive_contract": "terra1aw872zyt2y0qzzxn7x00mefympk5n9at04mmfmmxqpe42ev2pj0qax89d8",
      "pool_code_id": "2609",
      "lp_code_id": "726"
    },
    {
      "pair": "bLUNA-uluna",
      "assets": [
        {
          "token": {
            "contract_addr": "terra17aj4ty4sz4yhgm08na8drc0v03v2jwr3waxcqrwhajj729zhl7zqnpc0ml"
          }
        },
        {
          "native_token": {
            "denom": "uluna"
          }
        }
      ],
      "pool_address": "terra1j5znhs9jeyty9u9jcagl3vefkvzwqp6u9tq9a3e5qrz4gmj2udyqp0z0xc",
      "lp_asset": {
        "token": {
          "contract_addr": "terra1q475uvk9te5nxq2lzu0h96t0devmx4v8ctxqtm253ut05wrpugsq0m4e3k"
        }
      },
      "incentive_contract": "terra10vu0f9nknuhj89xq00aymqxxypmztgx8hwty5jj7cutnkx4j5sjshagm9a",
      "pool_code_id": "2609",
      "lp_code_id": "726"
    },
    {
      "pair": "bLUNA-SOLID",
      "assets": [
        {
          "token": {
            "contract_addr": "terra17aj4ty4sz4yhgm08na8drc0v03v2jwr3waxcqrwhajj729zhl7zqnpc0ml"
          }
        },
        {
          "token": {
            "contract_addr": "terra10aa3zdkrc7jwuf8ekl3zq7e7m42vmzqehcmu74e4egc7xkm5kr2s0muyst"
          }
        }
      ],
      "pool_address": "terra1shd0wd8atmevjtryzcqzu6sxsmc4hjek43kxqsz08wxwk4nt0wvsav9004",
      "lp_asset": {
        "token": {
          "contract_addr": "terra19sddeagdmflr7fh4tqkj37chv6zjpef2nnvfzfjlykwz0zvg6f4scvy5dr"
        }
      },
      "incentive_contract": "null",
      "pool_code_id": "2609",
      "lp_code_id": "726"
    }
  ]
}
```

```json
{
  "chain": "phoenix-1",
  "vault_factory_addr": "terra1vcn8h6fc26nv4f20p6g870a00nqzdpjwvshud9ku3qfaqhv7l69s9l29y2",
  "vaults": [
    {
      "vault": "terra1clwlcv2kekklzxdud2d938d0kyrgjryvr4a86qfal4n7wjerxrvsey7ch9",
      "asset": {
        "native_token": {
          "denom": "uluna"
        }
      },
      "lp_asset": {
        "token": {
          "contract_addr": "terra1pm6s5x770t27xajnj2qqkn6mku8s4k44ujs0m53h9epqqcarulnqwva8nt"
        }
      },
      "vault_code_id": "1453",
      "lp_code_id": "726"
    }
  ]
}
```

# Terra testnet (pisco-1)

```json
{
  "contracts": [
    {
      "wasm": "fee_collector.wasm",
      "code_id": "5202",
      "version": "1.0.3",
      "contract_address": "terra1ldqxud3myhfluw0y0ds0swdftqsj4fhkss9ge4y28cz3yy93rqksvvc7ut"
    },
    {
      "wasm": "terraswap_factory.wasm",
      "code_id": "5203",
      "version": "1.0.4",
      "contract_address": "terra15d7gjn0rtu93nxkjt7kqj0sz62gcgy7p5srjeefp74hjsyjry9uqdz5zc7"
    },
    {
      "wasm": "terraswap_pair.wasm",
      "code_id": "5204",
      "version": "1.0.1"
    },
    {
      "wasm": "terraswap_router.wasm",
      "code_id": "5205",
      "version": "1.0.0",
      "contract_address": "terra1ssrdlwawevh52k2dr6r25aeflgzcnwm097gqlga4tee7au35a4ss4wkdxw"
    },
    {
      "wasm": "terraswap_token.wasm",
      "code_id": "5206",
      "version": "1.0.1"
    },
    {
      "wasm": "vault_factory.wasm",
      "code_id": "5207",
      "version": "1.0.7",
      "contract_address": "terra1je4wvk8cfzdvxvtfp2sg4vfh0sw6vgu6penuye0rlhqmkmczxqus4ksgdd"
    },
    {
      "wasm": "vault_router.wasm",
      "code_id": "5208",
      "version": "1.0.0",
      "contract_address": "terra1kjwf4ft34g8m7naxexgzh4mg9d82kyc49w2rz9hd8djp2vdlhdnqfh2w4e"
    },
    {
      "wasm": "vault.wasm",
      "code_id": "5209",
      "version": "1.1.1"
    }
  ],
  "date": "2022-10-28T11:50:45+0000",
  "initial_block_height": "2445856",
  "final_block_height": "2445856",
  "chain_id": "pisco-1",
  "deployer_address": "terra1rmzydhhpgqpr3v8sfu82ewj7fj9rl6sfnnrcu8"
}
```

```json
{
  "pools": [
    {
      "pair": "lunafour-lunafive",
      "assets": [
        "{\"token\":{\"contract_addr\":\"terra1e8sqchdyrgtgf2jwsq0jerj0gp0wkezelj9sjw98z22g3s0v0qrqjwr39u\"}}",
        "{\"token\":{\"contract_addr\":\"terra1rzvdn9cc7efpqsgl4ha7q5egqlpnyfdkgu0at6fkzmmj9dr7aspsy4a5js\"}}"
      ],
      "pool_address": "terra1x0v3qrgtg4gvku6hcdu28mgaadp7cdu8kntk5v04wlxx8qgnm7gqg64y55",
      "lp_address": "terra1497udqamdn53kqlc0gkxje8zje66du6edtxfa2dwz52plr0g48ssz34syx",
      "pool_code_id": "5204",
      "lp_code_id": "5206"
    }
  ],
  "date": "2022-11-02T14:43:09+0000",
  "chain_id": "pisco-1",
  "pool_factory_addr": "terra15d7gjn0rtu93nxkjt7kqj0sz62gcgy7p5srjeefp74hjsyjry9uqdz5zc7"
}
```