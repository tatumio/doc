# getTransactionCount

### How to Use It

{% code overflow="wrap" lineNumbers="true" %}
```javascript
// yarn add @tatumio/tatum

import { TatumSDK, Solana, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Solana>({ network: Network.SOLANA })

const res = await tatum.rpc.getTransactionCount()

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}

### Overview

The `getTransactionCount` method retrieves the current transaction count from the ledger. This can be used to track the number of transactions processed by the network.

{% embed url="https://codepen.io/tatum-devrel/pen/jOQJroJ?editors=1111" %}

### Parameters

* `options` (object, optional): Configuration object containing the following fields:
  * `commitment` (string, optional): Specifies the confirmation level of data to be fetched.
    * Values: `finalized` `confirmed` `processed`
  * `minContextSlot`: (number, optional) The minimum slot that the request can be evaluated at.
    * Example: `5`

### Return Object

The method returns a number indicating the current transaction count from the ledger.

### JSON-RPC Request Example

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "getTransactionCount",
}
```

### JSON-RPC Response Example

```json
{
  "jsonrpc": "2.0",
  "result": 268,
  "id": 1
}
```
