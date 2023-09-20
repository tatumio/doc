# getdelegatedresource

### How to use it

{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Tron, Network, VisibleOption } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Tron>({network: Network.TRON})

const res = await tatum.rpc.getDelegatedResource('TZ4UXDV5ZhNW7fb2AMSbgfAEZ7hWsnYS2g', 'TPswDDCAWhJAZGdHPidFg5nEf8TkNToDX1', {
  visible: true,
})

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}

### Overview

The `getDelegatedResource` method retrieves all resources delegations during the stake1.0 phase from one account to another. It is useful when you need to assess the resources that an address delegates to a target address. The `fromAddress` parameter can be retrieved from the GetDelegatedResourceAccountIndex API.

{% embed url="https://codepen.io/tatum-devrel/pen/ZEmZwRJ" %}

### Parameters

* `fromAddress` (string, required): The energy from address. Default is hexString.
* `toAddress` (string, required): The target address for the energy delegation information.
* `options` (object, optional): This optional parameter contains the following properties:
  * `visible` (boolean, optional): Defaults to false. Whether addresses are in base58 format.

### Return Object

The return object is a list of `DelegatedResource` objects. Each `DelegatedResource` object contains:

* `from` (string): Delegate account
* `to` (string): Resource receiving account
* `frozen_balance_for_bandwidth` (integer): Bandwidth delegate share
* `frozen_balance_for_energy` (integer): Energy delegate share
* `expire_time_for_bandwidth` (integer): Deadline of this delegate bandwidth's lock period
* `expire_time_for_energy` (integer): Deadline of this delegate energy's lock period

### HTTP Request Example

```json
{
  "fromAddress": "TZ4UXDV5ZhNW7fb2AMSbgfAEZ7hWsnYS2g",
  "toAddress": "TPswDDCAWhJAZGdHPidFg5nEf8TkNToDX1",
  "visible": true
}
```

### HTTP Response Example

```json
[
    {
      "from": "TZ4UXDV5ZhNW7fb2AMSbgfAEZ7hWsnYS2g",
      "to": "TPswDDCAWhJAZGdHPidFg5nEf8TkNToDX1",
      "frozen_balance_for_bandwidth": 2000,
      "frozen_balance_for_energy": 3000,
      "expire_time_for_bandwidth": 1672448400000,
      "expire_time_for_energy": 1675040400000
    }
]
```
