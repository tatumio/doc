# getHighestSnapshotSlot

### How to Use It

{% code overflow="wrap" lineNumbers="true" %}
```javascript
// yarn add @tatumio/tatum

import { TatumSDK, Solana, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Solana>({ network: Network.SOLANA })

const res = await tatum.rpc.getHighestSnapshotSlot()

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}

### Overview

The `getHighestSnapshotSlot` method provides the highest slot information for which the node has snapshots. It determines the highest full snapshot slot and, if available, the highest incremental snapshot slot based on the full snapshot slot.

This method can be used in a variety of scenarios, including managing data storage and synchronisation of blockchain data. By knowing the highest snapshot slot, developers can estimate the amount of data that needs to be downloaded to sync a new node, or to ensure the node is up to date with the current state of the blockchain.

{% embed url="https://codepen.io/tatum-devrel/pen/MWzxjEK" %}

### Parameters

None

### Return Object

When the node has a snapshot, this method returns a JSON object with the following fields:

* `full`: The highest full snapshot slot.
* `incremental`: The highest incremental snapshot slot based on the full snapshot slot, if available.

### JSON-RPC Request Example

```json
{
  "jsonrpc":"2.0",
  "id":1,
  "method":"getHighestSnapshotSlot"
}
```

### JSON-RPC Response Example

Here is an example response when the node has a snapshot:

```json
{
  "jsonrpc": "2.0",
  "result": {
    "full": 100,
    "incremental": 110
  },
  "id": 1
}
```

In case the node does not have a snapshot, the response would be:

```json
{
  "jsonrpc": "2.0",
  "error": { "code": -32008, "message": "No snapshot" },
  "id": 1
}
```
