# eth_getProof

### How to use it

{% tabs %}
{% tab title="TypeScript/JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}

```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Base, Network } from "@tatumio/tatum";

const tatum = await TatumSDK.init<Base>({ network: Network.BASE });

const result = await tatum.rpc.getProof(
  "0x833589fcd6edb6e08f4c7c32d4f71b54bda02913",
  ["0x0000000000000000000000000000000000000000000000000000000000000000"],
  "latest"
);

await tatum.destroy(); // Destroy Tatum SDK - needed for stopping background jobs
```

{% endcode %}
{% endtab %}
{% endtabs %}

### Overview

The `eth_getProof` is an method that retrieves the Merkle-Patricia proof for an account, storage key-value pairs, and account transaction count. It allows developers to verify the state of an account or storage value at a specific block without needing the entire state trie. This method is particularly useful for light clients or off-chain applications that require proof of an account's state or specific storage values.

### Parameters

1. **`address`** - `Data`, 20 Bytes
   - The address of the account.
   - Example: `"0x833589fcd6edb6e08f4c7c32d4f71b54bda02913"`
2. **`keys`** - `Array` of `Data`
   - An array of storage keys for which the proof should be generated.
   - Example: `["0x0000000000000000000000000000000000000000000000000000000000000000"]`
3. **`blockNumber`** - `Quantity` or `String`
   - The block number for which the proof should be generated.
   - Example: `"0x1"` or `"latest"`

### Return Object

The method returns an object containing the following fields:

1. **`accountProof`** - `Array` of `Data`
   - The serialized Merkle-Patricia proof for the account.
2. **`balance`** - `Quantity`
   - The balance of the account at the specified block.
3. **`codeHash`** - `Data`, 32 Bytes
   - The hash of the code for the account at the specified block.
4. **`nonce`** - `Quantity`
   - The transaction count of the account at the specified block.
5. **`storageProof`** - `Array` of `Object`
   - An array of storage proof objects, one for each requested key, containing the following fields:
     - `key` - `Data`, 32 Bytes: The storage key.
     - `value` - `Quantity`: The storage value.
     - `proof` - `Array` of `Data`: The serialized Merkle-Patricia proof for the key-value pair.

#### Response Example

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": {
    "address": "0x1234567890123456789012345678901234567890",
    "accountProof": ["0x..."],
    "balance": "0x31e1c8c4d6299",
    "codeHash": "0xc5d2460186f7233c927e7db2dcc703c0e500b653ca82273b7bfad8045d85a470",
    "nonce": "0x0",
    "storageHash": "0x56e81f171bcc55a6ff8345e692c0f86e5b48e01b996cadc001622fb5e363b421",
    "storageProof": [
      {
        "key": "0x0000000000000000000000000000000000000000000000000000000000000000",
        "value": "0x0",
        "proof": []
      }
    ]
  }
}
```
