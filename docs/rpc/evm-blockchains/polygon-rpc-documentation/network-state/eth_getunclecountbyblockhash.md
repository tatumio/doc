# eth\_getUncleCountByBlockHash

### How to use it

{% tabs %}
{% tab title="TypeScript/JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Polygon, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Polygon>({network: Network.POLYGON})

const result = await tatum.rpc.getUncleCountByBlockHash('0x3a3e528dcd6e05a614c9241b0a9296db961fa6a92e05af9f6c0d7d2f6bc92f7a', 'pending')

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Overview

The `eth_getUncleCountByBlockHash` method is a Polygon JSON-RPC method that returns the number of uncles in a specified block by its hash. This method can be useful for gathering information about the performance of the Polygon network and analyzing the security of the blockchain.

Uncles are blocks that are not included in the main blockchain but are still valid, and they contribute to the overall security and decentralisation of the Polygon network. The inclusion of uncles helps prevent centralisation and ensures the mining process remains competitive.

{% embed url="https://codepen.io/tatum-devrel/pen/jOQdXQq" %}

### Parameters

The `eth_getUncleCountByBlockHash` method takes one parameter:

* `blockHash`: The hash of the block for which you want to get the uncle count.
  * Example value: `"0x3a3e528dcd6e05a614c9241b0a9296db961fa6a92e05af9f6c0d7d2f6bc92f7a"`

### Return Object

The returned object for this method is a hex-encoded integer representing the number of uncles in the specified block.

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
    "0x3a3e528dcd6e05a614c9241b0a9296db961fa6a92e05af9f6c0d7d2f6bc92f7a"
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

