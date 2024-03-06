# eth\_getTransactionByHash

### How to use it

{% tabs %}
{% tab title="TypeScript/JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Cronos, Network } from '@tatumio/tatum'
  
const tatum = await TatumSDK.init<Cronos>({network: Network.CRONOS})

const tx = await tatum.rpc.getTransactionByHash('0x068f00756843c4fa018771decb06767e0e6a57045eabcbce1125a56115f2742a')

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
  * Example: `"0x068f00756843c4fa018771decb06767e0e6a57045eabcbce1125a56115f2742a"`

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