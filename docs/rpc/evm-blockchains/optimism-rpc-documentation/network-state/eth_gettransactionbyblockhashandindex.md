# eth\_getTransactionByBlockHashAndIndex

### How to use it

{% tabs %}
{% tab title="TypeScript/JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Optimism, Network } from '@tatumio/tatum'
  
const tatum = await TatumSDK.init<Optimism>({network: Network.OPTIMISM})

const tx = await tatum.rpc.getTransactionByBlockHashAndIndex('0x00ccb8a97e104e09ebec66f9c58aca7d42df4fbb7cfcf1a9ff4cb7fc08814cd6', 0)

await tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Overview

`eth_getTransactionByBlockHashAndIndex` is an Optimism JSON-RPC method that allows you to fetch the transaction details based on the block hash and the index of the transaction within that block. This method can be useful when you want to retrieve transaction details for a specific transaction without knowing its transaction hash.

Use cases for this method may include:

* Inspecting transaction details for debugging purposes
* Gathering data for transaction analysis
* Fetching transaction information for specific blocks in a block explorer application

### Parameters

The `eth_getTransactionByBlockHashAndIndex` method accepts two parameters:

1. `blockHash` (required): The hash of the block containing the transaction.
   * Example: `"0x9a9a2a0d69b4ff48f7a2a8a26d135e1dbcbd3c3be3e8a3c90de0bcb104e4c4b4"`
2. `transactionIndex` (required): The index of the transaction within the specified block. The index is a hexadecimal value.
   * Example: `"0x0"`

### Return Object

The method returns a JSON object containing the following fields:

1. `hash`: The transaction hash as a 32-byte hex string.
2. `nonce`: The number of transactions made by the sender prior to this one.
3. `blockHash`: The hash of the block in which this transaction is included.
4. `blockNumber`: The block number in which this transaction is included.
5. `transactionIndex`: The index of the transaction within the block.
6. `from`: The address of the sender.
7. `to`: The address of the recipient. `null` if the transaction is a contract creation transaction.
8. `value`: The value transferred in wei.
9. `gasPrice`: The gas price provided by the sender in wei.
10. `gas`: The gas limit provided by the sender.
11. `input`: The data sent along with the transaction.

### JSON Examples

Request:

```json
{
    "jsonrpc": "2.0",
    "id": 1,
    "method": "eth_getTransactionByBlockHashAndIndex",
    "params": [
        "0x1091a5831b3556e80e53598c24e9d592e104dba0428f47f94c61523eb52d09d8",
        "0x0"
    ]
}
```

Response:

```json
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": {
        "blockHash": "0x1091a5831b3556e80e53598c24e9d592e104dba0428f47f94c61523eb52d09d8",
        "blockNumber": "0x316624",
        "from": "0x37a53636ee68f59d9346aabcfc0d36011d9d5b35",
        "gas": "0x5b8d80",
        "gasPrice": "0x59682f0a",
        "maxFeePerGas": "0x59682f10",
        "maxPriorityFeePerGas": "0x59682f00",
        "hash": "0x40a0f78e346d15b05efa1861149e5999ea48197dcf104d69160d45b08b7a5118",
        "input": "0xb1dc65a4000129d4314ec8c4bafb6468cc9d3c21de025fa54002558c9f76aec833406ab600000000000000000000000000000000000000000000000000000000001ccc01f18333a24416e0a0be9cdb78505c9c3c27fa42bccdbe6456cd6c1fc81bee7c0e00000000000000000000000000000000000000000000000000000000000000e0000000000000000000000000000000000000000000000000000000000000022000000000000000000000000000000000000000000000000000000000000003a001000000010100010100010000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000120000000000000000000000000000000000000000000000000000000000000002000000000000000000000000000000000000000000000000000000000000000800000000000000000000000000000000000000000000000000000000000003d150000000000000000000000000000000000000000000000000000000000003d17325325668a08b50a9587fd4605ce02dbc5ccefc4883a41b485ff4dc4a4f86f1e0000000000000000000000000000000000000000000000000000000000000060000000000000000000000000000000000000000000000000000000000000a8690000000000000000000000000000000000000000000000000000009d29229e000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000ba6547e7b549a1f180c5ad4f2e2e7104fecb8373482f3de6574ecbeefdc9be9dfd9f1934768a23584f1508adad8a7bbfbe445a27bed9f1d4538d4e4c9e458b0c5274b6f714f5aee9a8d56aeb8957b6da6b8914e445a46dcd349737b2eb7d72132e41926d07355de577b13e6ec8e55eaaf628b333197a8d1292bed1c375e891e1da1d519aabbebcc6d299b575b7bef506e2db9493de6f0cfdb0436a81597eb155edc63a8ea655a9b405a0c41c923b1734d78b5d9812f36a602ace3d8c5b22beb9519e406f32de9768e518f2b253a95364a9a2838ba5023c52d503fe8fa811c8803399679a19513671b13d4040e46be74e152d39be4f68bfecaa57d27965ba724a09464734faf7230b19e04f4aa581f10066884e2f402af36f0cdbf08de95e190f4f31fd3b718c1317b65fba9e7ea45ef6180e4861839c6395c814214ee8d56b28ba19f47b6b80f43045635432971b30f2bfb3a26a53ca502bf21fa598c5ddb934b000000000000000000000000000000000000000000000000000000000000000b3ab737e679aefe131ad3efc850fd2c50b316aabcdaa4368587d9606df84b3590541698c7c5538111187964e1b3f39fa033033bb7cab30275ea11b912089663ec43243ff37fa9d2cce04dfce25738c3a484d42f8d8a2c6be226627606f75788ee0e777481b5bd100d00d118bddd18e8726f7a54333b6228f57fa3237799079eb56e6e0ac0cb0f334d23f7284e2dcb2f463d8104fc198389e42a9d1bad1dcfe983115d3d85474db611a6e82b2f61b8d93efa77bc039bd5b3b0f02a7fc587d4a12a0daf256c21ecb9664e6c90c2bfb72a753ff008d3306f7cd4c823df6685fc4cba1514ed132d6367a8f99fba241fc6ef6917f5279ebfdd3e05a296e5c4d77a5463037d7c8180d0644d7e90123918c30fca011d710201ceabcae277924f32ff6b9d0e4d285eb59b4b56d3af8d4b2ab1a39ec2d4324e49deea661cbd43f21cbdc76a10a14055ecdd3251a5860c3bb02bcc1f21da5564fc05adbac70c7565fb5f44b8",
        "nonce": "0xec0",
        "to": "0x8febc74c26129c8d7e60288c6dccc75eb494aa3c",
        "transactionIndex": "0x0",
        "value": "0x0",
        "type": "0x2",
        "accessList": [],
        "chainId": "0xaa36a7",
        "v": "0x1",
        "r": "0xccf7b8fd2d63782e651f4d9650c0ed1a430060fd947d97b6504876f8ea16b357",
        "s": "0x50c56d90105b1b8aa475c9500137e9b7c4f0a331fee076bc395a695dc471dc05"
    }
}
```
