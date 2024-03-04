# debug\_getBadBlocks

### How to use it

{% tabs %}
{% tab title="TypeScript/JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Fantom, Network } from '@tatumio/tatum'
  
const tatum = await TatumSDK.init<Fantom>({ network: Network.FANTOM })

const result = await tatum.rpc.debugGetBadBlocks()

await tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Overview

`debug_getBadBlocks` is na RPC method that provides a list of the most recent bad blocks encountered by the client on the network. This feature is valuable for developers and node operators, as it enables them to identify and address any issues or anomalies related to block validation and synchronization.

By accessing `debug_getBadBlocks`, they can diagnose potential problems and take appropriate actions to ensure the network's stability and integrity.

### Parameters

* This method does not accept any parameters.

### Return Object

The output is an array of objects, with each object representing the trace result of a transaction within the block. These objects include essential details such as the transaction hash and a block object, which can be null if no block was found for the transaction:

* `baseFeePerGas`: The integer representation of the difficulty for this block encoded as hexadecimal.
* `difficulty`: The integer representation of the difficulty for this block encoded as hexadecimal.
* `extraData`: The extra data field of this block.
* `gasLimit`: The maximum gas allowed in this block encoded as hexadecimal.
* `gasUsed`: The total used gas by all transactions in this block encoded as hexadecimal.
* `logsBloom`: The bloom filter for the logs of the block. Null if pending.
* `miner`: The address of the beneficiary to whom the mining rewards were given.
* `mixHash`: A 256-bit hash encoded as hexadecimal.
* `nonce`: The hash of the generated proof-of-work. Null if pending.
* `number`: The block number of the requested block encoded as hexadecimal. Null if pending.
* `parentHash`: The hash of the parent block.
* `receiptsRoot`: The root of the receipts trie of the block.
* `sha3Uncles`: The SHA3 of the uncles' data in the block.
* `size`: The size of this block in bytes as an Integer value encoded as hexadecimal.
* `stateRoot`: The root of the final state trie of the block.
* `timestamp`: The Unix timestamp for when the block was collated.
* `transactions`: An array of transaction objects with the following fields:
  * `blockHash`: The hash of the block where this log was in. Null when it's a pending log.
  * `blockNumber`: The block number where this log was in. Null when it's a pending log.
  * `from`: The address of the sender.
  * `gas`: The gas provided by the sender, encoded as hexadecimal.
  * `gasPrice`: The gas price provided by the sender in wei, encoded as hexadecimal.
  * `maxFeePerGas`: The maximum fee per gas set in the transaction.
  * `maxPriorityFeePerGas`: The maximum priority gas fee set in the transaction.
  * `hash`: The hash of the transaction.
  * `input`: The data sent along with the transaction.
  * `nonce`: The number of transactions made by the sender before this one encoded as hexadecimal.
  * `to`: The address of the receiver. Null when it's a contract creation transaction.
  * `transactionIndex`: The integer of the transaction's index position that the log was created from. Null when it's a pending log.
  * `value`: The value transferred in wei encoded as hexadecimal.
  * `type`: The transaction type.
  * `accessList`: A list of addresses and storage keys that the transaction plans to access.
  * `chainId`: The chain id of the transaction, if any.
  * `v`: The standardized V field of the signature.
  * `r`: The R field of the signature.
  * `s`: The S field of the signature.
* `transactionsRoot`: The root of the transaction trie of the block.
* `uncles`: An array of uncle hashes.
* `rlp`: The RLP encoded header.

{% hint style="info" %}
This method is available only on the full archive node.
{% endhint %}

### JSON-RPC Request and Response Examples

#### Request

```json
{
  "id": 1,
  "jsonrpc": "2.0",
  "method": "debug_getBadBlocks",
  "params": []
}
```

#### Response

```json
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": []
}
```
