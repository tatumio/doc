# getcanwithdrawunfreezeamount

### How to use it

{% code overflow="wrap" lineNumbers="true" %}
```typescript
import { TatumSDK, Tron, Network } from '@tatumcom/js';

const tatum = await TatumSDK.init<Tron>({ network: Network.TRON });

const res = await tatum.rpc.getCanWithdrawUnfreezeAmount('TZ4UXDV5ZhNW7fb2AMSbgfAEZ7hWsnYS2g', {
  timestamp: 1667977444000,
  visible: true,
});

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}

### Overview

The `getCanWithdrawUnfreezeAmount` method allows you to retrieve the withdrawable balance for a specified owner address at a specific timestamp. This method is primarily used in the Stake 2.0 protocol on the TRON blockchain.

{% embed url="https://codepen.io/tatum-devrel/pen/BaGEMON" %}

Use Cases:

* Calculating the available balance that can be withdrawn by an owner address in the Stake 2.0 protocol.
* Providing real-time balance information to users or applications.

### Parameters

* `ownerAddress` (string): The owner address for which the withdrawable balance needs to be retrieved. (Default: hexString)
* `options` (object, optional): This optional parameter contains the following properties:
  * `timestamp` (integer, optional): The query cutoff timestamp in milliseconds.
  * `visible` (boolean, optional):  parameter to indicate whether the address is in base58 format.

### Return Object

The `getCanWithdrawUnfreezeAmount` method returns the following object:

* `amount`: The withdrawable balance in TRX, where the unit is sun.

### HTTP Request Example

```json
{
  "owner_address": "TZ4UXDV5ZhNW7fb2AMSbgfAEZ7hWsnYS2g",
  "timestamp": 1667977444000,
  "visible": true
}
```

### HTTP Response Example

```json
{
  "amount": 1000000
}
```

