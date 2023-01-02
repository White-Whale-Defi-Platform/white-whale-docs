# Comdex testnet (comdex-test2)

```json
{
  "contracts": [
    {
      "wasm": "fee_collector.wasm",
      "code_id": "5",
      "version": "1.0.5",
      "contract_address": "comdex1j08452mqwadp8xu25kn9rleyl2gufgfjnv0sn8dvynynakkjukcqp8p0w7"
    },
    {
      "wasm": "terraswap_factory.wasm",
      "code_id": "6",
      "version": "1.1.2",
      "contract_address": "comdex1fyr2mptjswz4w6xmgnpgm93x0q4s4wdl6srv3rtz3utc4f6fmxeqgytwdm"
    },
    {
      "wasm": "terraswap_pair.wasm",
      "code_id": "7",
      "version": "1.2.0"
    },
    {
      "wasm": "terraswap_router.wasm",
      "code_id": "8",
      "version": "1.0.7",
      "contract_address": "comdex1vguuxez2h5ekltfj9gjd62fs5k4rl2zy5hfrncasykzw08rezpfscw6nu6"
    },
    {
      "wasm": "terraswap_token.wasm",
      "code_id": "12",
      "version": "1.0.2"
    },
    {
      "wasm": "vault_factory.wasm",
      "code_id": "9",
      "version": "1.0.9",
      "contract_address": "comdex1vhndln95yd7rngslzvf6sax6axcshkxqpmpr886ntelh28p9ghuqp7z24e"
    },
    {
      "wasm": "vault.wasm",
      "code_id": "11",
      "version": "1.2.0"
    },
    {
      "wasm": "vault_router.wasm",
      "code_id": "10",
      "version": "1.1.3",
      "contract_address": "comdex13we0myxwzlpx8l5ark8elw5gj5d59dl6cjkzmt80c5q5cv5rt54qex0gde"
    }
  ],
  "date": "2022-12-20T11:02:43+0000",
  "initial_block_height": "null",
  "final_block_height": "291346",
  "chain_id": "comdex-test2",
  "deployer_address": "comdex1ut7pkdz4hgy689v98vf3dj650frynyajqul6yq"
}
```

```json
{
  "pools": [
    {
      "pair": "ucmdx-uharbor",
      "assets": [
        "{\"native_token\":{\"denom\":\"ucmdx\"}}",
        "{\"native_token\":{\"denom\":\"uharbor\"}}"
      ],
      "pool_address": "comdex1gg6f95cymcfrfzhpek7cf5wl53t5kng52cd2m0krgdlu8k58vd8qmal0am",
      "lp_address": "comdex16yzagwlqrzjkjlnaecam5fwvtzgae5zujtcch7y2uf6q9fyksncqm4rrk6",
      "pool_code_id": "7",
      "lp_code_id": "12"
    },
    {
      "pair": "ucmdx-uharbor",
      "assets": [
        "{\"native_token\":{\"denom\":\"ucmdx\"}}",
        "{\"native_token\":{\"denom\":\"uharbor\"}}"
      ],
      "pool_address": "comdex19hlynxzedrlqv99v6qscww7d3crhl86qtd0vprpltg5g9xx6jk9qcmxed5",
      "lp_address": "comdex1guczj53xxl4347adagh23eelyhnxvugw2nqq0q0dr6kws7q35jyqzf9hkm",
      "pool_code_id": "7",
      "lp_code_id": "12"
    }
  ],
  "date": "2022-12-20T11:23:56+0000",
  "chain_id": "comdex-test2",
  "pool_factory_addr": "comdex1fyr2mptjswz4w6xmgnpgm93x0q4s4wdl6srv3rtz3utc4f6fmxeqgytwdm"
}
```

```json
{
  "vaults": [
    {
      "asset": "ucmdx",
      "vault_address": "comdex1x8gwn06l85q0lyncy7zsde8zzdn588k2dck00a8j6lkprydcutwqdsg6t3",
      "lp_address": "comdex1657pee2jhf4jk8pq6yq64e758ngvum45gl866knmjkd83w6jgn3s4ljy9s",
      "vault_code_id": "11",
      "lp_code_id": "12"
    }
  ],
  "date": "2022-12-20T11:04:35+0000",
  "chain_id": "comdex-test2",
  "vault_factory_addr": "comdex1vhndln95yd7rngslzvf6sax6axcshkxqpmpr886ntelh28p9ghuqp7z24e"
}
```