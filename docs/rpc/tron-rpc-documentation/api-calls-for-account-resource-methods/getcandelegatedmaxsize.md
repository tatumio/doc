# getcandelegatedmaxsize

### How to use it

{% code overflow="wrap" lineNumbers="true" %}
```typescript
import { TatumSDK, Tron, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Tron>({ network: Network.TRON })

const res = await tatum.rpc.getCanDelegatedMaxSize('TZ4UXDV5ZhNW7fb2AMSbgfAEZ7hWsnYS2g', 0, {
  visible: true
})

await tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}

### Overview

The `getCanDelegatedMaxSize` method is used to query the amount of delegatable resources share of the specified resource type for a given address on the TRON blockchain. The unit of measurement for the amount is sun. This method is part of the Stake2.0 functionality.

Use cases for this method include:

* Determining the amount of delegatable bandwidth or energy resources for an address.
* Calculating the available resources for delegation before initiating a delegation transaction.

{% embed url="https://codepen.io/tatum-devrel/pen/zYMXeJR" %}

### Parameters

1. `ownerAddress` (string): The owner address for which the delegatable resource share needs to be queried. It should be provided as a hexadecimal string.
2. `type` (integer): The resource type to query. Use `0` for bandwidth and `1` for energy.
3. `options` (object, optional): Additional options for the method.
   * `visible` (boolean, optional): Whether the address is in base58 format. Defaults to `true`.

### Return Object

The `getCanDelegatedMaxSize` method returns the following object:

* `max_size`: The amount of delegatable resource share in sun.

Note: If the delegating transaction has a memo, it would consume more bandwidth. Therefore, the actual delegatable share might be less than the value returned by this API.

### HTTP Request Example

```json
{
    "owner_address": "TZ4UXDV5ZhNW7fb2AMSbgfAEZ7hWsnYS2g",
    "type": 0,
    "visible": true
}
```

### HTTP Response Example

```json
{
    "max_size": 12311
}
```
