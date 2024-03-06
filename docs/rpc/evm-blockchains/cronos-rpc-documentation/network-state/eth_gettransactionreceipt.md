# eth\_getTransactionReceipt

### How to use it

{% tabs %}
{% tab title="TypeScript/JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Cronos, Network } from '@tatumio/tatum'
  
const tatum = await TatumSDK.init<Cronos>({network: Network.CRONOS})

const tx = await tatum.rpc.getTransactionReceipt('0x6aefbd1a9c9e4c310cadde3bcdd809a14da87caa8fa4f10ca04d9e357a3907e9')

await tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Overview

`eth_getTransactionReceipt` is an JSON-RPC method that retrieves the transaction receipt of a given transaction hash. This method is particularly useful when you need to obtain detailed information about a transaction's execution, such as its status (success or failure), gas usage, and logs (events). Common use cases include checking the status of a transaction after it has been mined or inspecting the events emitted by a smart contract during a specific transaction.

### Parameters

This method requires a single parameter:

* **`transactionHash`**: The hash of the transaction for which you want to obtain the receipt.
  * Example: `"0x068f00756843c4fa018771decb06767e0e6a57045eabcbce1125a56115f2742a"`

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