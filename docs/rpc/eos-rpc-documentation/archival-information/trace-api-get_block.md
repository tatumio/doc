# Trace API get_block

{% hint style="warning" %}
Please note that you are able to get data only from block number 260742168 and newer.
{% endhint %}

### How to use it

{% tabs %}
{% tab title="TypeScript/JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Eos, Network} from '@tatumio/tatum'

const tatum = await TatumSDK.init<Eos>({network: Network.EOS})

const block = await tatum.rpc.traceApiGetBlock({blockNum:'260742168'})

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}
{% endtab %}
{% endtabs %}

{% hint style="info" %}
This method is available only on the full archive node.
{% endhint %}

### Overview
The `get_block` method of the Trace API retrieves detailed information concerning a specific block in the blockchain, returning a JSON object that conforms to the BlockTraceV1 schema. This method is crucial for applications and services requiring access to block and transaction details such as the list of transactions, actions within those transactions, the producer of the block, and more.

### Example use cases:

1. **Block Verification:**
Developers or validators might use the `get_block` method to fetch specific block details for the purpose of verifying block information. It allows the comparison of block data retrieved from different nodes to ensure data consistency and integrity across the network.

2. **Transaction Confirmation:**
Users and services might utilize the `get_block` method to confirm transaction inclusion within a block. By examining the transactions field of the returned block object, users can ascertain whether a specific transaction has been included and, consequently, confirm its successful execution.

3. **Data Analysis and Chain Exploration:**
Researchers and analysts can employ the `get_block` method to retrieve detailed block data for analytical purposes, exploring block and transaction patterns, studying network activity, and gaining insights into blockchain operations and behavior.

### Request Parameters

The `getBlock` method accepts the following parameters:

- `blockNum` (integer, required): The height of this block in the chain.

### Return Object

The return object provides detailed information about the requested block and contains the following fields:

- `id` (string): A unique identifier for the block.
- `number` (integer): The height of this block in the chain.
- `previous_id` (string): The unique identifier of the previous block in the chain.
- `status` (string): String indicating whether the block is "pending" or "irreversible".
- `timestamp` (string): The timestamp when the block was produced.
- `producer` (string): Information about who produced the block.
- `transaction_mroot` (string): The Merkle root of all transactions in the block.
- `action_mroot` (string): The Merkle root of all actions in the block.
- `schedule_version` (integer): Indicates the number of times the producer schedule has changed since genesis.
- `transactions` (array): An array containing TransactionTraceV1 objects representing each transaction included in the block.

### JSON-RPC Request Example

```json
{
  "block_num": "260742168"
}
```

### JSON-RPC Response Example

```json
{
  "id": "string",
  "number": 0,
  "previous_id": "string",
  "status": "string",
  "timestamp": "string",
  "producer": "string",
  "transactions": [
    {
      "id": "string",
      "actions": [
        {
          "global_sequence": 0,
          "receiver": "string",
          "account": "string",
          "action": "string",
          "authorization": [
            {
              "account": "string",
              "permission": "string"
            }
          ],
          "data": {}
        }
      ]
    }
  ]
}
```