# getIdentity

### How to Use It

{% code overflow="wrap" lineNumbers="true" %}
```javascript
// yarn add @tatumio/tatum

import { TatumSDK, Solana, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Solana>({ network: Network.SOLANA })

const res = await tatum.rpc.getIdentity()

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}

### Overview

The `getIdentity` method is used to retrieve the identity pubkey for the current node. This pubkey represents a unique identifier for the node in the Solana network.

Use cases for this method might include retrieving the identity of a node for tracking or monitoring purposes, or validating the identity of a node in scenarios where only certain nodes are trusted for certain operations.

{% embed url="https://codepen.io/tatum-devrel/pen/PoxLGdg" %}

### Parameters

This method does not require any parameters.

### Return Object

The result field will be a JSON object with the following fields:

* `identity`: The identity pubkey of the current node as a base-58 encoded string.

### JSON-RPC Request Example

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "getIdentity"
}
```

### JSON-RPC Response Example

```json
{
  "jsonrpc": "2.0",
  "result": {
    "identity": "2r1F4iWqVcb8M1DbAjQuFpebkQHY9hcVU4WuW2DJBppN"
  },
  "id": 1
}
```
