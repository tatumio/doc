# getMaxRetransmitSlot

### How to Use It

{% code overflow="wrap" lineNumbers="true" %}
```javascript
// yarn add @tatumio/tatum

import { TatumSDK, Solana, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Solana>({ network: Network.SOLANA })

const res = await tatum.rpc.getMaxRetransmitSlot()

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}

### Overview

The `getMaxRetransmitSlot` method returns the highest slot number seen from the retransmit stage. This can be useful for monitoring the progress of the network or for determining the highest slot number that has been processed by a specific node.

{% embed url="https://codepen.io/Night-Shift-Dev/pen/abQZJGR" %}

### Parameters

None

### Return Object

The method returns a value representing the highest slot number observed in the retransmit stage.

### JSON-RPC Request Example

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "getMaxRetransmitSlot"
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
