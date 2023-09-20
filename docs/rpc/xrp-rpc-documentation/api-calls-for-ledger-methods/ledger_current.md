# ledger\_current

### How to use it

```javascript
// yarn add @tatumio/tatum

import { TatumSDK, Xrp, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Xrp>({network: Network.XRP})

const res = await tatum.rpc.ledgerCurrent()

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```

### Overview

The `ledger_current` method is used to fetch the unique identifier (the ledger index) of the current in-progress ledger. This command is mostly useful for testing, as the returned ledger is still in flux and its contents are constantly changing.

{% embed url="https://codepen.io/tatum-devrel/pen/RwqOeoE" %}

### Parameters

This method does not require any parameters.

### Return Object

The `ledger_current` method returns an object with the following field:

* `ledger_current_index` (Unsigned Integer - Ledger Index): The ledger index of this ledger version.

Note: A `ledger_hash` field is not provided, because the hash of the current ledger is constantly changing along with its contents.

### JSON-RPC Request Example

Here's an example of the `ledger_current` method request:

```json
{
    "method": "ledger_current",
    "params": [
        {}
    ]
}
```

### JSON-RPC Response Example

Here's an example of a successful response:

```json
{
    "result": {
        "ledger_current_index": 8696233,
        "status": "success"
    }
}
```

In this response, `ledger_current_index` is the index number of the current in-progress ledger.
