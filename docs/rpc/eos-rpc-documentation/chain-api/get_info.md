# get_info

### Overview

The `get_info` RPC method in the EOS blockchain is used to retrieve various details about the blockchain's state, such as the head block, the last irreversible block, and the chain ID. It is one of the most fundamental RPC calls in the EOSIO blockchain, providing essential information about the network's status.
{% tabs %}
{% tab title="TypeScript/JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Eos, Network } from '@tatumio/tatum'
  
const tatum = await TatumSDK.init<Eos>({ network: Network.EOS })

const info = await tatum.rpc.getInfo()

await tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Example use cases:

1. **Checking Blockchain Status:**
Developers and users often use the `get_info` method to quickly check the status of the EOS blockchain, such as the head block number and the last irreversible block number, to ensure they are interacting with the most recent and confirmed state of the blockchain.

2. **Synchronization and Validation:**
For node operators and block producers, `get_info` is crucial to verify that their node is synchronized with the network, and to compare the `chain_id` and other details to ensure they are on the correct chain and avoid forks.

3. **Development and Debugging:**
Developers frequently use `get_info` during the development and debugging of dApps and smart contracts, to fetch real-time information about the blockchain, validate transactions, and test the behavior of their applications against the current state of the blockchain.

### Request Parameters
The `getInfo` method does not require any parameters; it is a simple GET request to the endpoint.

### Return Object
The `get_info` method returns an object with the following response parameters:

- `server_version` (string): The version of the nodeos software running on the node.
- `chain_id` (string): The unique identifier for the EOSIO blockchain.
- `head_block_num` (integer): The most recent block number on the blockchain.
- `head_block_id` (string): The unique identifier of the head block.
- `head_block_time` (string): The timestamp of when the head block was produced.
- `head_block_producer` (string): The name of the block producer that produced the head block.
- `last_irreversible_block_num` (integer): The most recent block that has been irreversibly confirmed on the blockchain.
- `last_irreversible_block_id` (string): The unique identifier of the last irreversible block.
- `virtual_block_cpu_limit` (integer): The current limit on CPU usage for virtual blocks.
- `virtual_block_net_limit` (integer): The current limit on NET usage for virtual blocks.
- `block_cpu_limit` (integer): The current limit on CPU usage for blocks.
- `block_net_limit` (integer): The current limit on NET usage for blocks.
- `server_version_string` (string): The server version as a string.
- `fork_db_head_block_num` (integer): Sequential block number representing the best known head in the fork database tree.
- `fork_db_head_block_id` (string): Hash representing the best known head in the fork database tree.

### JSON-RPC Response Example

```json
{
    "server_version": "7e1ad13e",
    "chain_id": "aca376f206b8fc25a6ed44dbdc66547c36c6c33e3a119ffbeaef943642f0e906",
    "head_block_num": 333261268,
    "last_irreversible_block_num": 333260936,
    "last_irreversible_block_id": "13dd2888c6e933ac455978baf53554605d95e0e2d2abd0c1159ddb218936fe03",
    "head_block_id": "13dd29d4aa69b67d138d0bbb82ee4d1de74ec0cd404d58902381ea9d5bdbff67",
    "head_block_time": "2023-09-27T12:51:57.500",
    "head_block_producer": "eoseouldotio",
    "virtual_block_cpu_limit": 200000,
    "virtual_block_net_limit": 1048576000,
    "block_cpu_limit": 200000,
    "block_net_limit": 1048576,
    "server_version_string": "v4.0.4",
    "fork_db_head_block_num": 333261268,
    "fork_db_head_block_id": "13dd29d4aa69b67d138d0bbb82ee4d1de74ec0cd404d58902381ea9d5bdbff67",
    "server_full_version_string": "v4.0.4-7e1ad13e1e98b1e0703d0ea072b4fca5419cfdbe",
    "total_cpu_weight": "383377176232761",
    "total_net_weight": "96156545705220",
    "earliest_available_block_num": 260742168,
    "last_irreversible_block_time": "2023-09-27T12:49:11.500"
}
```