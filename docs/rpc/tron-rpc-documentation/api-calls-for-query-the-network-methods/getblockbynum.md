# getblockbynum

### How to Use It

{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Tron, Network } from '@tatumio/tatum'

// Initialize Tatum SDK for TRON network
const tatum = await TatumSDK.init<Tron>({network: Network.TRON})

// Get the block by number
const block = await tatum.rpc.getBlockByNum(200)

await tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}

### Overview

The `getBlockByNum` method returns the block object corresponding to the block height specified (the number of blocks preceding it). This could be useful for retrieving specific block data or for validating transactions within a certain block.

{% embed url="https://codepen.io/tatum-devrel/pen/GRwLzPK" %}

### Parameters

* `num` (integer): The height of the block to retrieve.

### Return Object

The method returns a promise that resolves to a block object with the following fields:

*
* `blockID` (string): The block hash.
* `block_header` (object)
  * `raw_data` (object)
    * `timestamp` (integer): The timestamp of the block.
    * `txTrieRoot` (string): The root of the transaction merkle tree.
    * `parentHash` (string): The parent block hash.
    * `number` (integer): The block number.
    * `witness_id` (integer): The witness id.
    * `witness_address` (string): The witness address.
    * `version` (integer): The version.
    * `accountStateRoot` (string): The root of the account state tree.
  * `witness_signature` (string): The signature of the Super Representative (SR).
* `transactions` (Array): Contains transaction information in the block.
  * `raw_data.contract` - The main content of the transaction, contract is a list, but only one element is used at present. Different types of transactions have different contract contents. For example, for a TRX transfer type transaction, the contract will include the transfer amount, receiver address and other information. TRON supports multiple types of contracts, please refer to the official documentation [Types of Transaction](https://developers.tron.network/docs/tron-protocol-transaction#types-of-transaction).
  * `raw_data.ref_block_bytes` - The height of the transaction reference block, using the 6th to 8th (exclusive) bytes of the reference block height, a total of 2 bytes. The reference block is used in the TRON TAPOS mechanism, which can prevent a replay of a transaction on forks that do not include the referenced block. Generally, the latest solidified block is used as the reference block.
  * `raw_data.ref_block_hash` - The hash of the transaction reference block, using the 8th to 16th (exclusive) bytes of the reference block hash, a total of 8 bytes. The reference block is used in the TRON TAPOS mechanism, which can prevent a replay of a transaction on forks that do not include the referenced block. Generally, the latest solidified block is used as the reference block.
  * `raw_data.expiration` - Transaction expiration time, beyond which the transaction will no longer be packed. If the transaction is created by calling the java-tron API, its expiration time will be automatically set by the node to the value of adding 60 seconds to the timestamp of the node's latest block. The expiration time interval can be modified in the node's configuration file, the maximum value cannot exceed 24 hours.
  * `raw_data.data` - Transaction memo.
  * `raw_data.timestamp` - Transaction timestamp, set as the transaction creation time.
  * `raw_data.fee_limit` - The maximum energy cost allowed for the execution of smart contract transactions. Only deploying and triggering smart contract transactions need to be set, others not.
  * `signature` - The sender's signature for the transaction. This proves that the transaction could only have come from the sender and was not sent fraudulently.
  * `txID` - transaction id

### HTTP Request Example

```json
{
    "num":200
}
```

### HTTP Response Example

```json
{
  "blockID": "00000000000000c86d2473411771f83db5e314c01bc8f8cf0dc2f8892be6fd7f",
  "block_header": {
    "raw_data": {
      "number": 200,
      "txTrieRoot": "0000000000000000000000000000000000000000000000000000000000000000",
      "witness_address": "41f16412b9a17ee9408646e2a21e16478f72ed1e95",
      "parentHash": "00000000000000c7d4d47132f21fd0b74e2f8bcb0c2e9130f7cab35b5d38af9f",
      "version": 9,
      "timestamp": 1575594618000
    },
    "witness_signature": "97ecda5b130600d18304e02f7fd5ab9d115c5ec9c0e312c8c6fe83939771bb85505fafee598541dc902b1a7b8ca2735c83a12e640203ed4b8529d47ce4f413df00"
  }
}
```

***
