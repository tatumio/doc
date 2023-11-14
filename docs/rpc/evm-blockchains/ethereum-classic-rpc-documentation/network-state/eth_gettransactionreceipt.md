# eth\_getTransactionReceipt

### How to use it

{% tabs %}
{% tab title="TypeScript/JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, EthereumClassic, Network } from '@tatumio/tatum'
  
const tatum = await TatumSDK.init<EthereumClassic>({network: Network.ETHEREUM_CLASSIC})

const tx = await tatum.rpc.getTransactionReceipt('0x311b9228c7eb66500a3bc01162e0c7d3687e1df84d2e9b6104a87f8178b608c1')

await tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Overview

`eth_getTransactionReceipt` is an Flare JSON-RPC method that retrieves the transaction receipt of a given transaction hash. This method is particularly useful when you need to obtain detailed information about a transaction's execution, such as its status (success or failure), gas usage, and logs (events). Common use cases include checking the status of a transaction after it has been mined or inspecting the events emitted by a smart contract during a specific transaction.

### Parameters

This method requires a single parameter:

* **`transactionHash`**: The hash of the transaction for which you want to obtain the receipt.
  * Example: `"0xa536596d043c03d709aaccbc53f421963fe3537274e86444cd984404cf9ecb13"`

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
  "method": "eth_getTransactionReceipt",
  "params": [
    "0xa536596d043c03d709aaccbc53f421963fe3537274e86444cd984404cf9ecb13"
  ]
}
```

Response:

```json
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": {
        "blockHash": "0x1091a5831b3556e80e53598c24e9d592e104dba0428f47f94c61523eb52d09d8",
        "blockNumber": "0x316624",
        "contractAddress": null,
        "cumulativeGasUsed": "0x7ad81",
        "effectiveGasPrice": "0x306dc421e",
        "from": "0x53e8577c4347c365e4e0da5b57a589cb6f2ab848",
        "gasUsed": "0x3c518",
        "logs": [
            {
                "address": "0x211500d1960bdb7ba3390347ffd8ad486b897a18",
                "topics": [
                    "0xddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef",
                    "0x0000000000000000000000000000000000000000000000000000000000000000",
                    "0x00000000000000000000000074b4551c177592a908c6ab9ce671bfe8c1b5bd40",
                    "0x000000000000000000000000000000000000000000000000000056b990e70e00"
                ],
                "data": "0x",
                "blockNumber": "0x316624",
                "transactionHash": "0xa536596d043c03d709aaccbc53f421963fe3537274e86444cd984404cf9ecb13",
                "transactionIndex": "0x4",
                "blockHash": "0x1091a5831b3556e80e53598c24e9d592e104dba0428f47f94c61523eb52d09d8",
                "logIndex": "0x3",
                "removed": false
            }
        ],
        "logsBloom": "0x00000000000000000000000000000000000000000000000000020000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000008000000000000000000000000000000000000000000000000020000010000000000000800000000000000000000000010000040000000000000000000000000000000000000000000000000000000000000000000000000004000000000000000000000000000100000000000000000000000000000000002000000200000000000100000000000800000000000000000000020000000000000000000000200000000000000000000000000000000000000000000",
        "status": "0x1",
        "to": "0x211500d1960bdb7ba3390347ffd8ad486b897a18",
        "transactionHash": "0xa536596d043c03d709aaccbc53f421963fe3537274e86444cd984404cf9ecb13",
        "transactionIndex": "0x4",
        "type": "0x0"
    }
}
```

\
