# get_info

### How to use it

{% tabs %}
{% tab title="TypeScript/JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, EOS, Network} from '@tatumio/tatum'
  
const tatum = await TatumSDK.init<EOS>({network: Network.EOS})

const account = await tatum.rpc.getInfo('b1')

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Overview

The `get_info` RPC method in the EOS blockchain is used to retrieve various details about the blockchain's state, such as the head block, the last irreversible block, and the chain ID. It is one of the most fundamental RPC calls in the EOSIO blockchain, providing essential information about the network's status.

Example use cases:

**Checking Blockchain Status:**
Developers and users often use the get_info method to quickly check the status of the EOS blockchain, such as the head block number and the last irreversible block number, to ensure they are interacting with the most recent and confirmed state of the blockchain.

**Synchronization and Validation:**
For node operators and block producers, get_info is crucial to verify that their node is synchronized with the network, and to compare the chain_id and other details to ensure they are on the correct chain and avoid forks.

**Development and Debugging:**
Developers frequently use get_info during the development and debugging of dApps and smart contracts, to fetch real-time information about the blockchain, validate transactions, and test the behavior of their applications against the current state of the blockchain.

### Parameters

`get_info` does not require any request parameters

### Return Object



### JSON-RPC Request Example

```json

```

### JSON-RPC Response Example

```json

```