# Epoch Manager

## Instantiate

Instantiates an instance of the epoch manager contract

```json
{
  "start_epoch": {
    "id": 0,
    "start_time": "1571797419879305533"
  },
  "epoch_config": {
    "duration": "86400000000000",
    "genesis_epoch": "1571797419879305533"
  }
}
```

| Key            | Type        | Description                                  |
|----------------|-------------|----------------------------------------------|
| `start_epoch`  | Epoch       | The initial epoch to start the contract with |
| `epoch_config` | EpochConfig | The configuration for the epochs             |

## ExecuteMsg

### CreateEpoch

Creates a new epoch. It's permissionless. A new epoch can only be created after the current one has ended.

```json
{
  "create_epoch": {}
}
```

### AddHook

Adds a new hook to the hook registry, i.e. adds a contract to be notified when a new epoch is created.

```json
{
  "add_hook": {
    "contract_addr": "migaloo1..."
  }
}
```

| Key             | Type   | Description                                                  |
|-----------------|--------|--------------------------------------------------------------|
| `contract_addr` | String | The address of the contract to be added to the hook registry |

### RemoveHook

Removes a hook from the hook registry.

```json
{
  "remove_hook": {
    "contract_addr": "migaloo1..."
  }
}
```

| Key             | Type   | Description                                                  |
|-----------------|--------|--------------------------------------------------------------|
| `contract_addr` | String | The address of the contract to be added to the hook registry |

### UpdateConfig

Updates the contract configuration.

```json
{
  "update_config": {
    "owner": "migaloo1...",
    "epoch_config": {
      "duration": "86400000000000",
      "genesis_epoch": "1571797419879305533"
    }
  }
}
```

| Key            | Type                 | Description                   |
|----------------|----------------------|-------------------------------|
| `owner`        | Option\<String>      | The new owner of the contract |
| `epoch_config` | Option\<EpochConfig> | The new epoch configuration   |

## QueryMsg

### Config

Returns the configuration of the contract.

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
  "epoch_config": {
    "duration": "86400000000000",
    "genesis_epoch": "1571797419879305533"
  }
}
```

| Key            | Type        | Description               |
|----------------|-------------|---------------------------|
| `owner`        | Addr        | The owner of the contract |
| `epoch_config` | EpochConfig | The epoch configuration   |

{% endtab %}
{% endtabs %}

### CurrentEpoch

Returns the current epoch, which is the last on the EPOCHS map

{% tabs %}
{% tab title="Query" %}

```json
{
  "current_epoch": {}
}
```

{% endtab %}

{% tab title="Response (EpochResponse)" %}

```json
{
  "epoch": {
    "id": 0,
    "start_time": "1571797419879305533"
  }
}
```

| Key     | Type  | Description       |
|---------|-------|-------------------|
| `epoch` | Epoch | The current epoch |

{% endtab %}
{% endtabs %}

### Epoch

Returns the epoch with the given ID.

{% tabs %}
{% tab title="Query" %}

```json
{
  "epoch": {
    "id": 100
  }
}
```

{% endtab %}

{% tab title="Response (EpochResponse)" %}

```json
{
  "epoch": {
    "id": 100,
    "start_time": "1571797419879305533"
  }
}
```

| Key     | Type  | Description                         |
|---------|-------|-------------------------------------|
| `epoch` | Epoch | The queried epoch with the given id |

{% endtab %}
{% endtabs %}

### Hooks

Returns the hooks in the registry.

{% tabs %}
{% tab title="Query" %}

```json
{
  "hooks": {}
}
```

{% endtab %}

{% tab title="Response (HooksResponse)" %}

```json
{
  "hooks": [
    "migaloo1...",
    "migaloo2..."
  ]
}
```

| Key     | Type         | Description                        |
|---------|--------------|------------------------------------|
| `hooks` | Vec\<String> | The contracts registered for hooks |

{% endtab %}
{% endtabs %}

### Hook

Returns whether a hook has been registered.

{% tabs %}
{% tab title="Query" %}

```json
{
  "hook": {
    "hook": "migaloo1..."
  }
}
```

{% endtab %}

{% tab title="Response (bool)" %}

```json
{
  "data": true
}
```

| Key    | Type | Description                                              |
|--------|------|----------------------------------------------------------|
| `data` | bool | True if the hook exists in the registry, false otherwise |

{% endtab %}
{% endtabs %}
