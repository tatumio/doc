# eth\_getBlockReceipts

### How to use it

{% tabs %}
{% tab title="TypeScript/JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Ethereum, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Ethereum>({network: Network.ETHEREUM})

const result = await tatum.rpc.getBlockReceipts(10123321)

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
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
    "params":["0x10f5d58"],
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
            "blockHash": "0xf129ec079e3af6740128dde546e33ea85db2c46dbb7ea35f400a97bf837ec630",
            "blockNumber": "0x10f5d58",
            "contractAddress": null,
            "cumulativeGasUsed": "0x3f14c",
            "effectiveGasPrice": "0x174876e800",
            "from": "0xcf33ea41c015749f3ced2366364ef611d8d1425d",
            "gasUsed": "0x3f14c",
            "logs": [
                {
                    "address": "0xa62894d5196bc44e4c3978400ad07e7b30352372",
                    "topics": [
                        "0xddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef",
                        "0x000000000000000000000000cf33ea41c015749f3ced2366364ef611d8d1425d",
                        "0x000000000000000000000000a62894d5196bc44e4c3978400ad07e7b30352372"
                    ],
                    "data": "0x0000000000000000000000000000000000000000000000000002cbb24c4d2f98",
                    "blockNumber": "0x10f5d58",
                    "transactionHash": "0x81f1604ea2fa270307707d922d373e2e04069788334b648393aecb8c806ee6c0",
                    "transactionIndex": "0x0",
                    "blockHash": "0xf129ec079e3af6740128dde546e33ea85db2c46dbb7ea35f400a97bf837ec630",
                    "logIndex": "0x0",
                    "removed": false
                },
                {
                    "address": "0xa62894d5196bc44e4c3978400ad07e7b30352372",
                    "topics": [
                        "0xddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef",
                        "0x000000000000000000000000cf33ea41c015749f3ced2366364ef611d8d1425d",
                        "0x0000000000000000000000008e83de18b38ddc22166fb5454003a573a53be4ae"
                    ],
                    "data": "0x0000000000000000000000000000000000000000000000000114c5f381d9787d",
                    "blockNumber": "0x10f5d58",
                    "transactionHash": "0x81f1604ea2fa270307707d922d373e2e04069788334b648393aecb8c806ee6c0",
                    "transactionIndex": "0x0",
                    "blockHash": "0xf129ec079e3af6740128dde546e33ea85db2c46dbb7ea35f400a97bf837ec630",
                    "logIndex": "0x1",
                    "removed": false
                }
            ],
            "logsBloom": "0x00200000000000000000000080000000008000000000000000000000000000000000000000000000000000000000000102002010880120000000000000200000000000080000000800004008000000200000000000400800000002000020000000000000000000000000000000000000008000000000040000000010000800002000000000000000001020080000812000000000000000080000004000000000020080000000000000000000000000400000000200000000000000000010080000000002000000000000000000000000000000000000101000000002000000004010200000000000000000000000000000001000000000000000000000000000",
            "status": "0x1",
            "to": "0x3fc91a3afd70395cd496c647d5a6cc9d4b2b7fad",
            "transactionHash": "0x81f1604ea2fa270307707d922d373e2e04069788334b648393aecb8c806ee6c0",
            "transactionIndex": "0x0",
            "type": "0x2"
        },
        {
            "blockHash": "0xf129ec079e3af6740128dde546e33ea85db2c46dbb7ea35f400a97bf837ec630",
            "blockNumber": "0x10f5d58",
            "contractAddress": null,
            "cumulativeGasUsed": "0xbd884a",
            "effectiveGasPrice": "0x48ffe6b8e",
            "from": "0xdafea492d9c6733ae3d56b7ed1adb60692c98bc5",
            "gasUsed": "0x5208",
            "logs": [],
            "logsBloom": "0x00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000",
            "status": "0x1",
            "to": "0xe688b84b23f322a994a53dbf8e15fa82cdb71127",
            "transactionHash": "0x1104ac612589d19b6774ab1d8012c23036ebb5fae828b7a710acc6101b2b34bf",
            "transactionIndex": "0x99",
            "type": "0x2"
        }
    ]
}
```
