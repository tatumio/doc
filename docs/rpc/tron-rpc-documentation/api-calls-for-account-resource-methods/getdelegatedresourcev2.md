# getdelegatedresourcev2

### How to use it

{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Tron, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Tron>({network: Network.TRON})

const result = await tatum.rpc.getDelegatedResourceV2('fromAddress', 'toAddress', {
visible: true,
})

await tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}

### Overview

`getDelegatedResourceV2` is an RPC method provided by TRON's API. In the context of TRON's Stake2.0 system, it is used to query detailed information about the resource share delegated from one address to another.

Some potential use cases might include:

1. Checking the status of resource sharing between addresses.
2. Assessing the delegation history between two addresses.

{% embed url="https://codepen.io/tatum-devrel/pen/vYQMbzM" %}

### Parameters

* `fromAddress` (string): - The address from which resources are delegated. By default, it is in hexString format.
* `toAddress` (string): - The address to which resources are delegated.
* `options` (object, optional): This optional parameter contains the following properties:
  * `visible` (boolean, optional): Optional parameter to specify whether the address is in base58 format.

### Return Object

The returned object includes a `delegatedResource` list. Each item in the list includes the following fields:

* `from` (string): The owner's address.
* `to` (string): The recipient's address.
* `frozen_balance_for_bandwidth` (integer): The amount of TRX staked for bandwidth delegated from the `from` address to the `to` address.
* `frozen_balance_for_energy` (integer): The amount of TRX staked for energy delegated from the `from` address to the `to` address.
* `expire_time_for_bandwidth` (integer):  The lock-up period deadline for bandwidth delegation. If no lock is specified when delegating resources, this field will not be displayed in the returned result and the value will be 0.
* `expire_time_for_energy` (integer): The lock-up period deadline for energy delegation. If no lock is specified when delegating resources, this field will not be displayed in the returned result and the value will be 0.

### HTTP Request Example

<pre class="language-json"><code class="lang-json"><strong>{
</strong><strong>  "fromAddress": "TZ4UXDV5ZhNW7fb2AMSbgfAEZ7hWsnYS2g",
</strong>  "toAddress": "TPswDDCAWhJAZGdHPidFg5nEf8TkNToDX1",
  "visible": true
}
</code></pre>

### HTTP Response Example

```json
[
  {
    "from": "TZ4UXDV5ZhNW7fb2AMSbgfAEZ7hWsnYS2g",
    "to": "TPswDDCAWhJAZGdHPidFg5nEf8TkNToDX1",
    "frozen_balance_for_bandwidth": 1000,
    "frozen_balance_for_energy": 1000,
    "expire_time_for_bandwidth": 1597463006000,
    "expire_time_for_energy": 1597463006000
  }
]
```
