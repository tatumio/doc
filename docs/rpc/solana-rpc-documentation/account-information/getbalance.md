# getBalance

### How to use it

{% code overflow="wrap" lineNumbers="true" %}
```javascript
// yarn add @tatumio/tatum

import { TatumSDK, Solana, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Solana>({ network: Network.SOLANA })

const res = await tatum.rpc.getBalance('8Ew6iQXcTRHAUNNu3X9VBn1g1bJkXEZJ9gFD2AGKtdPB')

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}

### Overview

The `getBalance` RPC method is used to retrieve the current balance of a specified account on the Solana blockchain. It's a straightforward and efficient way to monitor and keep track of account balances.

This method is typically used in scenarios where you need to check the available balance before initiating a transaction or for accounting purposes in a wallet application.

### Parameters

The `getBalance` method requires one parameter:

* (string, required) Pubkey of account to query, as base-58 encoded string
  * Example: `"8Ew6iQXcTRHAUNNu3X9VBn1g1bJkXEZJ9gFD2AGKtdPB"`

### Return object

The `getBalance` method returns an object containing the following fields:

* `context`: An object containing details about the context in which the balance was fetched.
  * `slot`: The slot at which the data was fetched.
* `value`: The current balance of the account, in lamports.

### JSON-RPC Request Example

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "getBalance",
  "params": [
    "8Ew6iQXcTRHAUNNu3X9VBn1g1bJkXEZJ9gFD2AGKtdPB",
  ]
}
```

### JSON-RPC Response Example

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": {
    "context": {
      "slot": 194573649
    },
    "value": 2484257209
  }
}
```
