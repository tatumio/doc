# push_transactions

### Overview

The `push_transactions` method is designed to submit multiple transactions to the EOS blockchain simultaneously. This method expects an array of transactions in JSON format and attempts to apply them to the blockchain, enabling a range of blockchain interactions like transferring tokens, invoking smart contracts, and more.

{% tabs %}
{% tab title="TypeScript/JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Eos, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Eos>({ network: Network.EOS })

const transactions = [{
  expiration: "2023-09-27T10:00:00",
  refBlockNum: 12345,
  refBlockPrefix: 67890,
  maxNetUsageWords: "10",
  maxCpuUsageMs: "10",
  delaySec: 0,
  contextFreeActions: [],
  actions: [],
  transactionExtensions: []
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

The `pushTransactions` method requires the following parameters in the request body:

- `transactions` (array of Transaction Objects, required), each containing:
   - `expiration` (string, required): Time that the transaction must be confirmed by.
   - `refBlockNum` (integer, required)
   - `refBlockPrefix` (integer, required): 32-bit portion of block ID.
   - `maxNetUsageWords` (string or integer, required): A whole number.
   - `maxCpuUsageMs` (string or integer, required): A whole number.
   - `delaySec` (integer, required): Number of seconds to delay execution (used for scheduling).
   - `contextFreeActions` (array of objects, required): Actions that are context-free.
   - `actions` (array of objects, required): Actions that are context-dependent.
   - `transactionExtensions` (array of array of integers or strings): Extensions to the transaction.

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