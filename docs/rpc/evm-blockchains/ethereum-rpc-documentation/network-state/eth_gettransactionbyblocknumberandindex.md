# eth\_getTransactionByBlockNumberAndIndex

### How to use it

{% tabs %}
{% tab title="TypeScript/JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Ethereum, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Ethereum>({network: Network.ETHEREUM})

const tx = await tatum.rpc.getTransactionByBlockNumberAndIndex(10123321, 0)

await tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
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

{% embed url="https://codepen.io/tatum-devrel/pen/RwqvRNp" %}

### Parameters

The `eth_getTransactionByBlockHashAndIndex` method accepts two parameters:

1. `blockNumber` (required): either hexadecimal or decimal value
   * Example: 10123321
2. `transactionIndex` (required): The index of the transaction within the specified block. The index is a hexadecimal or decimal value.
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
    "method": "eth_getTransactionByBlockNumberAndIndex",
    "params": [
        10123321,
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
    "blockHash": "0x103eca282ca064902fa3e15ad705bcf52cff6a5d0e9ad7b077a503268f6aa317",
    "blockNumber": "0x9a7839",
    "from": "0xcabda7c04a240498636ee0e535e0596b504c66d2",
    "gas": "0x5208",
    "gasPrice": "0xfd51da9a3",
    "hash": "0x93f11750429ae0f792a584b0dca215c52c40b506086ceb16fb3200932939116f",
    "input": "0x",
    "nonce": "0x22e4",
    "to": "0x3cd76d4a67ebd1c88cd8cf613c4551199cccae4d",
    "transactionIndex": "0x0",
    "value": "0x46bdf53e068dc0000",
    "type": "0x0",
    "v": "0x1c",
    "r": "0x3a7ae13274733eac63e388a0f95568122431134ccbb1f408eedd4f3a579263a0",
    "s": "0x5362b2ad9c89e8c0be551a81b77945090351482abe30592f28ae869ff87ad1c5"
  }
}

```
