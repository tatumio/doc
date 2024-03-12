# eth_getTransactionByHash

### How to use it

{% tabs %}
{% tab title="TypeScript/JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}

```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Base, Network } from "@tatumio/tatum";

const tatum = await TatumSDK.init<Base>({ network: Network.BASE });

const tx = await tatum.rpc.getTransactionByHash(
  "0x48e0232d926a32d220feb670db77936c0a69db7a23c09c7e49bd63b9b2b16388"
);

await tatum.destroy(); // Destroy Tatum SDK - needed for stopping background jobs
```

{% endcode %}
{% endtab %}
{% endtabs %}

### Overview

`eth_getTransactionByHash` is an method that allows you to query transaction details based on its hash. This method is useful when you want to retrieve information about a specific transaction, such as its sender, receiver, value, and more. Common use cases include tracking transaction status, monitoring incoming transactions, or analyzing historical transaction data.

### Parameters

The `eth_getTransactionByHash` method takes one parameter:

- **`transactionHash`**: The hash of the transaction you want to retrieve. This should be a 32-byte hash string with a `0x` prefix.
  - Example: `"0x48e0232d926a32d220feb670db77936c0a69db7a23c09c7e49bd63b9b2b16388"`

### Return Object

The method returns a transaction object with the following fields:

- **`hash`**: The hash of the transaction (32 bytes).
- **`nonce`**: The number of transactions sent by the sender prior to this one (integer).
- **`blockHash`**: The hash of the block in which the transaction was included (32 bytes), or `null` if the transaction is not yet mined.
- **`blockNumber`**: The block number in which the transaction was included (integer), or `null` if the transaction is not yet mined.
- **`transactionIndex`**: The index of the transaction in the block (integer), or `null` if the transaction is not yet mined.
- **`from`**: The address of the sender (20 bytes).
- **`to`**: The address of the receiver (20 bytes), or `null` for contract creation transactions.
- **`value`**: The value transferred in the transaction, in wei.
- **`gasPrice`**: The price of gas for the transaction, in wei.
- **`maxFeePerGas`** - The maximum fee per gas set in the transaction.
- **`maxPriorityFeePerGas`** - The maximum priority gas fee set in the transaction.
- **`gas`**: The maximum amount of gas the transaction is allowed to consume.
- **`input`**: The data payload of the transaction (string), or `0x` for simple value transfers.

### Response:

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": {
    "blockHash": "0xd1d718c5aef254e044928c1afeffd1c62e8c8566075b4ce70102a0185f15fe5b",
    "blockNumber": "0x1149605",
    "from": "0x0712663d09c8da4fdaa43d3ebd87a03c14ca9a5a",
    "gas": "0x7b0c",
    "gasPrice": "0x75de7040b",
    "maxFeePerGas": "0x93e78c23c",
    "maxPriorityFeePerGas": "0x828f156",
    "hash": "0x97696c2014695e851d85a344cbbc6ae8ab9d386de05cb0230fe50b91c044639b",
    "input": "0x",
    "nonce": "0x21b",
    "to": "0x698f26578e9955e0ef9f849a778feeadf43658ac",
    "transactionIndex": "0x39",
    "value": "0x20c0677f05ec0000",
    "type": "0x2",
    "accessList": [],
    "chainId": "0x1",
    "v": "0x0",
    "r": "0xbe80603b27d91a8d311cc0ab02b549b378f497f71068d84abab2a81c43a3a586",
    "s": "0xb0d6771b3a0d3ba57f68b061f9841a9102a8bd8d9b62da4799b98cad0ce30",
    "yParity": "0x0"
  }
}
```
