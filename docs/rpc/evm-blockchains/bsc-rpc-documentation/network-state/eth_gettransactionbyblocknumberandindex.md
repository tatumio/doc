# eth\_getTransactionByBlockNumberAndIndex

### How to use it

{% tabs %}
{% tab title="TypeScript/JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, BinanceSmartChain, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<BinanceSmartChain>({network: Network.BINANCE_SMART_CHAIN})

const tx = await tatum.rpc.getTransactionByBlockNumberAndIndex('0xAD7C5E', 0)

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Overview

`eth_getTransactionByBlockHashAndIndex` is an JSON-RPC method that allows you to fetch the transaction details based on the block hash and the index of the transaction within that block. This method can be useful when you want to retrieve transaction details for a specific transaction without knowing its transaction hash.

Use cases for this method may include:

* Inspecting transaction details for debugging purposes
* Gathering data for transaction analysis
* Fetching transaction information for specific blocks in a block explorer application

### Parameters

The `eth_getTransactionByBlockHashAndIndex` method accepts two parameters:

1. `blockNumber` (required): The hash of the block containing the transaction.
   * Example: `"0xAD7C5E"`
2. `transactionIndex` (required): The index of the transaction within the specified block. The index is a hexadecimal value.
   * Example: `"0x0"`

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
    "method": "eth_getTransactionByBlockNumberAndIndex",
    "params": [
        "0xAD7C5E",
        "0x0"
    ]
}
```

Response:

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": {
    "blockHash": "0xee7d93c17d84df49b2923ce6922a6d1d3dd7c9ad9e5a845c53de15309c2722ef",
    "blockNumber": "0xad7c5e",
    "from": "0xcd22db09c69935c3c660438fec1758f855def472",
    "gas": "0xdbba0",
    "gasPrice": "0x9502f9000",
    "hash": "0x182c841ef47c1505e1e38677b9f1cfea74ad5a380e31e6b05b68279e9d332e99",
    "input": "0x095ea7b300000000000000000000000010ed43c718714eb63d5aa57b78b54704e256024effffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff",
    "nonce": "0xd",
    "to": "0x5e12bb6ddd9214923d6c837ddf1ffb9c90f18883",
    "transactionIndex": "0x0",
    "value": "0x0",
    "type": "0x0",
    "v": "0x94",
    "r": "0xa4967df17dd1418b50808e44019335b6ff831e17962c1e143777c2808d7f2cd0",
    "s": "0x43bdb946e52562c586ac6bf04e7d4c7e7252d2bfb455d3f5f486f64f34e40c33"
  }
}
```
