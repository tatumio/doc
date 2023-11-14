# getMaxShredInsertSlot

### How to Use It

{% code overflow="wrap" lineNumbers="true" %}
```javascript
// yarn add @tatumio/tatum

import { TatumSDK, Solana, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Solana>({ network: Network.SOLANA })

const res = await tatum.rpc.getMaxShredInsertSlot()

await tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}

### Overview

The `getMaxShredInsertSlot` method returns the highest slot number observed after a shred insert. This can be useful for monitoring the highest slot number that a specific node has processed after the shred insert stage, providing insights into the node's synchronisation status.

{% embed url="https://codepen.io/tatum-devrel/pen/gOQEwQy" %}

### Parameters

None

### Return Object

The method returns a value representing the highest slot number observed after a shred insert.

### JSON-RPC Request Example

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "getMaxShredInsertSlot"
}
```

### JSON-RPC Response Example

```json
{
  "jsonrpc": "2.0",
  "result": 1234,
  "id": 1
}
```
