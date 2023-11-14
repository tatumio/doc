# transaction\_entry

### How to use it

```javascript
// yarn add @tatumio/tatum

import { TatumSDK, Xrp, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Xrp>({network: Network.XRP})

const res = await tatum.rpc.transactionEntry('C53ECF838647FA5A4C780377025FEC7999AB4182590510CA461444B207AB74A9', {
  ledgerIndex: '56865245',
})

await tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```

### Overview

The `transaction_entry` method retrieves information on a single transaction from a specific ledger version. It does not search all ledgers for the specified transaction, unlike the `tx` method, which does. The `transaction_entry` method is useful for fetching transaction data from a specified ledger, making it an essential method for auditing or tracking transaction histories.

It's important to note that this method does not support retrieving information from the current in-progress ledger. A ledger version must be specified in either `ledger_index` or `ledger_hash`.

This method can fail to find the transaction due to the following reasons:

* The transaction does not exist.
* The transaction exists, but not in the specified ledger version.
* The server does not have the specified ledger version available. Another server that has the correct version on hand may have a different response.

{% embed url="https://codepen.io/tatum-devrel/pen/xxQeQXN" %}

### Parameters

The parameters required for this method are:

* `txHash`: (String) The unique hash of the transaction you are looking up.
* `options`: (Ledger) Options for specifying the ledger to use. It includes the following properties:
  * `ledger_hash`: (Optional) A 20-byte hex string for the ledger version to use.
  * `ledger_index`: (Optional) The ledger index of the ledger to use, or a shortcut string to choose a ledger automatically.

### Return Object

The `transaction_entry` method returns an object that provides detailed information about a transaction from a specified ledger. The object contains the following fields:

* `ledger_index`: A number that represents the ledger index of the ledger version the transaction was found in; this is the same as the one from the request.
* `ledger_hash`: A string that represents the identifying hash of the ledger version the transaction was found in; this is the same as the one from the request. This field may be omitted.
* `metadata`: An object that represents the transaction metadata. This shows the exact results of the transaction in detail.
* `tx_json`: An object that represents the JSON representation of the Transaction object.

### JSON-RPC Request Example

```json
{
  "method": "transaction_entry",
  "params": [
    {
      "tx_hash": "C53ECF838647FA5A4C780377025FEC7999AB4182590510CA461444B207AB74A9",
      "ledger_index": 56865245
    }
  ]
}
```

### JSON-RPC Response Example

```json
{
  "result": {
    "ledger_hash": "793E56131D8D4ABFB27FA383BFC44F2978B046E023FF46C588D7E0C874C2472A",
    "ledger_index": 56865245,
    "metadata": { /* Detailed result of the transaction */ },
    "status": "success",
    "tx_json": { /* JSON representation of the Transaction object */ },
    "validated": true
  }
}
```
