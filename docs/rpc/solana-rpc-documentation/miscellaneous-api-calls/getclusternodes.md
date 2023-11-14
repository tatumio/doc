# getClusterNodes

### How to Use It

{% code overflow="wrap" lineNumbers="true" %}
```javascript
// yarn add @tatumio/tatum

import { TatumSDK, Solana, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Solana>({ network: Network.SOLANA })

const res = await tatum.rpc.getClusterNodes()

await tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}

### Overview

The `getClusterNodes` method returns information about all the nodes participating in the cluster. This method can be used for network analysis, monitoring, and audit purposes. For example, you can use it to track the versions of software running on various nodes, identify the public keys of nodes, or determine the network addresses for various services.

{% embed url="https://codepen.io/tatum-devrel/pen/YzRgGjO" %}

### Parameters

This method does not require any parameters.

### Return Object

The method returns an array of JSON objects, each containing the following fields:

* `pubkey`: Node's public key, as base-58 encoded string.
* `gossip`: Gossip network address for the node.
* `tpu`: TPU network address for the node.
* `rpc`: JSON RPC network address for the node, or `null` if the JSON RPC service is not enabled.
* `version`: The software version of the node, or `null` if the version information is not available.
* `featureSet`: The unique identifier of the node's feature set.
* `shredVersion`: The shred version the node has been configured to use.

### JSON-RPC Request Example

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "getClusterNodes"
}
```

### JSON-RPC Response Example

```json
{
  "jsonrpc": "2.0",
  "result": [
    {
      "gossip": "10.239.6.48:8001",
      "pubkey": "9QzsJf7LPLj8GkXbYT3LFDKqsj2hHG7TA3xinJHu8epQ",
      "rpc": "10.239.6.48:8899",
      "tpu": "10.239.6.48:8856",
      "version": "1.0.0 c375ce1f"
    }
  ],
  "id": 1
}
```
