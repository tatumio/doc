# eth\_getBlockByHash

### How to use it

{% tabs %}
{% tab title="TypeScript/JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Ethereum, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Ethereum>({network: Network.ETHEREUM})

const block = await tatum.rpc.getBlockByHash('0x75e58e08a9f3a23bac9788d5077a9365abb5c29ec1aab70891264051624720af', true)

await tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Overview

`eth_getBlockByHash` is an Ethereum JSON-RPC method that allows developers to query a specific block in the Ethereum blockchain by its block hash. This method can be used in various scenarios, such as analysing historical transactions, validating the state of the blockchain, or monitoring the progress of mining activities.

{% embed url="https://codepen.io/tatum-devrel/pen/xxQNNGq" %}

### Parameters

The `eth_getBlockByHash` method accepts two parameters:

1. **`blockHash`**: The hash of the block you want to retrieve information about.
   * Type: `String`
   * Example: `"0x75e58e08a9f3a23bac9788d5077a9365abb5c29ec1aab70891264051624720af"`
2. **`fullTransactionDetails`**: A boolean value indicating whether to return full transaction details or just transaction hashes.
   * Type: `Boolean`
   * Example: `true`

### Return Object

The returned block object includes the following fields:

* **`number`** - The block number (hexadecimal string).
* **`hash`** - The block hash (32-byte string).
* **`parentHash`** - The hash of the parent block (32-byte string).
* **`nonce`** - The nonce used to generate the block (8-byte string).
* **`sha3Uncles`** - The SHA3 hash of the uncles in the block (32-byte string).
* **`logsBloom`** - The logs bloom filter of the block (256-byte string).
* **`transactionsRoot`** - The root of the transaction trie (32-byte string).
* **`stateRoot`** - The root of the state trie (32-byte string).
* **`miner`** - The address of the miner who mined the block (20-byte string).
* **`difficulty`** - The difficulty of the block (hexadecimal string).
* **`totalDifficulty`** - The total difficulty of the chain up to this block (hexadecimal string).
* **`extraData`** - Extra data included by the miner in the block (byte string).
* **`size`** - The block size in bytes (hexadecimal string).
* **`gasLimit`** - The gas limit for the block (hexadecimal string).
* **`gasUsed`** - The total gas used by all transactions in the block (hexadecimal string).
* **`timestamp`** - The block timestamp (hexadecimal string).
* **`transactions`** - An array of transaction objects or transaction hashes, depending on the `returnFullTransactionObjects` parameter.
* **`uncles`** - An array of uncle block hashes (32-byte strings).

If `returnFullTransactionObjects` is `true`, the `transactions` field contains transaction objects with the following fields:

* **`hash`** - The transaction hash (32-byte string).
* **`nonce`** - The number of transactions sent by the sender before this transaction (hexadecimal string).
* **`blockHash`** - The block hash where the transaction is included (32-byte string).
* **`blockNumber`** - The block number where the transaction is included (hexadecimal string).
* **`transactionIndex`** - The index of the transaction in the block (hexadecimal string).
* **`from`** - The sender address (20-byte string).
* **`to`** - The recipient address, or `null` for contract creation transactions (20-byte string).
* **`value`** - The value being transferred (hexadecimal string).
* **`gasPrice`** - The gas price in wei (hexadecimal string).
* **`gas`** - The gas provided for the transaction (hexadecimal string).
* **`input`** - The input data for the transaction (byte string).

### JSON-RPC Request and Response Examples

Here are examples of JSON-RPC request and response for the `eth_getBlockByNumber` method:

#### Request

```json
{
  "jsonrpc": "2.0",
  "method": "eth_getBlockByHash",
  "params": ["0x75e58e08a9f3a23bac9788d5077a9365abb5c29ec1aab70891264051624720af", true],
  "id": 1
}
```

#### Response

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": {
    "baseFeePerGas": "0x35ddd12aa",
    "difficulty": "0x0",
    "extraData": "0xd883010c02846765746888676f312e32302e37856c696e7578",
    "gasLimit": "0x1c9c380",
    "gasUsed": "0x9426f0",
    "hash": "0x75e58e08a9f3a23bac9788d5077a9365abb5c29ec1aab70891264051624720af",
    "logsBloom": "0x2734882843000e08f2096070f803a2a854304d0062c40102d01b1002478401820020904c234830800d100600018509900b0022029b0c2e949e95c000153e008250005a18b42888380b00423a590113e611192c2c2144081308321ccdfbe004e40b805841b24a91041e0ddc1630466d0800584d1400181e2482444cd0aa6b025423218b052b405824464e88584013849102801e8109a6862d26010a64289348858a28c0078382eb808e4600a631b09660437a04354c5290822c448400020a09104d94a7e320438530080060201e3a05c431a0c4184aed32140d5d3093584d611e1991600a034148c05f0c443c2a0208086a22d1c1cb689049900ab0114010c202",
    "miner": "0xb79743c0968c49a518be9c83bed8f6f69e005c32",
    "mixHash": "0x5781d7db87a40a3301d673155ae8d2faa5a87c72dabc4a82fb944175cac5cf59",
    "nonce": "0x0000000000000000",
    "number": "0x1143497",
    "parentHash": "0x41f676300e43cc244d5427b3714a5fc7146e443504c437b1f5bc4b337a06ae2a",
    "receiptsRoot": "0xd6c87dabf0ec502567a85c32e77051d83f08b7627f4ed7d85e194eeb1d2b9b54",
    "sha3Uncles": "0x1dcc4de8dec75d7aab85b567b6ccd41ad312451b948a7413f0a142fd40d49347",
    "size": "0x3ef6a",
    "stateRoot": "0x4e6df5a0f0181b146d1ff137a7548ab3d67630011f6ea9ea084b9325dda56ff5",
    "timestamp": "0x64fcddfb",
    "totalDifficulty": "0xc70d815d562d3cfa955",
    "transactions": [
      [Object], [Object], [Object], [Object], [Object],
      [Object], [Object], [Object], [Object], [Object],
      [Object], [Object], [Object], [Object], [Object],
      [Object], [Object], [Object], [Object], [Object],
      [Object], [Object], [Object], [Object], [Object],
      [Object], [Object], [Object], [Object], [Object],
      [Object], [Object], [Object], [Object], [Object],
      [Object], [Object], [Object], [Object], [Object],
      [Object], [Object], [Object], [Object], [Object],
      [Object], [Object], [Object], [Object], [Object],
      [Object], [Object], [Object], [Object], [Object],
      [Object], [Object], [Object], [Object], [Object],
      [Object], [Object], [Object], [Object]
    ],
    "transactionsRoot": "0xbe9ed26c6b185a4b6d0b175ba694c9243eb58d06e11aff3258f5167d4ace26e7",
    "uncles": [],
    "withdrawals": [
      [Object], [Object],
      [Object], [Object],
      [Object], [Object],
      [Object], [Object],
      [Object], [Object],
      [Object], [Object],
      [Object], [Object],
      [Object], [Object]
    ],
    "withdrawalsRoot": "0x365326ed6795e450a8f437c7c30da68254567bbaf755321b2663dcc6777fddcb"
  }
}

```
