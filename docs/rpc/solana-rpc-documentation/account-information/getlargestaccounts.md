# getLargestAccounts

### How to Use It

{% code overflow="wrap" lineNumbers="true" %}
```javascript
// yarn add @tatumio/tatum

import { TatumSDK, Solana, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Solana>({ network: Network.SOLANA })

const res = await tatum.rpc.getLargestAccounts()

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}

### Overview

The `getLargestAccounts` method returns the 20 largest accounts by lamport balance. This method may cache results for up to two hours.

### Parameters

* `options` (object, optional): A configuration object containing:
  * `commitment`(string, optional): Specifies the level of commitment to apply when fetching data.
    * Values: `finalized` `confirmed` `processed`
  * `filter` (string, optional): Filters the results by account type. Possible values are `circulating` or `nonCirculating`.

### Return Object

The result field will be an `RpcResponse` JSON object with a `value` field equal to an array of objects, each containing:

* `address`: Base-58 encoded address of the account.
* `lamports`: Number of lamports in the account.

### JSON-RPC Request Example

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "getLargestAccounts"
}
```

### JSON-RPC Response Example

```json
{
  "jsonrpc": "2.0",
  "result": {
    "context": {
      "slot": 54
    },
    "value": [
      {
        "lamports": 999974,
        "address": "99P8ZgtJYe1buSK8JXkvpLh8xPsCFuLYhz9hQFNw93WJ"
      },
      {
        "lamports": 42,
        "address": "uPwWLo16MVehpyWqsLkK3Ka8nLowWvAHbBChqv2FZeL"
      },
      // ...additional accounts...
    ]
  },
  "id": 1
}
```
