# eth\_getTransactionByHash

### How to use it

{% tabs %}
{% tab title="TypeScript/JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, BinanceSmartChain, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<BinanceSmartChain>({network: Network.BINANCE_SMART_CHAIN})

const tx = await tatum.rpc.getTransactionByHash('0xc5e257842e8fb62e286350d4bdddcaf24cb30dae4b8ec25ad3e52f463e16e656')

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Overview

`eth_getTransactionByHash` is an JSON-RPC method that allows you to query transaction details based on its hash. This method is useful when you want to retrieve information about a specific transaction, such as its sender, receiver, value, and more. Common use cases include tracking transaction status, monitoring incoming transactions, or analyzing historical transaction data.

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
  jsonrpc: '2.0',
  id: 1,
  result: {
    blockHash: '0x283da208c3429f3c3c38fc2c0a94bc767c9c2197962393cd4d79c6d6f2938b48',
    blockNumber: '0x1e3bb30',
    from: '0x35a84e6896aa5ba047221ac405afaf1977a75109',
    gas: '0x5208',
    gasPrice: '0xb2d05e00',
    hash: '0xc5e257842e8fb62e286350d4bdddcaf24cb30dae4b8ec25ad3e52f463e16e656',
    input: '0x',
    nonce: '0x4',
    to: '0x8aca17bcb5eed52e9854528d131d830149e9cdc0',
    transactionIndex: '0x35',
    value: '0x2386f26fc10000',
    type: '0x0',
    v: '0x94',
    r: '0xdb1edfd341493c5309952a880db14f291820940f78cedfe0639a65babe564c5a',
    s: '0x334ba27525743ff412e66b07bcb3683d0ed565edbad5a3e30ddd5d7f46233818'
  }
}
```

\
