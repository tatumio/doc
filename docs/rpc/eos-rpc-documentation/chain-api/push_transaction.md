# push_transaction

### Overview

The `push_transaction` method is utilized to transmit a transaction to the EOS blockchain. This method takes a transaction in JSON format and endeavors to apply it to the blockchain, facilitating numerous interactions such as transferring tokens and invoking smart contracts.
{% tabs %}
{% tab title="TypeScript/JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Eos, Network } from '@tatumio/tatum'
  
const tatum = await TatumSDK.init<Eos>({ network: Network.EOS })

const transaction = { 
  signatures: [/* array of signatures */], 
  compression: false, 
  packedContextFreeData: 'string', // json to hex
  packedTrx: 'string' // Transaction object json to hex
}

const response = await tatum.rpc.pushTransaction(transaction)

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Example use cases:

1. **Transaction Submission:**
   Developers and users might employ the `push_transaction` method to broadcast transactions to the EOS network, allowing for various interactions and operations on the blockchain.

2. **Smart Contract Interaction:**
   Invoking actions on smart contracts deployed on the EOS blockchain is another crucial functionality of this method, granting users the ability to interface with decentralized applications.

3. **Token Transfer:**
   For transferring EOS tokens or other tokens available on the EOS blockchain between accounts, the `push_transaction` method is used.

### Request Parameters

The `pushTransaction` method mandates the following parameters in the request body:

* `signatures` (array of strings, required) - An array of strings representing signatures needed to authorize the transaction.
* `compression` (boolean, required) - A boolean indicating the status of compression used, typically false.
* `packedContextFreeData` (string, required) - Represents the JSON converted to hex.
* `packedTrx` (string, required) - Specifies the transaction object, converted from JSON to hex.

### Return Object

When a transaction is successfully broadcasted, the `push_transaction` method typically returns nothing but a 200 OK status.

### JSON-RPC Request Example

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "push_transaction",
  "params": {
    "signatures": ["SIG_K1_..."],
    "compression": false,
    "packedContextFreeData": "746573742064617461", // Example hex of JSON data
    "packedTrx": "00e1f5055c95b089c2e0d0e4" // Example hex of JSON transaction object
  }
}
```
### JSON-RPC Response Example

```json
{
  "jsonrpc": "2.0",
  "id": 1
}
```