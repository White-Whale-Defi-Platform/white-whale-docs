# Terra (phoenix-1)

```json
{
  "contracts": [
    {
      "wasm": "fee_collector.wasm",
      "code_id": "1423",
      "version": "1.1.0",
      "contract_address": "terra1w8402njz8936ag4rlcmvek4zcns6hlkaapsd4qwz5us0ewwyghrsx7k47w"
    },
    {
      "wasm": "fee_distributor.wasm",
      "code_id": "1429",
      "version": "0.8.1",
      "contract_address": "terra1xm0yh8cv8rww6g87h3q0megt6ntxqzw6p6hgh5l4jrhed4fe7hnq9cvzm5"
    },
    {
      "wasm": "stableswap_3pool.wasm",
      "code_id": "1450",
      "version": "1.2.0"
    },
    {
      "wasm": "terraswap_factory.wasm",
      "code_id": "1444",
      "version": "1.2.0",
      "contract_address": "terra1f4cr4sr5eulp3f2us8unu6qv8a5rhjltqsg7ujjx6f2mrlqh923sljwhn3"
    },
    {
      "wasm": "terraswap_pair.wasm",
      "code_id": "1445",
      "version": "1.3.0"
    },
    {
      "wasm": "terraswap_router.wasm",
      "code_id": "1446",
      "version": "1.1.0",
      "contract_address": "terra1p37jrwlaqpklzlu4rwjyjrmzuezdgk3pyuyk2zclc4rda6awkm3qnj6f0a"
    },
    {
      "wasm": "terraswap_token.wasm",
      "code_id": "726",
      "version": "1.0.2"
    },
    {
      "wasm": "vault_factory.wasm",
      "code_id": "1452",
      "version": "1.1.2",
      "contract_address": "terra1vcn8h6fc26nv4f20p6g870a00nqzdpjwvshud9ku3qfaqhv7l69s9l29y2"
    },
    {
      "wasm": "vault.wasm",
      "code_id": "1453",
      "version": "1.2.2"
    },
    {
      "wasm": "vault_router.wasm",
      "code_id": "1451",
      "version": "1.1.5",
      "contract_address": "terra1c8tpvta3umr4mpufvxmq39gyuw2knpyxyfgq8thpaeyw2r6a80qsg5wa00"
    },
    {
      "wasm": "whale_lair.wasm",
      "code_id": "1438",
      "version": "0.8.2",
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
  "pools": [
    {
      "pair": "ATOM-LUNA",
      "label": "ibc/2739...5EB2-uluna pair",
      "contract": "terra1frfcj4xhvx0emkup4vel5jun9zun0797j5yhn7ant3r4jzy9mkxqzcwev6",
      "lp_token": "terra1adp223mw8937arxcfl36acjjyn2dcf7wzp8h09jek5k0gw3vch8sqlq6su"
    },
    {
      "pair": "ATOM-JUNO",
      "label": "ibc/2739...5EB2-ibc/4CD5...3D04 pair",
      "contract": "terra1p2xgcr2ewnetug8ahqms5y3k6rxyh2xglnzzx500ylh4420h9ucqz8w7x5",
      "lp_token": "terra1avfsch3ee82wyrpwlawecyz6zktr9jln0zaxp58xuvmxyl5g305q3rwuj3"
    },
    {
      "pair": "ATOM-axlUSDC",
      "label": "ibc/2739...5EB2-ibc/B350...C9E4 pair",
      "contract": "terra17l9xj8f6m8smumhn8wgpgnswr3mu60wfkcm6pjc69drxp0t398rs7335vn",
      "lp_token": "terra17ly9laewec70qu6tl0e3qrwh2vhz9akpf2jd7mxqram63xg2n0rsj36xvr"
    },
    {
      "pair": "LUNA-LUNAX",
      "label": "uluna-LunaX pair",
      "contract": "terra1qzux5j9he9nv95kq3unkuzy0hddf080um2t243raatg3f6requwsaahpqp",
      "lp_token": "terra1lt586fhwyuccktk58v8k96ugzp9szurhqvmlnjxhyn6yapa6v2jsmc468d"
    },
    {
      "pair": "LUNA-ASTRO",
      "label": "uluna-ASTRO pair",
      "contract": "terra1e6t37fgjkxrzdx2s95fyq6jdra5s82720vhtmxvx4yhcvnsrey4ssmrya6",
      "lp_token": "terra19glrs2vtgxaxww39cq5acxapgv2v8hyw562zmsk7ucn4yznmyv3sljewv9"
    },
    {
      "pair": "LUNA-axlUSDC",
      "label": "uluna-ibc/B350...C9E4 pair",
      "contract": "terra1ck8nkz35sa8mmqez3lqrm77vh36n2gd2f0dxjde4uemkwsjt22pqgk49zj",
      "lp_token": "terra1rlmjwapg7y3p39aucq2rq5rffyns7z94twm8acl59na4d9aehu9sl2dfkc"
    },
    {
      "pair": "WHALE-axlUSDC",
      "label": "ibc/36A0...B8DB-ibc/B350...C9E4 pair",
      "contract": "terra1qdu4g5zxxtmwsd95v8vjslq5874nkcull7ejycm0gy2v7p5qc67qenkf8t",
      "lp_token": "terra1necjy4mmes4fvsvjvne5kkl3zhszg7s3s3jayfgzudsshnpv69kss5m2k2"
    },
    {
      "pair": "ampWHALE-WHALE",
      "label": "ibc/B3F6...EC36-ibc/36A0...B8DB pair",
      "contract": "terra1ntx595elf3ukxcd0wy76h24rzztcv2p6n3wmfd358ks95prv42fs9mn63n",
      "lp_token": "terra16z3ksy6aqjkug8l3u48q0kvdaqk3dgaytl7ykt6vg2he9d6z9rgslr4k7l"
    },
    {
      "pair": "boneWHALE-WHALE",
      "label": "ibc/517E...D84E-ibc/36A0...B8DB pair",
      "contract": "terra1j9jmsplecj9ay2py27953p84nfmv7f6ce75ms5fleyhd0aecpc7q0hgmsa",
      "lp_token": "terra1le46uu9qjk53aktjs8dev96sl9sd2ujvcpspk75pdeg0txfvhyuswm6653"
    },
    {
      "pair": "ampLUNA-LUNA",
      "label": "ampLUNA-uluna pair",
      "contract": "terra1tsx0dmasjvd45k6tdywzv77d5t9k3lpzyuleavuah77pg3lwm9cq4469pm",
      "lp_token": "terra10un5hr6asmn7g0ggh9sz0x3v8f9evh5cvawk8xs65rghundc25mq7g5par"
    },
    {
      "pair": "bLUNA-LUNA",
      "label": "bLUNA-uluna pair",
      "contract": "terra1j5znhs9jeyty9u9jcagl3vefkvzwqp6u9tq9a3e5qrz4gmj2udyqp0z0xc",
      "lp_token": "terra1q475uvk9te5nxq2lzu0h96t0devmx4v8ctxqtm253ut05wrpugsq0m4e3k"
    },
    {
      "pair": "bLUNA-SOLID",
      "label": "bLUNA-SOLID pair",
      "contract": "terra1shd0wd8atmevjtryzcqzu6sxsmc4hjek43kxqsz08wxwk4nt0wvsav9004",
      "lp_token": "terra19sddeagdmflr7fh4tqkj37chv6zjpef2nnvfzfjlykwz0zvg6f4scvy5dr"
    }
  ],
  "date": "2022-08-25T11:52:10+0000",
  "chain_id": "phoenix-1",
  "pool_factory_address": "terra1f4cr4sr5eulp3f2us8unu6qv8a5rhjltqsg7ujjx6f2mrlqh923sljwhn3"
}
```

```json
{
  "vaults": [
    {
      "asset": "uluna",
      "vault_address": "terra1clwlcv2kekklzxdud2d938d0kyrgjryvr4a86qfal4n7wjerxrvsey7ch9",
      "lp_address": "terra1pm6s5x770t27xajnj2qqkn6mku8s4k44ujs0m53h9epqqcarulnqwva8nt",
      "vault_code_id": "1453",
      "lp_code_id": "726"
    }
  ],
  "chain_id": "phoenix-1",
  "vault_factory_addr": "terra1vcn8h6fc26nv4f20p6g870a00nqzdpjwvshud9ku3qfaqhv7l69s9l29y2"
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