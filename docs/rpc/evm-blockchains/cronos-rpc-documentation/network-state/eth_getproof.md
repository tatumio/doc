# eth\_getProof

### How to use it

{% tabs %}
{% tab title="TypeScript/JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Cronos, Network } from '@tatumio/tatum'
  
const tatum = await TatumSDK.init<Cronos>({network: Network.CRONOS})

const result = await tatum.rpc.getProof("0x523D6F30C4aaca133DAAD97eE2A0C48235bfF137",
    ["0x0000000000000000000000000000000000000000000000000000000000000000"],
    "latest")
    
await tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Overview

The `eth_getProof` is an JSON-RPC method that retrieves the Merkle-Patricia proof for an account, storage key-value pairs, and account transaction count. It allows developers to verify the state of an account or storage value at a specific block without needing the entire state trie. This method is particularly useful for light clients or off-chain applications that require proof of an account's state or specific storage values.

### Parameters

1. **`address`** - `Data`, 20 Bytes
   * The address of the account.
   * Example: `"0x523D6F30C4aaca133DAAD97eE2A0C48235bfF137"`
2. **`keys`** - `Array` of `Data`
   * An array of storage keys for which the proof should be generated.
   * Example: `["0x0000000000000000000000000000000000000000000000000000000000000000"]`
3. **`blockNumber`** - `Quantity` or `String`
   * The block number for which the proof should be generated.
   * Example: `"0x1"` or `"latest"`

### Return Object

The method returns an object containing the following fields:

1. **`accountProof`** - `Array` of `Data`
   * The serialized Merkle-Patricia proof for the account.
2. **`balance`** - `Quantity`
   * The balance of the account at the specified block.
3. **`codeHash`** - `Data`, 32 Bytes
   * The hash of the code for the account at the specified block.
4. **`nonce`** - `Quantity`
   * The transaction count of the account at the specified block.
5. **`storageProof`** - `Array` of `Object`
   * An array of storage proof objects, one for each requested key, containing the following fields:
     * `key` - `Data`, 32 Bytes: The storage key.
     * `value` - `Quantity`: The storage value.
     * `proof` - `Array` of `Data`: The serialized Merkle-Patricia proof for the key-value pair.