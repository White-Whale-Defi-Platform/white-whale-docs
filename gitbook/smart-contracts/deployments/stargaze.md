# Stargaze testnet (elgafar-1)

```json
{
  "contracts": [
    {
      "wasm": "fee_collector.wasm",
      "code_id": "719",
      "version": "1.0.5",
      "contract_address": "stars1umwpa8kas45qcusjkcgjd6l2e49lwnws6kq9ka7t75wwgf47fn3sf4j4vl"
    },
    {
      "wasm": "terraswap_factory.wasm",
      "code_id": "720",
      "version": "1.1.2",
      "contract_address": "stars13av7gw2mwejlkhsst8luva2q24kqql04afzpxmrrceuafehsg84q7pgtgu"
    },
    {
      "wasm": "terraswap_pair.wasm",
      "code_id": "721",
      "version": "1.2.0"
    },
    {
      "wasm": "terraswap_router.wasm",
      "code_id": "722",
      "version": "1.0.7",
      "contract_address": "stars1vndklq26ykcajzs4nq2kmgqj0zh2qxv6ntgvp4tyr6e4kev7rxsq9v2qcj"
    },
    {
      "wasm": "terraswap_token.wasm",
      "code_id": "723",
      "version": "1.0.2"
    },
    {
      "wasm": "vault_factory.wasm",
      "code_id": "724",
      "version": "1.0.9",
      "contract_address": "stars1hskve2k97qpmz9cfetum9x5t5fywvwkxn3arehgpu5zpld0k9udshfqs7q"
    },
    {
      "wasm": "vault_router.wasm",
      "code_id": "725",
      "version": "1.1.3",
      "contract_address": "stars1zdeflv48zk06cqa5zfav7qt27z8uelvd2h3q9ljlq6p2pkx73kns8v073f"
    },
    {
      "wasm": "vault.wasm",
      "code_id": "726",
      "version": "1.2.0"
    }
  ],
  "date": "2022-12-21T15:03:06+0000",
  "initial_block_height": "null",
  "final_block_height": "2574466",
  "chain_id": "elgafar-1",
  "deployer_address": "stars1ut7pkdz4hgy689v98vf3dj650frynyajn029kx"
}
```

```json
{
  "pools": [
    {
      "pair": "ustars-MOONS",
      "assets": [
        "{\"native_token\":{\"denom\":\"ustars\"}}",
        "{\"token\":{\"contract_addr\":\"stars1rezgwyptacfpvczgtpmr44dzv7kfnk7yuyyjnfkvdzg4gplsgz8qmsdnep\"}}"
      ],
      "pool_address": "stars1q75mppps4aram5ez9mn3e432p8klmy7ettp7yggrrl4aqtjx3ayqsy4h8x",
      "lp_address": "stars1eql9u0h7l8tlwc0ema3qp05f7zrzp8fppl05q0agnsw4nr9yvrfqq2sr4d",
      "pool_code_id": "721",
      "lp_code_id": "723"
    }
  ],
  "date": "2022-12-21T15:14:07+0000",
  "chain_id": "elgafar-1",
  "pool_factory_addr": "stars13av7gw2mwejlkhsst8luva2q24kqql04afzpxmrrceuafehsg84q7pgtgu"
}
```

```json
{
  "vaults": [
    {
      "asset": "ustars",
      "vault_address": "stars16454nykz652pxzlwujfh8qnqcq3w8vuutq8ned2g8rr52eyz3yqsyurq0v",
      "lp_address": "stars1a8ndcehx37guv447vyn4ucxwnu34xxv8gcxf8s0hrep69kusqg5sgzudk6",
      "vault_code_id": "726",
      "lp_code_id": "723"
    }
  ],
  "date": "2022-12-21T15:14:35+0000",
  "chain_id": "elgafar-1",
  "vault_factory_addr": "stars1hskve2k97qpmz9cfetum9x5t5fywvwkxn3arehgpu5zpld0k9udshfqs7q"
}
```