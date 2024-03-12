# eth_getTransactionReceipt

### How to use it

{% tabs %}
{% tab title="TypeScript/JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}

```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Base, Network } from "@tatumio/tatum";

const tatum = await TatumSDK.init<Base>({ network: Network.BASE });

const tx = await tatum.rpc.getTransactionReceipt(
  "0xeee8769601cf91488cc09dfd3f707bafc4b286c49c4c15814999ca6a3977e44b"
);

await tatum.destroy(); // Destroy Tatum SDK - needed for stopping background jobs
```

{% endcode %}
{% endtab %}
{% endtabs %}

### Overview

`eth_getTransactionReceipt` is an method that retrieves the transaction receipt of a given transaction hash. This method is particularly useful when you need to obtain detailed information about a transaction's execution, such as its status (success or failure), gas usage, and logs (events). Common use cases include checking the status of a transaction after it has been mined or inspecting the events emitted by a smart contract during a specific transaction.

### Parameters

This method requires a single parameter:

- **`transactionHash`**: The hash of the transaction for which you want to obtain the receipt.
  - Example: `"0xeee8769601cf91488cc09dfd3f707bafc4b286c49c4c15814999ca6a3977e44b"`

### Return Object

The method returns an object containing the following fields:

- **`transactionHash`**: The hash of the transaction.
- **`transactionIndex`**: The transaction's index position in the block.
- **`blockHash`**: The hash of the block where this transaction was mined.
- **`blockNumber`**: The block number where this transaction was mined.
- **`from`**: The address of the sender.
- **`to`**: The address of the receiver. `null` when it's a contract creation transaction.
- **`cumulativeGasUsed`**: The total amount of gas used when this transaction was executed in the block.
- **`gasUsed`**: The amount of gas used by this specific transaction alone.
- **`contractAddress`**: The address of the contract created, if the transaction was a contract creation. Otherwise, `null`.
- **`logs`**: An array of log objects, which were emitted during the transaction.
- **`logsBloom`**: A 256-byte bloom filter, which is a compressed representation of the logs emitted during the transaction.
- **`status`**: The status of the transaction's execution. `"0x1"` indicates success, while `"0x0"` indicates failure.

### Response:

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": {
    "blockHash": "0x75e58e08a9f3a23bac9788d5077a9365abb5c29ec1aab70891264051624720af",
    "blockNumber": "0x1143497",
    "contractAddress": null,
    "cumulativeGasUsed": "0x9382e0",
    "effectiveGasPrice": "0x35ef89748",
    "from": "0x2b862fe79a56419979e97b95f910b93f6d338e33",
    "gasUsed": "0x2b7fe",
    "logs": [
      [Object],
      [Object],
      [Object],
      [Object],
      [Object],
      [Object]
    ],
    "logsBloom": "0x0..."
    "status": "0x1",
    "to": "0xb517850510997a34b4ddc8c3797b4f83fad510c4",
    "transactionHash": "0x2a4811309750a84058d2fd1bd8dd534bf3a34039ff1b34e29f23a92dfb06449d",
    "transactionIndex": "0x4c",
    "type": "0x2"
  }
}

```
