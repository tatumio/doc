# getblockbylimitnext

### How to use it

{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum
import { TatumSDK, Tron, Network } from '@tatumio/tatum';

const tatum = await TatumSDK.init<Tron>({network: Network.TRON});

const res = await tatum.rpc.getBlockByLimitNext(1, 5);

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}

### Overview

The `getBlockByLimitNext` method allows interaction with the TRON blockchain to fetch a range of blocks. The method requires the starting and ending block heights as input and returns the list of Block Objects included in the range.

Use cases include, but are not limited to, data analysis, tracking block transactions, and network monitoring.

### Parameters

The method takes two parameters:

* `startNum` (integer): The starting block height, inclusive.
* `endNum` (integer): The ending block height, exclusive.

### Return Object

* `block:` Array of blocks
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

Here's how the request looks as a CURL command:

```json
{
  "startNum": 1,
  "endNum": 5
}
```

### HTTP Response Example

This is a general representation of a response. The actual response will contain a list of blocks based on the range specified:

```json
{
  "block": [
    {
      "blockID": "0000000000000001049f911bc1069bfd2c2225bc3cd210abd02fb219751813f0",
      "block_header": {
        "raw_data": {
          "number": 1,
          "txTrieRoot": "0000000000000000000000000000000000000000000000000000000000000000",
          "witness_address": "41f16412b9a17ee9408646e2a21e16478f72ed1e95",
          "parentHash": "0000000000000000de1aa88295e1fcf982742f773e0419c5a9c134c994a9059e",
          "version": 9,
          "timestamp": 1575594015000
        },
        "witness_signature": "a3feb861edcf246bd51a447f8f91636c1d7e6868b346eb2773e24859aacceaed4aa032664c2433bce5dc58e6febe87d3a7e70841684536964670fcad05fe111601"
      }
    },
    {
      "blockID": "00000000000000028e917e1dcf24b45bf9ba16d59d77f9a1846bc4861e7045e4",
      "block_header": {
        "raw_data": {
          "number": 2,
          "txTrieRoot": "0000000000000000000000000000000000000000000000000000000000000000",
          "witness_address": "41f16412b9a17ee9408646e2a21e16478f72ed1e95",
          "parentHash": "0000000000000001049f911bc1069bfd2c2225bc3cd210abd02fb219751813f0",
          "version": 9,
          "timestamp": 1575594024000
        },
        "witness_signature": "076e8610191e5e1b010697ed40fc4a8b316010374e27add85ca117160582223559e14195c7f475020b66f6136807a96c8aaea4b8a8061a9ab50d1d19234034eb00"
      }
    },
    {
      "blockID": "0000000000000003e7025004f6a699db79bd9d5f20bc5e363344f8b01f959394",
      "block_header": {
        "raw_data": {
          "number": 3,
          "txTrieRoot": "0000000000000000000000000000000000000000000000000000000000000000",
          "witness_address": "41f16412b9a17ee9408646e2a21e16478f72ed1e95",
          "parentHash": "00000000000000028e917e1dcf24b45bf9ba16d59d77f9a1846bc4861e7045e4",
          "version": 9,
          "timestamp": 1575594027000
        },
        "witness_signature": "fa4bf8994324f816b8ad1e85ae06b93b33e24cce84255c5656415573641b01410f5e2152d328c32525b8a03ca06dc6100e26fddb2c4836e3e4357134399372a901"
      }
    },
    {
      "blockID": "00000000000000044a56ccc0ee2c6ce0f6d1aeeeca788486ea0f6ad52853749c",
      "block_header": {
        "raw_data": {
          "number": 4,
          "txTrieRoot": "0000000000000000000000000000000000000000000000000000000000000000",
          "witness_address": "41f16412b9a17ee9408646e2a21e16478f72ed1e95",
          "parentHash": "0000000000000003e7025004f6a699db79bd9d5f20bc5e363344f8b01f959394",
          "version": 9,
          "timestamp": 1575594030000
        },
        "witness_signature": "192eadd1f1ae870d0e7464a72829307e5b214e1e3be16e03f223d264acf9c2f715b4b647e836c62cb88a428752b225aa8f3c6d9c85696c8f06635091b1c1982600"
      }
    }
  ]
}
```
