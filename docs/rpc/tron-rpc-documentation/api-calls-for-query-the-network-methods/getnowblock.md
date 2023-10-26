# getnowblock

### How to use it

{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Tron, Network } from '@tatumio/tatum';

const tatum = await TatumSDK.init<Tron>({ network: Network.TRON });

const res = await tatum.rpc.getNowBlock();

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}

### Overview

The `getNowBlock()` method is used to query the latest block information on the TRON network. It interacts with the TRON RPC to fetch the data, making it a crucial function for applications needing real-time information about the TRON blockchain. Examples of such applications include blockchain explorers, cryptocurrency wallets, or decentralised applications.

{% embed url="https://codepen.io/tatum-devrel/pen/GRwLzzK" %}

### Parameters

This method doesn't require any parameters.

### Return Object

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

```bash
{}
```

### HTTP Response Example

The HTTP response for the `getNowBlock()` function is a JSON object representing the latest block data. The exact fields can vary due to the dynamic nature of the blockchain data. Here is an example of how the HTTP response could look like:

```json
{
  "blockID": "000000000203c44fb29c8b78d653607e5b7c210a9b415c0daa1f84f00c8fa9af",
  "block_header": {
    "raw_data": {
      "number": 33801295,
      "txTrieRoot": "0000000000000000000000000000000000000000000000000000000000000000",
      "witness_address": "41977f82c69011cf4a7db6f7339edcded85c614d45",
      "parentHash": "000000000203c44e82ebe5332248e40efa68a5243458dc398628b1ce05db0d36",
      "version": 27,
      "timestamp": 1684510050000
    },
    "witness_signature": "05cd4c14889dc39a0465fc6c769fb6c39f986c90cfe0ef8cbf4be6402f7b25b613b97c4c7ee2e411b908d53658752102a7292a4965002609a50e075f171c151e01"
  }
}
```
