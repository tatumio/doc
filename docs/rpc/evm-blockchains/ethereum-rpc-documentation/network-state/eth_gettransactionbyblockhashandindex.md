# eth\_getTransactionByBlockHashAndIndex

### How to use it

{% tabs %}
{% tab title="TypeScript/JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Ethereum, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Ethereum>({network: Network.ETHEREUM})

const tx = await tatum.rpc.getTransactionByBlockHashAndIndex('0x2907402477167193008a0cbbaa8073278c48e8b97bf9ed1a2101f6ad2130dbaf', 1)

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Overview

`eth_getTransactionByBlockHashAndIndex` is an Ethereum JSON-RPC method that allows you to fetch the transaction details based on the block hash and the index of the transaction within that block. This method can be useful when you want to retrieve transaction details for a specific transaction without knowing its transaction hash.

Use cases for this method may include:

* Inspecting transaction details for debugging purposes
* Gathering data for transaction analysis
* Fetching transaction information for specific blocks in a block explorer application

{% embed url="https://codepen.io/tatum-devrel/pen/jOQojOV" %}

### Parameters

The `eth_getTransactionByBlockHashAndIndex` method accepts two parameters:

1. `blockHash` (required): The hash of the block containing the transaction.
   * Example: `"0x2907402477167193008a0cbbaa8073278c48e8b97bf9ed1a2101f6ad2130dbaf"`
2. `transactionIndex` (required): The index of the transaction within the specified block. The index is a hexadecimal value.
   * Example: `"0x1"`

### Return Object

The method returns a JSON object containing the following fields:

1. `hash`: The transaction hash as a 32-byte hex string.
2. `nonce`: The number of transactions made by the sender prior to this one.
3. `blockHash`: The hash of the block in which this transaction is included.
4. `blockNumber`: The block number in which this transaction is included.
5. `transactionIndex`: The index of the transaction within the block.
6. `from`: The address of the sender.
7. `to`: The address of the recipient. `null` if the transaction is a contract creation transaction.
8. `value`: The value transferred in wei.
9. `gasPrice`: The gas price provided by the sender in wei.
10. `gas`: The gas limit provided by the sender.
11. `input`: The data sent along with the transaction.

### JSON Examples

Request:

```json
{
    "jsonrpc": "2.0",
    "id": 1,
    "method": "eth_getTransactionByBlockHashAndIndex",
    "params": [
        "0x2907402477167193008a0cbbaa8073278c48e8b97bf9ed1a2101f6ad2130dbaf",
        "0x1"
    ]
}
```

Response:

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": {
    "blockHash": "0x2907402477167193008a0cbbaa8073278c48e8b97bf9ed1a2101f6ad2130dbaf",
    "blockNumber": "0x110e3f0",
    "from": "0xcfdda03e6167ad55392c03d962a9da1bec513a23",
    "gas": "0x39dca",
    "gasPrice": "0x4601d234d",
    "maxFeePerGas": "0x51cad3075",
    "maxPriorityFeePerGas": "0x2faf080",
    "hash": "0x9272e601263cf89cc3b5d65d33f8d708f9eb547b8d0d419cc0646361a8c8cca2",
    "input": "0x3593564c000000000000000000000000000000000000000000000000000000000000006000000000000000000000000000000000000000000000000000000000000000a00000000000000000000000000000000000000000000000000000000064d4cec300000000000000000000000000000000000000000000000000000000000000020b0800000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000020000000000000000000000000000000000000000000000000000000000000040000000000000000000000000000000000000000000000000000000000000000020000000000000000000000000000000000000000000000000de0b6b3a7640000000000000000000000000000000000000000000000000000000000000000010000000000000000000000000000000000000000000000000000000000000000010000000000000000000000000000000000000000000000000de0b6b3a76400000000000000000000000000000000000000000000000000085347052c302c70f700000000000000000000000000000000000000000000000000000000000000a000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000002000000000000000000000000c02aaa39b223fe8d0a0e5c4f27ead9083c756cc20000000000000000000000008c130499d33097d4d000d3332e1672f75b431543",
    "nonce": "0x29",
    "to": "0x3fc91a3afd70395cd496c647d5a6cc9d4b2b7fad",
    "transactionIndex": "0x1",
    "value": "0xde0b6b3a7640000",
    "type": "0x2",
    "accessList": [],
    "chainId": "0x1",
    "v": "0x1",
    "r": "0x6e3b191997b04e9b58bc2ada242830a6445ab233ea0971a53f9eceed7850cbfd",
    "s": "0x4cd69316c2f5e54d48df588f03d527904e7300ee4477dfaca436844ecb11cbd1",
    "yParity": "0x1"
  }
}
```
