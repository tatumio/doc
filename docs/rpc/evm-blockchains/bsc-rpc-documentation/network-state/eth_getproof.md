# eth\_getProof

### How to use it

{% tabs %}
{% tab title="TypeScript/JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, BinanceSmartChain, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<BinanceSmartChain>({network: Network.BINANCE_SMART_CHAIN})

const result = await tatum.rpc.getProof("0xa41d19F4258a388c639B7CcD938FCE3fb7D05e86",
    ["0x0000000000000000000000000000000000000000000000000000000000000000"],
    "latest")
    
tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Overview

The `eth_getProof` is a JSON-RPC method that retrieves the Merkle-Patricia proof for an account, storage key-value pairs, and account transaction count. It allows developers to verify the state of an account or storage value at a specific block without needing the entire state trie. This method is particularly useful for light clients or off-chain applications that require proof of an account's state or specific storage values.

### Parameters

1. **`address`** - `Data`, 20 Bytes
   * The address of the account.
   * Example: `"0xa41d19F4258a388c639B7CcD938FCE3fb7D05e86"`
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

### JSON-RPC Request and Response Examples

_Request_:

```json
{
  "id": 1,
  "jsonrpc": "2.0",
  "method": "eth_getProof",
  "params": [
    "0xa41d19F4258a388c639B7CcD938FCE3fb7D05e86",
    [
      "0x0000000000000000000000000000000000000000000000000000000000000000"
    ],
    "latest"
  ]
}
```

_Response_:

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": {
    "address": "0xa41d19f4258a388c639b7ccd938fce3fb7d05e86",
    "accountProof": [],
    "balance": "0x0",
    "codeHash": "0xc5d2460186f7233c927e7db2dcc703c0e500b653ca82273b7bfad8045d85a470",
    "nonce": "0x0",
    "storageHash": "0x56e81f171bcc55a6ff8345e692c0f86e5b48e01b996cadc001622fb5e363b421",
    "storageProof": [{}]
  }
}
```
