# eth\_getTransactionReceipt

### How to use it

{% tabs %}
{% tab title="TypeScript/JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Klaytn, Network } from '@tatumio/tatum'
  
const tatum = await TatumSDK.init<Klaytn>({network: Network.KLAYTN})

const tx = await tatum.rpc.getTransactionReceipt('0xa3fd3d2b01ee234899b487fb1480b7e14142dde55f07b7a079b9fdcf04733220')

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Overview

`klay_getTransactionReceipt` is an JSON-RPC method that retrieves the transaction receipt of a given transaction hash. This method is particularly useful when you need to obtain detailed information about a transaction's execution, such as its status (success or failure), gas usage, and logs (events). Common use cases include checking the status of a transaction after it has been mined or inspecting the events emitted by a smart contract during a specific transaction.

### Parameters

This method requires a single parameter:

* **`transactionHash`**: The hash of the transaction for which you want to obtain the receipt.
  * Example: `"0x97d83656ca05890100149be18d0c2a2f94e5337e5e6a643ea78794cd418cdbc7"`

### Return Object

The method returns an object containing the following fields:

* **`transactionHash`**: The hash of the transaction.
* **`transactionIndex`**: The transaction's index position in the block.
* **`blockHash`**: The hash of the block where this transaction was mined.
* **`blockNumber`**: The block number where this transaction was mined.
* **`from`**: The address of the sender.
* **`to`**: The address of the receiver. `null` when it's a contract creation transaction.
* **`cumulativeGasUsed`**: The total amount of gas used when this transaction was executed in the block.
* **`gasUsed`**: The amount of gas used by this specific transaction alone.
* **`contractAddress`**: The address of the contract created, if the transaction was a contract creation. Otherwise, `null`.
* **`logs`**: An array of log objects, which were emitted during the transaction.
* **`logsBloom`**: A 256-byte bloom filter, which is a compressed representation of the logs emitted during the transaction.
* **`status`**: The status of the transaction's execution. `"0x1"` indicates success, while `"0x0"` indicates failure.

### JSON-RPC Examples

Request:

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "klay_getTransactionReceipt",
  "params": [
    "0x97d83656ca05890100149be18d0c2a2f94e5337e5e6a643ea78794cd418cdbc7"
  ]
}
```

Response:

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": {
    "blockHash": "0xb0ddfcdcc375afce9f365458c5035ca4aaf99f9fe8699522193e16a8718615b6",
    "blockNumber": "0x5a9d4",
    "transactionIndex": "0x0",
    "transactionHash": "0x97d83656ca05890100149be18d0c2a2f94e5337e5e6a643ea78794cd418cdbc7",
    "type": "0x2",
    "from": "0x8bd5723981d3f96a6544519c4a075f5994919d3a",
    "to": "0xa55d9ef16af921b70fed1421c1d298ca5a3a18f1",
    "effectiveGasPrice": "0x5017ff700",
    "contractAddress": null,
    "logs": [],
    "logsBloom": "0x00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000",
    "gasUsed": "0x12a68",
    "cumulativeGasUsed": "0x12a68",
    "status": "0x1"
  }
}
```

\
