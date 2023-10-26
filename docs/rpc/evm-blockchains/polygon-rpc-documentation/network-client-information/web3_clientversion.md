# web3\_clientVersion

### How to use it

{% tabs %}
{% tab title="TypeScript/JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Polygon, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Polygon>({network: Network.POLYGON})

const version = await tatum.rpc.clientVersion()

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Overview

`web3_clientVersion` is a method of the Polygon JSON-RPC API that allows the client to retrieve the current version of the Polygon client software being used by the node.

This method is read-only and does not require authentication. The `web3_clientVersion` method can be used by developers to confirm the version of the Polygon client software they are using and ensure that it is compatible with their application.

{% embed url="https://codepen.io/tatum-devrel/pen/poQGqGN" %}

### Parameters

This method has no parameters. It only retrieves the current version of the Polygon client software.

### Return Object

The `web3_clientVersion` method returns a string representing the version of the Polygon client software being used. The string includes the client name, version number, and build information.

* `String` - Version string of the Polygon client software being used.

### Example Request

#### JSON Request

```json
{
  "jsonrpc": "2.0",
  "method": "web3_clientVersion",
  "params": [],
  "id": 67
}
```

### Example Response

#### JSON Response

```json
{
  "jsonrpc": "2.0",
  "id": 67,
  "result": "Geth/v1.10.3-stable-c2d2f1a3/linux-amd64/go1.16.4"
}
```

In the above example, the Polygon client software being used is Geth, version 1.10.3, with build information `stable-c2d2f1a3/linux-amd64/go1.16.4`. The `result` field contains the version string.
