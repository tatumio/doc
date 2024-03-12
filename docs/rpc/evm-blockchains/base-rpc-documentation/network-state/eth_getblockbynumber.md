# eth_getBlockByNumber

### How to use it

{% tabs %}
{% tab title="TypeScript/JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}

```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Base, Network } from "@tatumio/tatum";

const tatum = await TatumSDK.init<Base>({ network: Network.BASE });

const block = await tatum.rpc.getBlockByNumber("latest", true);

await tatum.destroy(); // Destroy Tatum SDK - needed for stopping background jobs
```

{% endcode %}
{% endtab %}
{% endtabs %}

### Overview

`eth_getBlockByNumber` is an method that allows developers to query a specific block in the blockchain by its block number. This method can be used in various scenarios, such as analyzing historical transactions, validating the state of the blockchain, or monitoring the progress of mining activities.

### Parameters

There are two required parameters for this method:

1.  **`blockNumber`** - The block number of the block to be retrieved. This can be a hexadecimal string or one of the predefined aliases: `"earliest"`, `"latest"`, or `"pending"`.

    Example: `"0x1b4"`

2.  **`returnFullTransactionObjects`** - A boolean value that determines whether the returned block contains complete transaction objects (`true`) or only transaction hashes (`false`).

    Example: `true`

### Return Object

The returned block object includes the following fields:

- **`number`** - The block number (hexadecimal string).
- **`hash`** - The block hash (32-byte string).
- **`parentHash`** - The hash of the parent block (32-byte string).
- **`nonce`** - The nonce used to generate the block (8-byte string).
- **`sha3Uncles`** - The SHA3 hash of the uncles in the block (32-byte string).
- **`logsBloom`** - The logs bloom filter of the block (256-byte string).
- **`transactionsRoot`** - The root of the transaction trie (32-byte string).
- **`stateRoot`** - The root of the state trie (32-byte string).
- **`miner`** - The address of the miner who mined the block (20-byte string).
- **`difficulty`** - The difficulty of the block (hexadecimal string).
- **`totalDifficulty`** - The total difficulty of the chain up to this block (hexadecimal string).
- **`extraData`** - Extra data included by the miner in the block (byte string).
- **`size`** - The block size in bytes (hexadecimal string).
- **`gasLimit`** - The gas limit for the block (hexadecimal string).
- **`gasUsed`** - The total gas used by all transactions in the block (hexadecimal string).
- **`timestamp`** - The block timestamp (hexadecimal string).
- **`transactions`** - An array of transaction objects or transaction hashes, depending on the `returnFullTransactionObjects` parameter.
- **`uncles`** - An array of uncle block hashes (32-byte strings).

If `returnFullTransactionObjects` is `true`, the `transactions` field contains transaction objects with the following fields:

- **`hash`** - The transaction hash (32-byte string).
- **`nonce`** - The number of transactions sent by the sender before this transaction (hexadecimal string).
- **`blockHash`** - The block hash where the transaction is included (32-byte string).
- **`blockNumber`** - The block number where the transaction is included (hexadecimal string).
- **`transactionIndex`** - The index of the transaction in the block (hexadecimal string).
- **`from`** - The sender address (20-byte string).
- **`to`** - The recipient address, or `null` for contract creation transactions (20-byte string).
- **`value`** - The value being transferred (hexadecimal string).
- **`gasPrice`** - The gas price in wei (hexadecimal string).
- **`gas`** - The gas provided for the transaction (hexadecimal string).
- **`input`** - The input data for the transaction (byte string).

#### Response

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": {
    "baseFeePerGas": "0x13c",
    "difficulty": "0x0",
    "extraData": "0x",
    "gasLimit": "0x1c9c380",
    "gasUsed": "0x13bb33",
    "hash": "0x1141fda5c9d290557d3d0079f33423e2bc4ccba9b279d23dbc0884687cf36fe5",
    "logsBloom": "0x002b00022008080000800000800000402000000100000189000400200020000000004000020000400000081003041000000100008200200080700000002800080000101800000248008240388000002008100000004808080100000480200800008000401a0000800d0000002000080000001200000004004002001800082201000000408400004000008080000200000400000100200008000000440080000002400000408000049028211020000002041000000120200008000020000001000200000200080600000400204010004080000080040002100000000200002080001008408000000000000000000080406000100000000a400000400000000401",
    "miner": "0x4200000000000000000000000000000000000011",
    "mixHash": "0xf1ae28655be7b11309bb1580f9e2a140c48e601514c78dde5732eecd4bedc59e",
    "nonce": "0x0000000000000000",
    "number": "0xb2e214",
    "parentHash": "0xe12dccfd6bbe81455aaa8449f693558b421981dd8f9217bba1cd12458274cc5d",
    "receiptsRoot": "0x9b6f653ea398a8e8e638c848f409968ce25528ae37b2b2fca7f6ccdc3006a317",
    "sha3Uncles": "0x1dcc4de8dec75d7aab85b567b6ccd41ad312451b948a7413f0a142fd40d49347",
    "size": "0x117b",
    "stateRoot": "0x429ce07c4b9260883382d3ec42595ff0773f8c01243780922e0fb8552baf3126",
    "timestamp": "0x65f0210b",
    "totalDifficulty": "0x0",
    "transactions": [
      {
        "blockHash": "0x1141fda5c9d290557d3d0079f33423e2bc4ccba9b279d23dbc0884687cf36fe5",
        "blockNumber": "0xb2e214",
        "from": "0xdeaddeaddeaddeaddeaddeaddeaddeaddead0001",
        "gas": "0xf4240",
        "gasPrice": "0x0",
        "hash": "0xa36e0435dd125093711d3ef25b1d4eb87cb39889ca8d351625cdfe7d0186b439",
        "input": "0x015d8eb90000000000000000000000000000000000000000000000000000000001284bfa0000000000000000000000000000000000000000000000000000000065f0204f0000000000000000000000000000000000000000000000000000000af1a89294093b62d94188e7e3334de292332f3839fd1190f84cefc8f8ab9c08c2f2bb3b7d00000000000000000000000000000000000000000000000000000000000000020000000000000000000000005050f69a9786f081509234f1a7f4684b5e5b76c900000000000000000000000000000000000000000000000000000000000000bc00000000000000000000000000000000000000000000000000000000000a6fe0",
        "nonce": "0xb2e213",
        "to": "0x4200000000000000000000000000000000000015",
        "transactionIndex": "0x0",
        "value": "0x0",
        "type": "0x7e",
        "v": "0x0",
        "r": "0x0",
        "s": "0x0",
        "sourceHash": "0x44ec695558fdb606f1a4e3ed50b5ed9a08974bc15ca048108a38066ac75ec874",
        "mint": "0x0",
        "depositReceiptVersion": "0x1"
      }
    ],
    "transactionsRoot": "0xb076addd937ce2fe0733b9f27a7f75111a1c69b5cbf05edca57ce1289bf6857c",
    "uncles": [],
    "withdrawals": [],
    "withdrawalsRoot": "0x56e81f171bcc55a6ff8345e692c0f86e5b48e01b996cadc001622fb5e363b421"
  }
}
```
