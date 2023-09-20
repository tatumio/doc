# getFirstAvailableBlock

### How to Use It

{% code overflow="wrap" lineNumbers="true" %}
```javascript
// yarn add @tatumio/tatum

import { TatumSDK, Solana, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Solana>({ network: Network.SOLANA })

const res = await tatum.rpc.getFirstAvailableBlock()

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}

### Overview

The `getFirstAvailableBlock` method returns the slot of the lowest confirmed block that has not been purged from the ledger. This method is useful when you want to start parsing the ledger from the oldest available data, or when you want to check how far back the data in your node goes. This can be critical in scenarios where historical block data is required for backtracking transactions or auditing purposes.

{% embed url="https://codepen.io/tatum-devrel/pen/MWzxjvK" %}

### Parameters

This method does not require any parameters.

### Return Object

The method returns an integer representing the slot of the oldest confirmed block that has not been purged from the ledger.

### JSON-RPC Request Example

```json
{
  "jsonrpc":"2.0",
  "id":1,
  "method":"getFirstAvailableBlock"
}
```

### JSON-RPC Response Example

```json
{
  "jsonrpc": "2.0",
  "result": 250000,
  "id": 1
}
```
