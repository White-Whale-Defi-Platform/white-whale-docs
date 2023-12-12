# 👷 Frontend Helper

The frontend helper contract is used to make it easy for frontends or other contracts to provide liquidity and lock the
LP for incentives with a single message.

Once users have provided liquidity on WW pools via the [pair contract](terraswap-pair.md#provide-liquidity), there is an
additional step to lock the LP tokens for incentives in the [incentive contract](incentive.md#openposition) of the pool
they provided liquidity to. These two actions are separate, so in a normal scenario, the user would need to first
provide liquidity and then lock it, effectively signing two separate transactions.

The frontend helper allows users to do this in a single transaction, by providing liquidity and locking it for
incentives via the [deposit](#deposit) message.

***

The following are the messages that can be executed on the frontend helper contract:

## Instantiate

Instantiates the frontend helper.

```json
{
  "incentive_factory": "migaloo1..."
}
```

| Key                 | Type   | Description                      |
|---------------------|--------|----------------------------------|
| `incentive_factory` | String | Address of the incentive factory |

## Migrate

Migrates the frontend helper. This is to be triggered by the owner.

```json
{}
```

## ExecuteMsg

### Deposit

Deposits assets into a pair pool and opens or expands a position on the respective incentive contract with the received
LP tokens.

```json
{
  "deposit": {
    "pair_address": "migaloo1...",
    "assets": [
      {
        "info": {
          "native_token": {
            "denom": "uusdc"
          }
        },
        "amount": "1000"
      },
      {
        "info": {
          "native_token": {
            "denom": "ibc/B3504E092456BA618CC28AC671A71FB08C6CA0FD0BE7C8A5B5A3E2DD933CC9E4"
          }
        },
        "amount": "1000"
      }
    ],
    "slippage_tolerance": "0.01",
    "unbonding_duration": 86400
  }
}
```

| Key                  | Type             | Description                                                                                                |
|----------------------|------------------|------------------------------------------------------------------------------------------------------------|
| `pair_address`       | String           | Address of the pair to provide liquidity to                                                                |
| `assets`             | \[Asset; 2]      | Assets to provide liquidity with                                                                           |
| `slippage_tolerance` | Option\<Decimal> | If set, the transaction will succeed if the price in the pool moves less than the given slippage tolerance |
| `unbonding_duration` | u64              | The amount of time in seconds to unbond tokens for when incentivizing                                      |

### Update config

Updates the configuration of the frontend helper.

```json
{
  "update_config": {
    "owner": "migaloo1...",
    "incentive_factory_addr": "migaloo1..."
  }
}
```

| Key                      | Type            | Description                   |
|--------------------------|-----------------|-------------------------------|
| `owner`                  | Option\<String> | New owner of the contract     |
| `incentive_factory_addr` | Option\<String> | New incentive factory address |

## Queries

### Config

Retrieves the configuration of the frontend helper.

{% tabs %}
{% tab title="Query" %}

```json
{
  "config": {}
}
```

{% endtab %}    

{% tab title="Response (ConfigResponse)" %}

```json
{
  "owner": "migaloo1...",
  "incentive_factory_addr": "migaloo1..."
}
```

| Key                      | Type | Description                            |
|--------------------------|------|----------------------------------------|
| `owner`                  | Addr | The contract's owner                   |
| `incentive_factory_addr` | Addr | The incentive factory contract address |

{% endtab %}
{% endtabs %}
