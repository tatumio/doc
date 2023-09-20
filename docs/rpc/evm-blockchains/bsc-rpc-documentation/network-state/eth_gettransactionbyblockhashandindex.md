# eth\_getTransactionByBlockHashAndIndex

### How to use it

{% tabs %}
{% tab title="TypeScript/JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, BinanceSmartChain, Network} from '@tatumio/tatum'

const tatum = await TatumSDK.init<BinanceSmartChain>({network: Network.BINANCE_SMART_CHAIN})

const tx = await tatum.rpc.getTransactionByBlockHashAndIndex('0xd109a2054e3301c446573859bcbdb0fb26107ea1c218d097042b34e3bd8f6d91', 0)

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

1. `blockHash` (required): The hash of the block containing the transaction.
   * Example: `"0xd109a2054e3301c446573859bcbdb0fb26107ea1c218d097042b34e3bd8f6d91"`
2. `transactionIndex` (required): The index of the transaction within the specified block. The index is a number in decimal.
   * Example: 0

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
        "0xd109a2054e3301c446573859bcbdb0fb26107ea1c218d097042b34e3bd8f6d91",
        0
    ]
}
```

Response:

```json
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": {
        "blockHash": "0xd109a2054e3301c446573859bcbdb0fb26107ea1c218d097042b34e3bd8f6d91",
        "blockNumber": "0x1e3c1a1",
        "from": "0x071e5581ea04d93336fd6d2557c56f5c6ab2bea8",
        "gas": "0x35b63",
        "gasPrice": "0x5af993e87",
        "hash": "0x7d05b7e686241f7aa0593e30c819fc59deb14154576b9d048820726079cf1c69",
        "input": "0x0000000000000000000001edd108f9d850100000000003e7dc5f9076ab0000004e5cb88aaf8227d9b7e61a7555cee07c617941ee0033",
        "nonce": "0x14089d",
        "to": "0x0000000000016a723d0d576df7dc79ec149ac760",
        "transactionIndex": "0x0",
        "value": "0x0",
        "type": "0x0",
        "v": "0x93",
        "r": "0xbe4a49be222942d61aad6f995b33fe59aefeaf2c8e8d9a3fea595e11ec03810b",
        "s": "0x3b22209ddfcc3737de2990195dd9b6bb350f1fb6265e7d06789abaa619467d1e"
    }
}
```
