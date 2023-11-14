# getaccount

### How to use it

{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumcom/js

import { TatumSDK, Tron, Network } from '@tatumcom/js'

const tatum = await TatumSDK.init<Tron>({network: Network.TRON})

const account = await tatum.rpc.getAccount('TZ4UXDV5ZhNW7fb2AMSbgfAEZ7hWsnYS2g', {
  visible: true,
})

await tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}

### Overview

The `getAccount` method is used to query information about an account on the TRON network. It provides details including TRX balance, TRC-10 balances, stake information, vote information, permissions, and more.

{% embed url="https://codepen.io/tatum-devrel/pen/oNQOmqa" %}

### Parameters

* `address` (string): The account address to be queried. It should be converted to a hex string.
* `options` (object, optional): This optional parameter contains the following properties:
  * `visible` (boolean, optional): Determines whether the address is in base58 format. Default is false.

### Return Object

* `account_name` (string): The name of the account. The account name can be modified once through the `wallet/updateaccount` interface.
* `address` (string): Account address.
* `create_time` (int64): Account creation time, i.e. account activation time on the TRON network.
* `balance` (int64): TRX balance of the account.
* `frozen` (object): Contains two properties - `frozen_balance` (int64) which is the total amount of TRX staked by the account to obtain bandwidth in Stake 1.0, and `expire_time` (int64) which is the expiration time of the stake operation performed by the account to obtain bandwidth. The account can perform the unstake operation after this time.
* `delegated_frozen_balance_for_bandwidth` (int64): Total amount of TRX staked by the account for others to get bandwidth in Stake 1.0.
* `acquired_delegated_frozen_balance_for_bandwidth` (int64): Total amount of TRX staked by other accounts for this account to get bandwidth in Stake 1.0.
* `account_resource` (object): Contains information about the account's resources, including `frozen_balance_for_energy` (object) with `frozen_balance` (int64) and `expire_time` (int64), `delegated_frozen_balance_for_energy` (int64), `acquired_delegated_frozen_balance_for_energy` (int64), `delegated_frozenV2_balance_for_energy` (int64), `acquired_delegated_frozenV2_balance_for_energy` (int64), `energy_window_size` (int64), `energy_usage` (int64), and `latest_consume_time_for_energy` (int64).
* `delegated_frozenV2_balance_for_bandwidth` (int64): Total amount of TRX staked by the account for others to get bandwidth in Stake 2.0.
* `acquired_delegated_frozenV2_balance_for_bandwidth` (int64): Total amount of TRX staked by other accounts for this account to get bandwidth in Stake 2.0.
* `frozenV2` (FreezeV2\[]): In Stake 2.0, the total amount of TRX staked to obtain various types of resources does not include the delegated TRX.
* `unfrozenV2` (UnFreezeV2\[]): In Stake 2.0, each unstaking information. One of the unstaking information contains three fields: `type` (resource type), `unfreeze_amount` (the amount of unstaked TRX), `unfreeze_expire_time` (the start timestamp when the unstaked TRX can be withdrawn, in ms).
* `net_usage` (int64): The amount of bandwidth used by the account.
* `free_net_usage` (int64): The amount of free bandwidth used by the account.
* `net_window_size` (int64): The number of block times required for bandwidth obtained by stake to fully recover.
* `free_asset_net_usageV2` (map\<string, int64>): The amount of trc10's free bandwidth used by this account.
* `votes` (Vote): The number of votes for each Super Representative.
* `latest_opration_time` (int64): The last operation time.
* `latest_consume_time` (int64): The last time the account consumed bandwidth.
* `latest_consume_free_time` (int64): The last time the account consumed free bandwidth.

### HTTP Request Example

The HTTP request body for invoking this method is:

```json
{
  "address": "TZ4UXDV5ZhNW7fb2AMSbgfAEZ7hWsnYS2g",
  "visible": true
}
```

### HTTP Response Example

A successful response might look like:

```json
{
  "address": "TZ4UXDV5ZhNW7fb2AMSbgfAEZ7hWsnYS2g",
  "balance": 2000000000,
  "create_time": 1637411046000,
  "net_window_size": 28800,
  "account_resource": {
    "energy_window_size": 28800
  },
  "owner_permission": {
    "permission_name": "owner",
    "threshold": 1,
    "keys": [
      {
        "address": "TZ4UXDV5ZhNW7fb2AMSbgfAEZ7hWsnYS2g",
        "weight": 1
      }
    ]
  },
  "active_permission": [
    {
      "type": "Active",
      "id": 2,
      "permission_name": "active",
      "threshold": 1,
      "operations": "7fff1fc0033e0300000000000000000000000000000000000000000000000000",
      "keys": [
        {
          "address": "TZ4UXDV5ZhNW7fb2AMSbgfAEZ7hWsnYS2g",
          "weight": 1
        }
      ]
    }
  ],
  "frozenV2": [
    {},
    {
      "type": "ENERGY"
    },
    {
      "type": "TRON_POWER"
    }
  ]
}
```
