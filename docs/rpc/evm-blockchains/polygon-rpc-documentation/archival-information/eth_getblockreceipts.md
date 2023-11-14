# eth\_getBlockReceipts

### How to use it

{% tabs %}
{% tab title="TypeScript/JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Polygon, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Ethereum>({network: Network.POLYGON})

const result = await tatum.rpc.getBlockReceipts(47292218)

await tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Overview&#x20;

`eth_getBlockReceipts` method retrieves and returns all transaction receipts for a specific block. Transaction receipts contain essential information related to the execution status and outcomes of individual transactions within the block, including details about the amount of gas used, contract events emitted, and whether the transactions were successful or not.&#x20;

By using the `eth_getBlockReceipts`, developers can seek a comprehensive overview of the transactions' results within a particular block.

### Parameters

The `eth_getBlockReceipts` method accepts the following parameters:

* `blockNumber` - `Quantity` or `String`
  * The block number of the block to trace.
  * Example: `"0x1"` or `"latest"`

### Return Object

`eth_getBlockReceipts` method provides a detailed set of information for each transaction receipt within a given block. The returned data includes:

* `blockHash`: The hash of the block (null if pending).
* `blockNumber`: The block number.
* `contractAddress`: The contract address created if the transaction was for contract creation; otherwise, null.
* `cumulativeGasUsed`: The total amount of gas used when this transaction was executed in the block.
* `effectiveGasPrice`: The actual value per gas deducted from the sender account.
* from: The address of the sender.
* `gasUsed`: The amount of gas used by this specific transaction alone.
* `logs`: An array of log objects that generated this transaction, containing:
  * `address`: The address from which this log originated.
  * topics: In Solidity, the first topic is the hash of the signature of the event, unless the event is declared with the anonymous specifier.
  * `data`: It contains one or more 32 Bytes non-indexed arguments of the log.
  * `blockNumber`: The block number where this log was in.
  * `transactionHash`: The hash of the transaction this log was created from, or null if it's a pending log.
  * `transactionIndex`: The integer of the transaction's index position that the log was created fromr null if it's a pending log.
  * `blockHash`: The hash of the block where this log was inr null if it's a pending log.
  * `logIndex`: The integer of the log index position in the blockr null if it's a pending log.
  * `removed`: It is true when the log was removed due to a chain reorganization, and false if it's a valid log.
* `logsBloom`: The bloom filter for light clients to quickly retrieve related logs.
* `status`: It is either 1 (success) or 0 (failure) encoded as a hexadecimal.
* `to`: The address of the receiver. It will be null when the transaction is for contract creation.
* `transactionHash`: The hash of the transaction.
* `transactionIndex`: The index of the transaction within the block.
* `type`: The value type.

{% hint style="info" %}
This method is available only on the full archive node.
{% endhint %}

### JSON-RPC Request and Response Examples

#### Request

```json
{
    "jsonrpc":"2.0",
    "method":"eth_getBlockReceipts",
    "params":["0x2a6a150"],
    "id":1
}
```

#### Response

```json
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": [
        {
            "blockHash": "0xfb368ca825fdf63ce3bd3c22344e9b50fcb56fc7341cce71192535c2f55ccf93",
            "blockNumber": "0x2a6a150",
            "contractAddress": null,
            "cumulativeGasUsed": "0x5b2a92",
            "effectiveGasPrice": "0x26b748cd1d",
            "from": "0x0d882c09a3e03aa9afb2967a1eebddd67934f7be",
            "gasUsed": "0xf840",
            "logs": [
                {
                    "address": "0x2791bca1f2de4661ed88a30c99a7a9449aa84174",
                    "topics": [
                        "0xddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef",
                        "0x0000000000000000000000000d882c09a3e03aa9afb2967a1eebddd67934f7be",
                        "0x00000000000000000000000073cc2c7189aa0d63ed0c243d42d3cd5210372067"
                    ],
                    "data": "0x0000000000000000000000000000000000000000000000000000000003750280",
                    "blockNumber": "0x2a6a150",
                    "transactionHash": "0x21b576878544bc1e8731d6fb120901bc6b7ecc27713f3bf1e2a75118f1fa35e3",
                    "transactionIndex": "0x36",
                    "blockHash": "0xfb368ca825fdf63ce3bd3c22344e9b50fcb56fc7341cce71192535c2f55ccf93",
                    "logIndex": "0xc3",
                    "removed": false
                },
                {
                    "address": "0x0000000000000000000000000000000000001010",
                    "topics": [
                        "0x4dfe1bbbcf077ddc3e01291eea2d5c70c2b422b415d95645b9adcfd678cb1d63",
                        "0x0000000000000000000000000000000000000000000000000000000000001010",
                        "0x0000000000000000000000000d882c09a3e03aa9afb2967a1eebddd67934f7be",
                        "0x00000000000000000000000002f70172f7f490653665c9bfac0666147c8af1f5"
                    ],
                    "data": "0x0000000000000000000000000000000000000000000000000006c601978b000000000000000000000000000000000000000000000000000932b9349556b3b25c000000000000000000000000000000000000000000000082c4b21c5f77055dc900000000000000000000000000000000000000000000000932b26e93bf28b25c000000000000000000000000000000000000000000000082c4b8e2610e905dc9",
                    "blockNumber": "0x2a6a150",
                    "transactionHash": "0x21b576878544bc1e8731d6fb120901bc6b7ecc27713f3bf1e2a75118f1fa35e3",
                    "transactionIndex": "0x36",
                    "blockHash": "0xfb368ca825fdf63ce3bd3c22344e9b50fcb56fc7341cce71192535c2f55ccf93",
                    "logIndex": "0xc4",
                    "removed": false
                }
            ],
            "logsBloom": "0x00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000008000000000000000000000000000000000000002000000000008000000800000000000200000000110000000000000000000000000000000000000000001000000800000000180000010000000000001000000400000000000000000000000000000000000000000000000000000200000000000000000000000000000000000000000000000000000000000004000000002000000000001000000000000100000000000000000100000000000000000008000080000000000000000000000000000000000001000000000100000",
            "status": "0x1",
            "to": "0x2791bca1f2de4661ed88a30c99a7a9449aa84174",
            "transactionHash": "0x21b576878544bc1e8731d6fb120901bc6b7ecc27713f3bf1e2a75118f1fa35e3",
            "transactionIndex": "0x36",
            "type": "0x2"
        }
    ]
}
```
