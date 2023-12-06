# eth\_getTransactionByHash

### How to use it

{% tabs %}
{% tab title="TypeScript/JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum
  
import { TatumSDK, Optimism, Network } from '@tatumio/tatum'
  
const tatum = await TatumSDK.init<Optimism>({network: Network.OPTIMISM})  

const tx = await tatum.rpc.getTransactionByHash('0x501bc07b1e3346dabe68c6c0bee7fa52ea59c829396cd621cde0b61829321e58')

await tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Overview

`eth_getTransactionByHash` is an [JSON-RPC](https://community.optimism.io/docs/developers/build/json-rpc/) method that allows you to query transaction details based on its hash. This method is useful when you want to retrieve information about a specific transaction, such as its sender, receiver, value, and more. Common use cases include tracking transaction status, monitoring incoming transactions, or analyzing historical transaction data.

### Parameters

The `eth_getTransactionByHash` method takes one parameter:

* **`transactionHash`**: The hash of the transaction you want to retrieve. This should be a 32-byte hash string with a `0x` prefix.
  * Example: `"0xa536596d043c03d709aaccbc53f421963fe3537274e86444cd984404cf9ecb13"`

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
  "params": ["0xa536596d043c03d709aaccbc53f421963fe3537274e86444cd984404cf9ecb13"],
  "id": 1
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
        "from": "0x53e8577c4347c365e4e0da5b57a589cb6f2ab848",
        "gas": "0x3c524",
        "gasPrice": "0x306dc421e",
        "hash": "0xa536596d043c03d709aaccbc53f421963fe3537274e86444cd984404cf9ecb13",
        "input": "0x50bb4e7f00000000000000000000000074b4551c177592a908c6ab9ce671bfe8c1b5bd40000000000000000000000000000000000000000000000000000056b990e70e000000000000000000000000000000000000000000000000000000000000000060000000000000000000000000000000000000000000000000000000000000006068747470733a2f2f6574682d6d61696e6e65742e672e616c6368656d792e636f6d2f76322f72646f704c505054424a31536f786b2d555179306b7464676f4b45326146637a2f6765744e4654732f3f6f776e65723d766974616c696b2e657468",
        "nonce": "0xc97",
        "to": "0x211500d1960bdb7ba3390347ffd8ad486b897a18",
        "transactionIndex": "0x4",
        "value": "0x0",
        "type": "0x0",
        "chainId": "0xaa36a7",
        "v": "0x1546d71",
        "r": "0xf89098451217613aa4abbb3f8988e75e20ae948d07bf8b26c472bc9bda50c9d9",
        "s": "0x15cfb5b34bcb23730aeadc28df3b66fa9cf28103ffc8b557d76f0c1df078028e"
    }
}
```

\
