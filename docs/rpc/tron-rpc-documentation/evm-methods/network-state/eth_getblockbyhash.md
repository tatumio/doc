# eth\_getBlockByHash

### How to use it

{% tabs %}
{% tab title="TypeScript/JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Tron, Network } from '@tatumio/tatum'

// Initialize the SDK for the TRON network
const tatum = await TatumSDK.init<Tron>({network: Network.TRON})

const block = await tatum.rpc.getBlockByHash('0x48dfcf43404dffdb3b93a0b0d9982b642b221187bc3ed5c023bdab6c0e863e3d', true)

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Overview

`eth_getBlockByHash` is an JSON-RPC method that allows developers to query a specific block in the blockchain by its block hash. This method can be used in various scenarios, such as analyzing historical transactions, validating the state of the blockchain, or monitoring the progress of mining activities.

### Parameters

The `eth_getBlockByHash` method accepts two parameters:

1. **`blockHash`**: The hash of the block you want to retrieve information about.
   * Type: `String`
   * Example: `"0x078610ca461480e4b78557f20e544084cccc4accb41f5c1b7ef792246b78c94b"`
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
  "params": ["0x078610ca461480e4b78557f20e544084cccc4accb41f5c1b7ef792246b78c94b", true],
  "id": 1
}
```

#### Response

```json
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": {
        "difficulty": "0x2",
        "extraData": "0xd883010114846765746888676f312e31392e36856c696e75780000008279af9a2f9343c00920c795a7abe84303ee56588946383a15d1e9ee422a7df6dcbe199e4ec93511fe1ffa3c3ab10cb5b12459e8f64553ad3a741e9562e1d5e522c336a400",
        "gasLimit": "0x2faed85",
        "gasUsed": "0xd81f1",
        "hash": "0x078610ca461480e4b78557f20e544084cccc4accb41f5c1b7ef792246b78c94b",
        "logsBloom": "0x0020001000000000000001000000000000000000000000040000000000084000000004000800000000c06100800000000000000000010000200000000024008000004000000000000000001800001000a050000000040004000000000000000000000220020200000000000000400800080008000000000000001010004000400000000000010000000000000000000000002400000008000000008000000021022000000000000000000000000000000000000000000000000000000000010010180003000800000000000000000000000000800000000020000082000060000010000000001002010800000000000000020000080000800000000000000000",
        "miner": "0x35552c16704d214347f29fa77f77da6d75d7c752",
        "mixHash": "0x0000000000000000000000000000000000000000000000000000000000000000",
        "nonce": "0x0000000000000000",
        "number": "0x1b5dd23",
        "parentHash": "0x41f85649fa6d5e58a4631f76724a96dba8313302323f0834b9cf2b63d0308e0f",
        "receiptsRoot": "0x81835f75c1f7521016ce3404f19a44f10c4d56b6ab780fad3388d490c154afbe",
        "sha3Uncles": "0x1dcc4de8dec75d7aab85b567b6ccd41ad312451b948a7413f0a142fd40d49347",
        "size": "0x8e9",
        "stateRoot": "0xda34eefae13e5940f564f3f6cc63c96fb9a0ee015b66552f01a14c2b002b0f7f",
        "timestamp": "0x642ea5d2",
        "totalDifficulty": "0x36908d2",
        "transactions": [
            {
                "blockHash": "0x078610ca461480e4b78557f20e544084cccc4accb41f5c1b7ef792246b78c94b",
                "blockNumber": "0x1b5dd23",
                "from": "0xaa25aa7a19f9c426e07dee59b12f944f4d9f1dd3",
                "gas": "0x5208",
                "gasPrice": "0x430e23400",
                "hash": "0x82544cc4cf767ec9d235f2afa72af2cf468b25c682c302b76390cf0830006174",
                "input": "0x",
                "nonce": "0x87bf4f",
                "to": "0x2fc9076c0ebfa453dee1649721010764cbdf18fc",
                "transactionIndex": "0x0",
                "value": "0x16345785d8a0000",
                "type": "0x0",
                "v": "0xe5",
                "r": "0x282c0953168acda79a7ec86be5392370bbce08441aa803be0576dfa467a46329",
                "s": "0x59e528253c8fe85e72c43d84dd13d6fe724899cf3f94c4800761f2414b2b8f1e"
            }
        ],
        "transactionsRoot": "0xc6939e1f42fa4c4a264a1c1617cc0a6ac7122f3cb5c2848e53b3fba35b33f6ad",
        "uncles": []
    }
}
```
