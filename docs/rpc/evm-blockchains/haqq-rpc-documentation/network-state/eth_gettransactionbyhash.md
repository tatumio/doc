# eth\_getTransactionByHash

### How to use it

{% tabs %}
{% tab title="TypeScript/JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Haqq, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Haqq>({network: Network.HAQQ})

const tx = await tatum.rpc.getTransactionByHash('0xf920dd038c8264244bc7faab54d3f0c1256f992c744a134f0e5886a73107e536')

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Overview

`eth_getTransactionByHash` is an Haqq JSON-RPC method that allows you to query transaction details based on its hash. This method is useful when you want to retrieve information about a specific transaction, such as its sender, receiver, value, and more. Common use cases include tracking transaction status, monitoring incoming transactions, or analyzing historical transaction data.

{% embed url="https://codepen.io/Jan-Musil-the-lessful/pen/MWzLxGd?editors=1111" %}

### Parameters

The `eth_getTransactionByHash` method takes one parameter:

* **`transactionHash`**: The hash of the transaction you want to retrieve. This should be a 32-byte hash string with a `0x` prefix.
  * Example: `"0xf920dd038c8264244bc7faab54d3f0c1256f992c744a134f0e5886a73107e536"`

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
  "params": ["0xf920dd038c8264244bc7faab54d3f0c1256f992c744a134f0e5886a73107e536"],
  "id": 1
}
```

Response:

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": {
    "blockHash": "0xc9a74365087632df3824877d8515f4fca6152148c393d427b5a1f73b6b48216a",
    "blockNumber": "0x10a24fe",
    "from": "0x1f9090aae28b8a3dceadf281b0f12828e676c326",
    "gas": "0x565f",
    "gasPrice": "0x4920f718b",
    "maxFeePerGas": "0x4920f718b",
    "maxPriorityFeePerGas": "0x0",
    "hash": "0x06b57a2430c71328be4f86a7bf8bb18cdbe2d55725791733f4eb6151012319a1",
    "input": "0x",
    "nonce": "0x1c0fa",
    "to": "0x388c818ca8b9251b393131c08a736a67ccb19297",
    "transactionIndex": "0xc5",
    "value": "0x18c6d8afd7453e2",
    "type": "0x2",
    "accessList": [],
    "chainId": "0x1",
    "v": "0x0",
    "r": "0x9ce24e115c0b85be0c14a6b58fe87f41a5c0179432ec09717edbcd46ff33ab25",
    "s": "0x2184449629568a4b3c5420108bf4f5c270d36cf81d11ea7590f010de7bf335a6"
  }

```

\
