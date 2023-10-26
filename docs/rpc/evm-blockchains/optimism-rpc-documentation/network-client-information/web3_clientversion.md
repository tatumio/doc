# web3\_clientVersion

### How to use it

{% tabs %}
{% tab title="TypeScript/JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Optimism, Network } from '@tatumio/tatum'
  
const tatum = await TatumSDK.init<Optimism>({network: Network.OPTIMISM})

const version = await tatum.rpc.clientVersion()

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Overview

`web3_clientVersion` is a method of the Optimism JSON-RPC API that allows the client to retrieve the current version of the Optimism client software being used by the node.

This method is read-only and does not require authentication. The `web3_clientVersion` method can be used by developers to confirm the version of the Optimism client software they are using and ensure that it is compatible with their application.

### Parameters

This method has no parameters. It only retrieves the current version of the Optimism client software.

### Return Object

The `web3_clientVersion` method returns a string representing the version of the Optimism client software being used. The string includes the client name, version number, and build information.

* `String` - Version string of the Optimism client software being used.

### Example Request

#### JSON Request

```json
{
  "jsonrpc": "2.0",
  "method": "web3_clientVersion",
  "params": [],
  "id": 1
}
```

### Example Response

#### JSON Response

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": "Geth/v1.10.3-stable-c2d2f1a3/linux-amd64/go1.16.4"
}
```
