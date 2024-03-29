# eth_getUncleCountByBlockNumber

### How to use it

{% tabs %}
{% tab title="TypeScript/JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}

```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Base, Network } from "@tatumio/tatum";

const tatum = await TatumSDK.init<Base>({ network: Network.BASE });

const result = await tatum.rpc.getUncleCountByBlockNumber(15537345);

await tatum.destroy(); // Destroy Tatum SDK - needed for stopping background jobs
```

{% endcode %}
{% endtab %}
{% endtabs %}

### Overview

The `eth_getUncleCountByBlockHash` method returns the number of uncles in a specified block by its hash. This method can be useful for gathering information about the performance of the network and to analyse the security of the blockchain.

Uncles are blocks that are not included in the main blockchain but are still valid, and they contribute to the overall security and decentralisation of the network. The inclusion of uncles helps prevent centralisation and ensures the mining process remains competitive.

{% embed url="https://codepen.io/Jan-Musil-the-lessful/pen/vYQPXer" %}

### Parameters

The `eth_getUncleCountByBlockHash` method takes one parameter:

- `blockNumber`: The number of the block for which you want to get the uncle count.
  - Example value: 15537345

### Return Object

The return object for this method is a hex-encoded integer representing the number of uncles in the specified block.

- Example value: `"0x1"` (1 uncle)

### Request and Response Examples

Here is an example request and response for the `eth_getUncleCountByBlockNumber` method:

**Request:**

```json
{
  "id": 1,
  "jsonrpc": "2.0",
  "method": "eth_getUncleCountByBlockNumber",
  "params": ["0xED14C1"]
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

In this example, the request asks for the number of uncles in the block with the specified hash. The response indicates that there is one uncle in the block.

\
