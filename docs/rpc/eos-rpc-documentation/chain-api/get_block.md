# get_block

{% hint style="warning" %}
Please note that you are able to get data only from block number 260742168 and newer.
{% endhint %}

### Overview

The `get_block` method returns an object containing various details about a specific block on the blockchain, providing block number or block id in request.

{% tabs %}
{% tab title="TypeScript/JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Eos, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Eos>({ network: Network.EOS })

const block = await tatum.rpc.getBlock({ blockNumOrId: '260742168' })

await tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Example use cases:

1. **Block Verification:**
Developers or validators might use the `get_block` method to fetch specific block details for the purpose of verifying block information. It allows the comparison of block data retrieved from different nodes to ensure data consistency and integrity across the network.

2. **Transaction Confirmation:**
Users and services might utilize the `get_block` method to confirm transaction inclusion within a block. By examining the transactions field of the returned block object, users can ascertain whether a specific transaction has been included and, consequently, confirm its successful execution.

3. **Data Analysis and Chain Exploration:**
Researchers and analysts can employ the `get_block` method to retrieve detailed block data for analytical purposes, exploring block and transaction patterns, studying network activity, and gaining insights into blockchain operations and behavior.

### Request Parameters

The `getBlock` method requires the following parameter in the request body:

- `blockNumOrId` (string, required): Provide either a block number or a block ID.

### Return Object

The `get_block` method returns an object containing the following parameters:

- `timestamp` (string): Date/time string in the format YYYY-MM-DDTHH:MM:SS.sss.
- `producer` (string): The account name of the block producer.
- `confirmed` (integer): Number of prior blocks confirmed by this block producer in the current schedule.
- `previous` (string, Sha256): The ID of the block that immediately precedes this one.
- `transaction_mroot` (string, Sha256): The Merkle root of the transactions included in this block.
- `action_mroot` (string, Sha256): The Merkle root of the actions included in this block.
- `schedule_version` (integer): Number of times the producer schedule has changed since genesis.
- `new_producers` (nullable array of objects): Information about any new block producers that have been elected in this block.
- `header_extensions` (array of integers or strings): Any extensions to the block header.
- `new_protocol_features` (array of objects): List of new protocol features.
- `producer_signature` (string, Signature): Base58 encoded EOSIO cryptographic signature.
- `transactions` (array of objects): List of valid transaction receipts included in block.
- `block_extensions` (array of integers or strings): Any extensions to this block.
- `id` (string, Sha256): The ID of this block.
- `block_num` (integer): The height of this block in the chain.
- `ref_block_prefix` (integer): 32-bit portion of block ID.

### JSON-RPC Request Example

```json
{
  "block_num_or_id": "260742168"
}
```

### JSON-RPC Response Example

```json
{
  "timestamp": "2023-09-26T16:50:32.500",
  "producer": "eosio",
  "confirmed": 0,
  "previous": "0000004bc2b4483cfad9a2aeb93196c8c47744cc553d5ed30b71058e9aa2e410",
  "transaction_mroot": "0000000000000000000000000000000000000000000000000000000000000000",
  "action_mroot": "0e6e36f2db9fc3f7a7d3f1a1a7fd2aef9b9b9827060bbe5a8811e0e86e7d7d3a",
  "schedule_version": 0,
  "new_producers": null,
  "header_extensions": [],
  "new_protocol_features": [],
  "producer_signature": "SIG_K1_Jyv4wSc8yr5UWwLq9m7eKzWEVJgEo9rzUq9Zt49gCQjzjxrtBQyd1ZQsZt5Ge9wXCUsMxra1mHLJyZXFqSRcR5wSEDF1",
  "transactions": [
    {
      "status": "executed",
      "cpu_usage_us": 758,
      "net_usage_words": 14,
      "trx": [ "2", "e4be63d97b553a5d7b2c9b0

d21e753b69a3c0bf4a7f9f0b2ff806c16d8a8e959" ]
    }
  ],
  "block_extensions": [],
  "id": "0000004cc2b4483cfad9a2aeb93196c8c47744cc553d5ed30b71058e9aa2e410",
  "block_num": 76,
  "ref_block_prefix": 3708016389
}
```