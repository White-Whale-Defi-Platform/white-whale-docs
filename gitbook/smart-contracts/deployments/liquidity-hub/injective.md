# Injective (injective-1)

```json
{
  "contracts": [
    {
      "wasm": "fee_collector.wasm",
      "code_id": "162",
      "version": "1.1.2",
      "contract_address": "inj1g6kht9c5s4jwn4akfjt3zmsfh4nvguewuevmk0"
    },
    {
      "wasm": "fee_distributor.wasm",
      "code_id": "163",
      "version": "0.9.1",
      "contract_address": "inj1s0q949jwm6n502sspvjmnaj4zjuv36fzpl33rr"
    },
    {
      "wasm": "frontend_helper.wasm",
      "code_id": "164",
      "version": "1.0.0",
      "contract_address": "inj1fwfudkjv95qtj9h32agcfwpg0wwzz352jlyk58"
    },
    {
      "wasm": "incentive.wasm",
      "code_id": "156",
      "version": "1.0.6"
    },
    {
      "wasm": "incentive_factory.wasm",
      "code_id": "155",
      "version": "1.0.1",
      "contract_address": "inj189rhgt2d78a7djv0x6mulwy7kre07n9x3z72nd"
    },
    {
      "wasm": "stableswap_3pool.wasm",
      "code_id": "157",
      "version": "1.2.2"
    },
    {
      "wasm": "terraswap_factory.wasm",
      "code_id": "165",
      "version": "1.2.0",
      "contract_address": "inj1x22q8lfhz7qcvtzs0dakhgx2th64l79kfye5lk"
    },
    {
      "wasm": "terraswap_pair.wasm",
      "code_id": "161",
      "version": "1.3.3"
    },
    {
      "wasm": "terraswap_router.wasm",
      "code_id": "166",
      "version": "1.1.1",
      "contract_address": "inj1657pee2jhf4jk8pq6yq64e758ngvum45nft8rf"
    },
    {
      "wasm": "terraswap_token.wasm",
      "code_id": "17",
      "version": "1.0.2"
    },
    {
      "wasm": "vault_factory.wasm",
      "code_id": "160",
      "version": "1.1.3",
      "contract_address": "inj1wastjc07zuuy46mzzl3egz4uzy6fs59758vrwr"
    },
    {
      "wasm": "vault.wasm",
      "code_id": "158",
      "version": "1.2.6"
    },
    {
      "wasm": "vault_router.wasm",
      "code_id": "159",
      "version": "1.1.6",
      "contract_address": "inj1hyja4uyjktpeh0fxzuw2fmjudr85rk2qxgqkvu"
    },
    {
      "wasm": "whale_lair.wasm",
      "code_id": "167",
      "version": "0.9.1",
      "contract_address": "inj1vz5g8pfdk4pjjhnf8vy000nq7evc2kgnfmrxt9"
    }
  ],
  "date": "2023-10-30T13:43:00+0000",
  "initial_block_height": "null",
  "final_block_height": "21861859",
  "chain_id": "injective-1",
  "deployer_address": "inj1xzzu4jt274zzj0w9c3szg5u0mz68y0m7de7ftw"
}
```

