# push_transactions

### Overview

The `push_transactions` method is designed to submit multiple transactions to the EOS blockchain simultaneously. This method expects an array of transactions in JSON format and attempts to apply them to the blockchain, enabling a range of blockchain interactions like transferring tokens, invoking smart contracts, and more.

{% tabs %}
{% tab title="TypeScript/JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, EOS, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<EOS>({ network: Network.EOS })

const transactions = [{
  expiration: "2023-09-27T10:00:00",
  ref_block_num: 12345,
  ref_block_prefix: 67890,
  max_net_usage_words: "10",
  max_cpu_usage_ms: "10",
  delay_sec: 0,
  context_free_actions: [],
  actions: [],
  transaction_extensions: []
}]

const response = await tatum.rpc.pushTransaction(transactions)

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Example use cases:

1. **Bulk Transaction Submission:**
   Developers and users can use the `push_transactions` method to broadcast multiple transactions to the EOS network in one go, facilitating various blockchain interactions and operations.

2. **Bulk Smart Contract Interaction:**
   This method is vital for invoking actions on multiple smart contracts deployed on the EOS blockchain, allowing users to interact with multiple decentralized applications simultaneously.

3. **Bulk Token Transfer:**
   `push_transactions` is used for transferring EOS tokens or other tokens deployed on the EOS blockchain between multiple accounts in a single request.

### Request Parameters

The `push_transactions` method requires the following parameters in the request body:

- `Array()` of Transaction Objects, each containing:
   - `expiration` (string, required): Time that transaction must be confirmed by.
   - `ref_block_num` (integer, required)
   - `ref_block_prefix` (integer, required): 32-bit portion of block ID.
   - `max_net_usage_words` (string or integer, required): A whole number.
   - `max_cpu_usage_ms` (string or integer, required): A whole number.
   - `delay_sec` (integer, required)
   - `context_free_actions` (Array of objects, required): Actions that are context-free.
   - `actions` (Array of objects, required): Actions that are context-dependent.
   - `transaction_extensions` (Array of Array of integers or strings): Extensions to the transaction.

### Return Object

Upon successful broadcast of transactions, the `push_transactions` method typically does not return any object but acknowledges with a 200 OK status.

### JSON-RPC Request Example

```json
[
  {
    "expiration": "2023-09-27T10:00:00",
    "ref_block_num": 12345,
    "ref_block_prefix": 67890,
    "max_net_usage_words": "10",
    "max_cpu_usage_ms": "10",
    "delay_sec": 0,
    "context_free_actions": [],
    "actions": [],
    "transaction_extensions": []
  }
]
```
### JSON-RPC Response Example

200 OK status implies successful broadcast, and typically no object is returned.
