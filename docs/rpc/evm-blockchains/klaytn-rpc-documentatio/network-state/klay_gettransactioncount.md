# eth\_getTransactionCount

### How to use it

{% tabs %}
{% tab title="TypeScript/JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Klaytn, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Klaytn>({network: Network.KLAYTN})

const result = await tatum.rpc.getTransactionCount('0x3E18a8c3348447E3e69c847FbAA07117E2f46a1b', 'latest')

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Overview

The `klay_getTransactionCount` method is an JSON-RPC method that retrieves the number of transactions sent from a given address. It is a useful method for developers who need to keep track of an account's nonce value to avoid transaction collisions or incorrect order of execution. The nonce value is essential for ensuring transaction uniqueness and preventing replay attacks.

Use cases for this method include:

* Determining the nonce value for a new transaction to be sent from a specific address
* Monitoring the number of transactions sent by an address to observe its activity
* Troubleshooting transaction issues and verifying if a transaction was submitted successfully

### Parameters

The `klay_getTransactionCount` method accepts two parameters:

1. **`address`** - The address whose transaction count will be retrieved.
   * Example: `"0xBB52B2B91488d60eFb6848bBadd000005A511E5C"`
2. **`blockParameter`** - A string indicating the block number or block state to consider when retrieving the transaction count.
   * Possible values: `"earliest"`, `"latest"`, `"pending"`, or a specific block number in hexadecimal format
   * Example: `"latest"`

### Return Object

The method returns a single value:

* **`transactionCount`** - A hexadecimal representation of the number of transactions sent from the specified address.
  * Example: `"0x1e"`

### JSON-RPC Request and Response Examples

_Request_:

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "klay_getTransactionCount",
  "params": [
    "0xBB52B2B91488d60eFb6848bBadd000005A511E5C",
    "latest"
  ]
}
```

_Response_:

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": {
    "BigNumber": {
      "s": 1,
      "e": 0,
      "c": [1]
    }
  }
}
```
