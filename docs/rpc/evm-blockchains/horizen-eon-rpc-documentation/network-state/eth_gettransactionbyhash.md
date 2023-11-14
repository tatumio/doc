# eth\_getTransactionByHash

### How to use it

{% tabs %}
{% tab title="TypeScript/JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, HorizenEon, Network } from '@tatumio/tatum'
  
const tatum = await TatumSDK.init<HorizenEon>({network: Network.HORIZEN_EON})

const tx = await tatum.rpc.getTransactionByHash('0x97d83656ca05890100149be18d0c2a2f94e5337e5e6a643ea78794cd418cdbc7')

await tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Overview

`eth_getTransactionByHash` is an JSON-RPC method that allows you to query transaction details based on its hash. This method is useful when you want to retrieve information about a specific transaction, such as its sender, receiver, value, and more. Common use cases include tracking transaction status, monitoring incoming transactions, or analyzing historical transaction data.

### Parameters

The `eth_getTransactionByHash` method takes one parameter:

* **`transactionHash`**: The hash of the transaction you want to retrieve. This should be a 32-byte hash string with a `0x` prefix.
  * Example: `"0x97d83656ca05890100149be18d0c2a2f94e5337e5e6a643ea78794cd418cdbc7"`

### Return Object

The method returns a transaction object with the following fields:

* **`hash`**: The hash of the transaction (32 bytes).
* **`nonce`**: The number of transactions sent by the sender prior to this one (integer).
* **`blockHash`**: The hash of the block in which the transaction was included (32 bytes), or `null` if the transaction is not yet mined.
* **`blockNumber`**: The block number in which the transaction was included (integer), or `null` if the transaction is not yet mined.
* **`transactionIndex`**: The index of the transaction in the block (integer), or `null` if the transaction is not yet mined.
* **`from`**: The address of the sender (20 bytes).
* **`to`**: The address of the receiver (20 bytes), or `null` for contract creation transactions.
* **`value`**: The value transferred in the transaction, in wei.
* **`gasPrice`**: The price of gas for the transaction, in wei.
* **`maxFeePerGas`** - The maximum fee per gas set in the transaction.
* **`maxPriorityFeePerGas`** - The maximum priority gas fee set in the transaction.
* **`gas`**: The maximum amount of gas the transaction is allowed to consume.
* **`input`**: The data payload of the transaction (string), or `0x` for simple value transfers.

### JSON-RPC Examples

Request:

```json
{
  "jsonrpc": "2.0",
  "method": "eth_getTransactionByHash",
  "params": ["0x97d83656ca05890100149be18d0c2a2f94e5337e5e6a643ea78794cd418cdbc7"],
  "id": 1
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
    "hash": "0x97d83656ca05890100149be18d0c2a2f94e5337e5e6a643ea78794cd418cdbc7",
    "type": "0x2",
    "nonce": "0x1d8",
    "from": "0x8bd5723981d3f96a6544519c4a075f5994919d3a",
    "to": "0xa55d9ef16af921b70fed1421c1d298ca5a3a18f1",
    "value": "0x0",
    "input": "0x3798c7f2000000000000000000000000000000000000000000000000000000000000008000000000000000000000000000000000000000000000000000000000000003400000000000000000000000000000000000000000000000000000000065082bd900000000000000000000000000000000000000000000000000000000013ebef0000000000000000000000000000000000000000000000000000000000000000700000000000000000000000000000000000000000000000000000000000000e00000000000000000000000000000000000000000000000000000000000000120000000000000000000000000000000000000000000000000000000000000016000000000000000000000000000000000000000000000000000000000000001a000000000000000000000000000000000000000000000000000000000000001e0000000000000000000000000000000000000000000000000000000000000022000000000000000000000000000000000000000000000000000000000000002600000000000000000000000000000000000000000000000000000000000000003415242000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000034254430000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000344414900000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000003455448000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000024f50000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000455534443000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000004555344540000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000070000000000000000000000000000000000000000000000000000000031339e8d000000000000000000000000000000000000000000000000000018a759056108000000000000000000000000000000000000000000000000000000003b9aca000000000000000000000000000000000000000000000000000000017fc9b3dfb80000000000000000000000000000000000000000000000000000000054572fc0000000000000000000000000000000000000000000000000000000003b9aca00000000000000000000000000000000000000000000000000000000003b9b181f",
    "gas": "0x12a68",
    "gasPrice": "0x5017ff700",
    "maxPriorityFeePerGas": "0x59682f00",
    "maxFeePerGas": "0xba43b7400",
    "chainId": "0x1ca4",
    "v": "0x1c",
    "r": "0x75884978fae04ee04de9a2d4fefaaaa4742f4e8f4ccdaf89b01238bafb5292fd",
    "s": "0x1f0e92ae5b7f2c8805ebb07900a59a04e73cda12a309021849a5d9ed151d7fd1",
    "accessList": []
  }
}
```

\
