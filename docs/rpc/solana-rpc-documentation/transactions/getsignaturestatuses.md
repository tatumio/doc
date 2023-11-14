# getSignatureStatuses

### How to Use It

{% code overflow="wrap" lineNumbers="true" %}
```javascript
// yarn add @tatumio/tatum

import { TatumSDK, Solana, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Solana>({ network: Network.SOLANA })

const signatures = ['4CgnQtRfnUekfn21meTyHYvoAc6pBYK3DhimeiZL6a6o2QXMTHqDomninDkaZLmSfdiEzZfyfLGN4mrDvs8HmnBh'] // list of transaction signatures
const options = {searchTransactionHistory: true} // optional

const res = await tatum.rpc.getSignatureStatuses(signatures, options)

await tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}

### Overview

The `getSignatureStatuses` method fetches the processing statuses of a list of transactions, identified by their signatures. This is especially useful for tracking the status of transactions, whether they are being processed, confirmed or finalised.

{% embed url="https://codepen.io/tatum-devrel/pen/gOQErNL" %}

### Parameters

* `signatures`: (Array of strings, required) An array of transaction signatures to fetch the statuses of.
  * Example: `["4CgnQtRfnUekfn21meTyHYvoAc6pBYK3DhimeiZL6a6o2QXMTHqDomninDkaZLmSfdiEzZfyfLGN4mrDvs8HmnBh"]`
* `options` (object, optional): Configuration object containing the following fields:
  * `searchTransactionHistory` (bool, optional): if `true` - a Solana node will search its ledger cache for any signatures not found in the recent status cache
    * Example: `true`

### Return Object

The result will be an RpcResponse JSON object with `value` equal to an array of JSON objects, consisting of either:

* `null` Unknown transaction, or
* `object`
  * `slot:` The slot the transaction was processed
  * `confirmations:` Number of blocks since signature confirmation, null if rooted, as well as finalized by a supermajority of the cluster
  * `err:`  Error if transaction failed, null if transaction succeeded.&#x20;
  * `confirmationStatus:` The transaction's cluster confirmation status; Either `processed`, `confirmed`, or `finalized`.&#x20;
  * DEPRECATED: `status:` Transaction status object
    * `"Ok":` Transaction was successful
    * `"Err":` Transaction failed with TransactionError

### JSON-RPC Request Example

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "getSignatureStatuses",
  "params": [
    [
      "4CgnQtRfnUekfn21meTyHYvoAc6pBYK3DhimeiZL6a6o2QXMTHqDomninDkaZLmSfdiEzZfyfLGN4mrDvs8HmnBh"
    ],
    {
      "searchTransactionHistory": true
    }
  ]
}
```

### JSON-RPC Response Example

```json
{
  "jsonrpc": "2.0",
  "result": {
    "context": {
      "slot": 82
    },
    "value": [
      {
        "slot": 48,
        "confirmations": null,
        "err": null,
        "status": {
          "Ok": null
        },
        "confirmationStatus": "finalized"
      },
      null
    ]
  },
  "id": 1
}
```
