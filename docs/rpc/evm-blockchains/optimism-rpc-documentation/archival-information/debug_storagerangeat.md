# debug\_storageRangeAt

### How to use it

{% tabs %}
{% tab title="TypeScript/JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Optimism, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Optimism>({network: Network.OPTIMISM})

const result = await tatum.rpc.debugStorageRangeAt(
'0x00ccb8a97e104e09ebec66f9c58aca7d42df4fbb7cfcf1a9ff4cb7fc08814cd6',
1, '0x365a2dabcdb56f4f595c3af088b8975c26331448', '0x0000000000000000000000000000000000000000000000000000000000000000', 1
)

await tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Overview

`debug_storageRangeAt` is an RPC method that allows you to retrieve the contract storage range for a given block and address. This can be useful for developers and auditors who want to inspect the storage state of a specific contract at a particular point in time. This method can also help in debugging and identifying potential issues with contract storage, as well as understanding how storage evolves as transactions are executed.

### Parameters

The `debug_storageRangeAt` method accepts the following parameters:

* `blockHash`: The block hash for which the storage range should be retrieved. Example: `"0x3c4523b7e8c21e3d68f1c3af3d18e8a87c0d43e35b2c1b7f8f4e87e4d4db9c82"`
* `txIndex`: The transaction index within the specified block. Example: `1`
* `address`: The contract address for which the storage range should be retrieved. Example: `"0x742d35Cc6634C0532925a3b844Bc454e4438f44e"`
* `begin`: The beginning of the storage range. Example: `"0x0000000000000000000000000000000000000000000000000000000000000000"`
* `end`: The end of the storage range. Example: `1` (inclusive)

### Return Object

The `debug_storageRangeAt` method returns an object with the following fields:

* `storage`: An object that contains key-value pairs representing the contract storage, where the key is the storage slot and the value is the stored data. Example: `"0x00..01": "0x00..01"`
* `nextKey`: A key indicating the next storage slot if the requested range is too large, otherwise `null`. Example: `"0x00..02"` or `null`

{% hint style="info" %}
This method is available only on the full archive node.
{% endhint %}

### JSON-RPC Request and Response Examples

#### Request

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "debug_storageRangeAt",
  "params": [
    "0x3c4523b7e8c21e3d68f1c3af3d18e8a87c0d43e35b2c1b7f8f4e87e4d4db9c82",
    "0x1",
    "0x742d35Cc6634C0532925a3b844Bc454e4438f44e",
    "0x0000000000000000000000000000000000000000000000000000000000000000", 1
  ]
}
```

#### Response

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": {
    "storage": {
      "0x0000000000000000000000000000000000000000000000000000000000000001": "0x0000000000000000000000000000000000000000000000000000000000000001",
      "0x0000000000000000000000000000000000000000000000000000000000000002": "0x0000000000000000000000000000000000000000000000000000000000000002"
    },
    "nextKey": "0x0000000000000000000000000000000000000000000000000000000000000065"
  }
}
```