```json
{
  "pools": [
    {
      "pair": "ampWHALE-uwhale",
      "assets": [
        {
          "native_token": {
            "denom": "ibc/168C3904C45C6FE3539AE85A8892DF87371D00EA7942515AFC50AA43C4BB0A32"
          }
        },
        {
          "native_token": {
            "denom": "ibc/D6E6A20ABDD600742D22464340A7701558027759CE14D12590F8EA869CCCF445"
          }
        }
      ],
      "pool_address": "inj1gyxlm5j537d8pvl5eqfswya93delvh3nlhustk",
      "lp_asset": {
        "token": {
          "contract_addr": "inj185gqewrlde8vrqw7j8lpad67v8jfrx9u28w38t"
        }
      },
      "incentive_contract": "inj12x7vzmsgj496ps0n9gt0xzmec0vw2wgvqgjxys",
      "pool_code_id": "161",
      "lp_code_id": "17"
    },
    {
      "pair": "uatom-peggy0xdAC17F958D2ee523a2206206994597C13D831ec7",
      "assets": [
        {
          "native_token": {
            "denom": "ibc/C4CFF46FD6DE35CA4CF4CE031E643C8FDC9BA4B99AE598E9B0ED98FE3A2319F9"
          }
        },
        {
          "native_token": {
            "denom": "peggy0xdAC17F958D2ee523a2206206994597C13D831ec7"
          }
        }
      ],
      "pool_address": "inj14zykjnz94dr9nj4v2yzpvnlrw5uurk5hhea8xw",
      "lp_asset": {
        "token": {
          "contract_addr": "inj1j30wx6kjfsessdx5mlp32hqwklj48ufvxx6tyc"
        }
      },
      "incentive_contract": "inj1r7tm9zndwyw898hjt3xgmdecugret22vc3ecdw",
      "pool_code_id": "161",
      "lp_code_id": "17"
    },
    {
      "pair": "boneWhale-uwhale",
      "assets": [
        {
          "native_token": {
            "denom": "ibc/ECB0AA28D6001EF985047558C410B65581FC85BD92D4E3CFCCA0D3D964C67CC2"
          }
        },
        {
          "native_token": {
            "denom": "ibc/D6E6A20ABDD600742D22464340A7701558027759CE14D12590F8EA869CCCF445"
          }
        }
      ],
      "pool_address": "inj17dez7atlgwrl7lxzszxjy7gzuj325n8re3f7mh",
      "lp_asset": {
        "token": {
          "contract_addr": "inj1a6tcf60pyz8qq2n532dzcs7s7sj8klcmj94nhd"
        }
      },
      "incentive_contract": "inj10udnevccyg50e80gkeynr0s9gx70j699jgepzl",
      "pool_code_id": "161",
      "lp_code_id": "17"
    },
    {
      "pair": "inj-uwhale",
      "assets": [
        {
          "native_token": {
            "denom": "inj"
          }
        },
        {
          "native_token": {
            "denom": "ibc/D6E6A20ABDD600742D22464340A7701558027759CE14D12590F8EA869CCCF445"
          }
        }
      ],
      "pool_address": "inj109ptsw60g2mx69guq0rzurvsw7krpcjzht3p5l",
      "lp_asset": {
        "token": {
          "contract_addr": "inj126raxkq6fvpqearfjpx3exa6rg26c6m7367de6"
        }
      },
      "incentive_contract": "inj1kgssa2jy5ygzealwvuaat8x8zytjv3f6j0tlqv",
      "pool_code_id": "161",
      "lp_code_id": "17"
    },
    {
      "pair": "peggy0xdAC17F958D2ee523a2206206994597C13D831ec7-uwhale",
      "assets": [
        {
          "native_token": {
            "denom": "peggy0xdAC17F958D2ee523a2206206994597C13D831ec7"
          }
        },
        {
          "native_token": {
            "denom": "ibc/D6E6A20ABDD600742D22464340A7701558027759CE14D12590F8EA869CCCF445"
          }
        }
      ],
      "pool_address": "inj1t9daxn85sz688vkn8wu4w47jnrak296hh2q579",
      "lp_asset": {
        "token": {
          "contract_addr": "inj1869zena97sctemj78sgjmu737p2g9490esftk5"
        }
      },
      "incentive_contract": "inj1f9j7u5mf8lzgkqqyx00mkeze2nlk9sqf0hv35d",
      "pool_code_id": "161",
      "lp_code_id": "17"
    },
    {
      "pair": "inj-peggy0xdAC17F958D2ee523a2206206994597C13D831ec7",
      "assets": [
        {
          "native_token": {
            "denom": "inj"
          }
        },
        {
          "native_token": {
            "denom": "peggy0xdAC17F958D2ee523a2206206994597C13D831ec7"
          }
        }
      ],
      "pool_address": "inj1zfw930csx0k5qzf35vndaulwada4wa3pywekyx",
      "lp_asset": {
        "token": {
          "contract_addr": "inj14n26cr7dj79smrgg44hfylhph9y45h4yx5gvzm"
        }
      },
      "incentive_contract": "inj1pm4vll4c0q5y6q0qcvvx94377tq670k5gdyuyg",
      "pool_code_id": "161",
      "lp_code_id": "17"
    }
  ]
}
```

