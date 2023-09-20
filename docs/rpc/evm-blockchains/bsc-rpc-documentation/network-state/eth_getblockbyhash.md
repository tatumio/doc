# eth\_getBlockByHash

### How to use it

{% tabs %}
{% tab title="TypeScript/JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, BinanceSmartChain, Network} from '@tatumio/tatum'

const tatum = await TatumSDK.init<BinanceSmartChain>({network: Network.BINANCE_SMART_CHAIN})

const block = await tatum.rpc.getBlockByHash('0xf6ab52aebd492d20f7d5aef604d3d35111ec3d0ea4387431222429828652c9a1', true)

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
   * Example: `"0xf6ab52aebd492d20f7d5aef604d3d35111ec3d0ea4387431222429828652c9a1"`
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
  "params": ["0xf6ab52aebd492d20f7d5aef604d3d35111ec3d0ea4387431222429828652c9a1", true],
  "id": 1
}
```

#### Response

```json
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": {
        "baseFeePerGas": "0x0",
        "difficulty": "0x2",
        "extraData": "0xd88301020b846765746888676f312e32302e34856c696e7578000000b19df4a2f8b5830d77ffb86082b4f5f252d14a0114894d1a27ffd744abf6ad2b17ca03aee899d30472cd252fa552a55980b1ad815d100d9a0477068407cdac3e6bdf640a2f4ee08441719d7af44a6851f52b751e97a63f73bbda4b5193e065750c33ff685751e60546be875cf84c8401e3babba01c37c7cbb5104d70b946cb41fa58a4d9233ab8fbb5eb3157e4f47e660a418d098401e3babca0dada7f63e1e688bb4c038c65b59ae516095b530eb0aafa6670b25d79826e77fe80faf5f05a0b8058404f73d37dc8817e4756ce0fc98867164735f94604f43bdb3138fd9441d75eff0276f07ca4ae85aeb112e3cfac9b2a432d0e73e08622ff3d2200",
        "gasLimit": "0x84fe2c6",
        "gasUsed": "0xa41073",
        "hash": "0xf6ab52aebd492d20f7d5aef604d3d35111ec3d0ea4387431222429828652c9a1",
        "logsBloom": "0x34a61a1c00021592286002548f5e940711b04513241c06a91dea45c892210331814498885820b1614e122a82c472000198c3ce0c23027368b67a74209aa03a2bc4566012215e488c25445149a23d022d607290c5a96438ea00540085c62d460d4f0e00e02b22082420c5193a9518189d08523e4bd3686c1662125a11585805b6c00d4864221b10dc078946a41dc50f18402d9685782202a82d2de9c888ead0b202e8121e7b64aa11684834cd0f944620c5a90d2401868404116059253312526c98231546d1090856b060080f09bf52eca0d50dc3f8bbf074213140cb1621e6fc1971e9375b0083e0c38516d495a6ad04ad51840c023e8548732499d4a2ed25d2",
        "miner": "0x9f8ccdafcc39f3c7d6ebf637c9151673cbc36b88",
        "mixHash": "0x0000000000000000000000000000000000000000000000000000000000000000",
        "nonce": "0x0000000000000000",
        "number": "0x1e3babd",
        "parentHash": "0xdada7f63e1e688bb4c038c65b59ae516095b530eb0aafa6670b25d79826e77fe",
        "receiptsRoot": "0xcf29bb7fc17c26f39b86c02b4b08f5b11763e3cc19497b58ef18049978b0c7cc",
        "sha3Uncles": "0x1dcc4de8dec75d7aab85b567b6ccd41ad312451b948a7413f0a142fd40d49347",
        "size": "0x65cb",
        "stateRoot": "0x89063043aaf47c7ff87de3e197d3e556c7752fb2e338ec2ab4626d0b60f0f2d8",
        "timestamp": "0x65017610",
        "totalDifficulty": "0x3c12b38",
        "transactions": [],
        "transactionsRoot": "0x28caed6a0174dc936da148dcf519eb66ab912c4a94eacc123a05ca66d03c224b",
        "uncles": []
    }
}
```
