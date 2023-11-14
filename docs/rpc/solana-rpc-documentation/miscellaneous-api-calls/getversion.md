# getVersion

### How to Use It

{% code overflow="wrap" lineNumbers="true" %}
```javascript
// yarn add @tatumio/tatum

import { TatumSDK, Solana, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Solana>({ network: Network.SOLANA })

const res = await tatum.rpc.getVersion()

await tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}

### Overview

The `getVersion` method is used to retrieve the current Solana version running on the node. This information can be useful for troubleshooting, compatibility checks, or for understanding the node's capabilities based on its version.

{% embed url="https://codepen.io/tatum-devrel/pen/vYQPXVV" %}

### Parameters

This method does not require any parameters.

### Return Object

The result field will be a JSON object with the following fields:

* `solana-core`: The software version of `solana-core`.
* `feature-set`: The unique identifier of the current software's feature set.

### JSON-RPC Request Example

```json
jsonCopy code{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "getVersion"
}
```

### JSON-RPC Response Example

```json
jsonCopy code{
  "jsonrpc": "2.0",
  "result": {
    "solana-core": "1.15.0"
  },
  "id": 1
}
```