```json
{
  "vaults": [
    {
      "asset": "peggy0xdAC17F958D2ee523a2206206994597C13D831ec7",
      "vault_address": "inj17kfjhj8mf7l5qus4kjqxtxext2rtnpqzdjz2qm",
      "lp_address": "inj1s66zhks8v3fm24974crzxufh7w6ktt694g9t3j",
      "vault_code_id": "158",
      "lp_code_id": "17"
    }
  ],
  "date": "2022-12-18T16:02:30+0000",
  "chain_id": "injective-1",
  "vault_factory_addr": "inj1wastjc07zuuy46mzzl3egz4uzy6fs59758vrwr",
  "vault_router_addr": "inj1hyja4uyjktpeh0fxzuw2fmjudr85rk2qxgqkvu"
}
```

```json
{
  "pool_incentives": [
    {
      "pool": "inj1gyxlm5j537d8pvl5eqfswya93delvh3nlhustk",
      "pool_label": "ibc/168C...0A32-ibc/D6E6...F445",
      "incentive_contract": "inj12x7vzmsgj496ps0n9gt0xzmec0vw2wgvqgjxys"
    },
    {
      "pool": "inj14zykjnz94dr9nj4v2yzpvnlrw5uurk5hhea8xw",
      "pool_label": "ibc/C4CF...19F9-peggy0xdAC...ec7",
      "incentive_contract": "inj1r7tm9zndwyw898hjt3xgmdecugret22vc3ecdw"
    },
    {
      "pool": "inj17dez7atlgwrl7lxzszxjy7gzuj325n8re3f7mh",
      "pool_label": "ibc/ECB0...7CC2-ibc/D6E6...F445",
      "incentive_contract": "inj10udnevccyg50e80gkeynr0s9gx70j699jgepzl"
    },
    {
      "pool": "inj1t9daxn85sz688vkn8wu4w47jnrak296hh2q579",
      "pool_label": "peggy0xdAC...ec7-ibc/D6E6...F445",
      "incentive_contract": "inj1f9j7u5mf8lzgkqqyx00mkeze2nlk9sqf0hv35d"
    },
    {
      "pool": "inj1zfw930csx0k5qzf35vndaulwada4wa3pywekyx",
      "pool_label": "inj-peggy0xdAC...ec7",
      "incentive_contract": "inj1pm4vll4c0q5y6q0qcvvx94377tq670k5gdyuyg"
    }
  ],
  "date": "2023-10-30T13:53:00+0000",
  "initial_block_height": "49751492",
  "final_block_height": "49751534",
  "chain_id": "injective-1",
  "deployer_address": "inj189rhgt2d78a7djv0x6mulwy7kre07n9x3z72nd"
}
```

# Injective testnet (injective-888)

```json
{
  "contracts": [
    {
      "wasm": "fee_collector.wasm",
      "code_id": "186",
      "version": "1.0.4",
      "contract_address": "inj1cuja0pknl3adngs4nnqa7nhrjx59q3ty65nhl8"
    },
    {
      "wasm": "terraswap_factory.wasm",
      "code_id": "187",
      "version": "1.1.1",
      "contract_address": "inj1e40kslczvwzset7c20p92pg3hzhuesms4j96f2"
    },
    {
      "wasm": "terraswap_pair.wasm",
      "code_id": "188",
      "version": "1.1.0"
    },
    {
      "wasm": "terraswap_router.wasm",
      "code_id": "189",
      "version": "1.0.5",
      "contract_address": "inj1ckqz4r0n3m9smvharm65pgu8mm7vhep8cq89mg"
    },
    {
      "wasm": "terraswap_token.wasm",
      "code_id": "190",
      "version": "1.0.2"
    },
    {
      "wasm": "vault_factory.wasm",
      "code_id": "191",
      "version": "1.0.8",
      "contract_address": "inj1u7jy0sm42elyuuspsw29pclm6030hsv6htqydc"
    },
    {
      "wasm": "vault.wasm",
      "code_id": "193",
      "version": "1.1.3"
    },
    {
      "wasm": "vault_router.wasm",
      "code_id": "192",
      "version": "1.1.2",
      "contract_address": "inj188nerzufmt69sujawrxz6ekx7duvjzv4p8f77c"
    }
  ],
  "date": "2022-12-01T09:57:00+0000",
  "chain_id": "injective-888",
  "deployer_address": "inj1k433snt7qdn8tztuhf2wh90uyze2ga3hwpfsug"
}
```

