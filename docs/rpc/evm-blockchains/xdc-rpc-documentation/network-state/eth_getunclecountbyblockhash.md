# eth\_getUncleCountByBlockHash

### How to use it

{% tabs %}
{% tab title="TypeScript/JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, XinFin, Network } from '@tatumio/tatum'
  
const tatum = await TatumSDK.init<XinFin>({ network: Network.XINFIN })

const result = await tatum.rpc.getUncleCountByBlockHash('0x0003bd8d00000625538ae9cb302a2eea2f17e5b751b447257b94617d90f1e01c')

await tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Overview

The `eth_getUncleCountByBlockHash` method is an JSON-RPC method that returns the number of uncles in a specified block by its hash. This method can be useful for gathering information about the performance of the network and to analyze the security of the blockchain.

Uncles are blocks that are not included in the main blockchain but are still valid, and they contribute to the overall security and decentralization of the network. The inclusion of uncles helps prevent centralization and ensures the mining process remains competitive.

### Parameters

The `eth_getUncleCountByBlockHash` method takes one parameter:

* `blockHash`: The hash of the block for which you want to get the uncle count.
  * Example value: `"0x0003bd8d00000625538ae9cb302a2eea2f17e5b751b447257b94617d90f1e01c"`

### Return Object

The return object for this method is a hex-encoded integer representing the number of uncles in the specified block.

* Example value: `"0x1"` (1 uncle)

### JSON-RPC Request and Response Examples

Here is an example JSON-RPC request and response for the `eth_getUncleCountByBlockHash` method:

**Request:**

```json
{
  "id": 1,
  "jsonrpc": "2.0",
  "method": "eth_getUncleCountByBlockHash",
  "params": [
    "0x0003bd8d00000625538ae9cb302a2eea2f17e5b751b447257b94617d90f1e01c"
  ]
}
```

**Response:**

```json
{
  "id": 1,
  "jsonrpc": "2.0",
  "result": "0x1"
}
```

In this example, the JSON-RPC request asks for the number of uncles in the block with the specified hash. The response indicates that there is one uncle in the block.

