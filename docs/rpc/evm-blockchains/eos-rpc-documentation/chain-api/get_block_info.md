# get_block_info

### How to use it

{% tabs %}
{% tab title="TypeScript/JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Eos, Network} from '@tatumio/tatum'
  
const tatum = await TatumSDK.init<Eos>({network: Network.EOS})

const blockInfo = await tatum.rpc.getBlockInfo()

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Overview

The `get_block_info` method retrieves crucial information about a specific block in the EOS blockchain. It returns an object containing details such as block time, block number, previous block ID, producer, and transaction count. Similar to `get_block` but returns a fixed-size smaller subset of the block data.

### Example use cases:

1. **Fetching Specific Block Details:**
   Developers and users may utilize the `get_block_info` method to gather information about a particular block, aiding in debugging or validating blockchain states and transactions.

2. **Block Verification:**
   Validators and network participants can employ this method to verify the integrity and authenticity of a block, ensuring the security and reliability of the network.

3. **Data Analysis and Chain Exploration:**
   Blockchain analysts and enthusiasts might use `get_block_info` to study block patterns and transaction activities, gaining insights into the network’s operations and behaviors.

### Request Parameters

The `get_block_info` method usually has one parameter:
* `block_num_or_id` in body. It could be either a block number or a block ID.

### Return Object

The `get_block_info` method typically returns an object containing these parameters:
* `block_num` - The block number (Integer).
* `ref_block_num` - The reference block number (Integer).
* `id` - The ID of the block (String).
* `timestamp` - The timestamp when the block was produced (String).
* `producer` - The name of the block producer (String).
* `confirmed` - The number of confirmed transactions in the block (Integer).
* `previous` - The ID of the previous block (String).
* `transaction_mroot` - The Merkle root of the transactions in the block (String).
* `action_mroot` - The Merkle root of the actions in the block (String).
* `schedule_version` - The schedule version (Integer).
* `producer_signature` - The signature of the block producer (String).
* `ref_block_prefix` - The reference block prefix (Integer).

### JSON-RPC Request Example

```json
{
  "block_num_or_id": "260742168"
}
```
### JSON-RPC Response Example

```json
{
    "block_num": 260742168,
    "ref_block_num": 39960,
    "id": "0f8a9c180c996f9a88e463ca22428b3ed13c7ddc5ad09fc9c77c3c635ef9872b",
    "timestamp": "2022-08-03T16:00:36.000",
    "producer": "eosasia11111",
    "confirmed": 240,
    "previous": "0f8a9c1787cb055ab97b9beae18b762d6c3b4cfebf25060ddcc47213a2ef64d2",
    "transaction_mroot": "03313763ba0a854edbd46517bc515d090ff8e64c842e19ab91fb61f6f7bb0ce8",
    "action_mroot": "7c91b3be9fab14fe589a99312c6366d4077f49a80fd1f0ad4077f7575bbb4fe8",
    "schedule_version": 2023,
    "producer_signature": "SIG_K1_KkDoLCNaRyV62pxoUW8XQDgbZ31TrvSEDVebKFrL6fU8EsVkEFL7Wx8YMXyx2ydqY9KhPSYKQZD6dtD2cnbBmsETsZsdxt",
    "ref_block_prefix": 3395544200
}
```