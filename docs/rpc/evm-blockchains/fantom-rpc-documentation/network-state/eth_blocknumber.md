# eth\_blockNumber

### How to use it

{% tabs %}
{% tab title="TypeScript/JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Fantom, Network } from '@tatumio/tatum'
  
const tatum = await TatumSDK.init<Fantom>({ network: Network.FANTOM })

const latestBlock = await tatum.rpc.blockNumber()

await tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Overview

The `eth_blockNumber` method returns the number of the most recent block on the blockchain. This method is commonly used to track the current state of the network, monitor for new blocks, or fetch historical data.

Use cases for `eth_blockNumber` include:

* Synchronising a local copy of the blockchain with the network
* Checking the status of a transaction by comparing its block number to the current block number
* Determining the current network state for smart contract interactions

### Parameters

The `eth_blockNumber` method does not require any parameters.

### Return Object

The `eth_blockNumber` method returns a single field:

* **`blockNumber`**: The number of the most recent block on the blockchain. The value is returned as a hexadecimal string.

### JSON-RPC Request Example

```json
{
  "id": 1,
  "jsonrpc": "2.0",
  "method": "eth_blockNumber",
  "params": []
}
```

### JSON-RPC Response Example

```json
{
  "id": 1,
  "jsonrpc": "2.0",
  "result": "0x4b7" // 1207
}
```

In this example, the most recent block number is 1207 (`0x4b7` in hexadecimal notation).

Please note that while this document provides a comprehensive description of the `eth_blockNumber` method, other methods may be needed to obtain full transaction details or perform more complex tasks. 