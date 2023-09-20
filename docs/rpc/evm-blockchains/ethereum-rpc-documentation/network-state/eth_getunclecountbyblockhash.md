# eth\_getUncleCountByBlockHash

### How to use it

{% tabs %}
{% tab title="TypeScript/JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Ethereum, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Ethereum>({network: Network.ETHEREUM})

const result = await tatum.rpc.getUncleCountByBlockHash('0x827d30e914a3adeefabb9d53f70da87e6e0ed3d02a72e7d9ae9bfd1bf123c7a3')

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Overview

The `eth_getUncleCountByBlockHash` method is an Ethereum JSON-RPC method that returns the number of uncles in a specified block by its hash. This method can be useful for gathering information about the performance of the Ethereum network and to analyse the security of the blockchain.

Uncles are blocks that are not included in the main blockchain but are still valid, and they contribute to the overall security and decentralisation of the Ethereum network. The inclusion of uncles helps prevent centralisation and ensures the mining process remains competitive.



{% embed url="https://codepen.io/Jan-Musil-the-lessful/pen/NWEJRvZ" %}

### Parameters

The `eth_getUncleCountByBlockHash` method takes one parameter:

* `blockHash`: The hash of the block for which you want to get the uncle count.
  * Example value: `"0x827d30e914a3adeefabb9d53f70da87e6e0ed3d02a72e7d9ae9bfd1bf123c7a3"`

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
    "0x827d30e914a3adeefabb9d53f70da87e6e0ed3d02a72e7d9ae9bfd1bf123c7a3"
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

