# eth\_getStorageAt

### How to use it

{% tabs %}
{% tab title="TypeScript/JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, HorizenEon, Network} from '@tatumio/tatum'

const tatum = await TatumSDK.init<HorizenEon>({network: Network.HORIZEN_EON})

const response = await tatum.rpc.getStorageAt('0x6eA7d015342b7eb7344F7ebf0150234f41F524d6', '0x0')

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Overview

`eth_getStorageAt` is an JSON-RPC method that allows you to query the storage value of a contract at a given position. It can be used to inspect the internal state of a smart contract. This method is particularly useful for developers, auditors, and analysts who want to examine contract storage values for various purposes, such as debugging, verifying contract behavior, or analyzing data.

### Parameters

`eth_getStorageAt` accepts three parameters:

1. **`address`**: The address of the contract you want to query.
   * Example: `"0x6eA7d015342b7eb7344F7ebf0150234f41F524d6"`
2. **`position`**: The storage position (slot) you want to query.
   * Example: `"0x0"`
3. **`blockParameter`**: The block number, block hash, or one of the string literals (`"earliest"`, `"latest"` or `"pending"`), representing the point in the blockchain to query the storage value.
   * Example: `"latest"`

### Return Object

The return object is a single string value, representing the storage value at the given position in the contract.

* `result`: The storage value in a 32-byte (64 character) hexadecimal format.

### JSON-RPC Request Example

```json
{
  "id": 1,
  "jsonrpc": "2.0",
  "method": "eth_getStorageAt",
  "params": [
    "0x6eA7d015342b7eb7344F7ebf0150234f41F524d6",
    "0x0"
  ]
}
```

### JSON-RPC Response Example

```json
{
  "id": 1,
  "jsonrpc": "2.0",
  "result": "0x0000000000000000000000000000000000000000000000000000000000000001"
}
```

\