```json
{
  "pools": [
    {
      "pair": "inj-cwshib",
      "assets": [
        "{\"native_token\":{\"denom\":\"inj\"}}",
        "{\"token\":{\"contract_addr\":\"inj1dlg3xhqnhfucarxkjj8khlgrnx988cdjjsmasc\"}}"
      ],
      "pool_address": "inj1jjun9me022r589ytezhhrs29es8a2fwk9hgpyq",
      "lp_address": "inj1qr6srl0egqqyw4jdeqqm8xusclhef0epuvx8j7",
      "pool_code_id": "188",
      "lp_code_id": "190"
    },
    {
      "pair": "cwshib-cwsix",
      "assets": [
        "{\"token\":{\"contract_addr\":\"inj1dlg3xhqnhfucarxkjj8khlgrnx988cdjjsmasc\"}}",
        "{\"token\":{\"contract_addr\":\"inj14efstake5h3kah7wezkxwvqqv4ew6ahlht0qfz\"}}"
      ],
      "pool_address": "inj19tq8qe983z5fjhh0y4ym0276dm8al3entjjxhj",
      "lp_address": "inj16twsluegh25h7syt9yyraq4wqt2zf4js96vhfc",
      "pool_code_id": "188",
      "lp_code_id": "190"
    },
    {
      "pair": "inj-usdt",
      "assets": [
        "{\"native_token\":{\"denom\":\"inj\"}}",
        "{\"native_token\":{\"denom\":\"peggy0x87aB3B4C8661e07D6372361211B96ed4Dc36B1B5\"}}"
      ],
      "pool_address": "inj1yjayfr08tu5sl5uajsylh3kwntzc46zfkn7ua4",
      "lp_address": "inj129pns8jnlpth8pe0ualamv4m7lgtj8qsrrm2av",
      "pool_code_id": "188",
      "lp_code_id": "190"
    }
  ],
  "date": "2022-12-01T10:07:00+0000",
  "chain_id": "injective-888",
  "pool_factory_addr": "inj1e40kslczvwzset7c20p92pg3hzhuesms4j96f2"
}
```

```json
{
  "vaults": [
    {
      "asset": "inj",
      "vault_address": "inj1hufvs90dpstkdg9ly3uy4v78nwgz3yapn0cm0y",
      "lp_address": "inj1cwwrqju43ztnleqsv26pcxn2d9kfgs09t8pf7x",
      "vault_code_id": "193",
      "lp_code_id": "190"
    },
    {
      "asset": "peggy0x87aB3B4C8661e07D6372361211B96ed4Dc36B1B5",
      "vault_address": "inj1ncs3cft6qzw40d5y8kdvqrml2lj5jpuxx6jzp7",
      "lp_address": "inj1ze8msxgzx0y0p5l3e4pdjd9qtwgg9wdxq5zjce",
      "vault_code_id": "194",
      "lp_code_id": "190"
    },
    {
      "asset": "inj1dlg3xhqnhfucarxkjj8khlgrnx988cdjjsmasc",
      "vault_address": "inj19tmd50964wxfvfcrjem7falnxpg669cuv9sz35",
      "lp_address": "inj1stvpkzqja5rt5c3s380kv6swfut6jnrcka7xcz",
      "vault_code_id": "194",
      "lp_code_id": "190"
    }
  ],
  "date": "2022-12-01T10:15:42+0000",
  "chain_id": "injective-888",
  "vault_factory_addr": "inj1u7jy0sm42elyuuspsw29pclm6030hsv6htqydc"
}
```