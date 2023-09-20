# ledger\_closed

### How to use it

```javascript
// yarn add @tatumio/tatum

import { TatumSDK, Xrp, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Xrp>({network: Network.XRP})

const res = await tatum.rpc.ledgerClosed()

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```

### Overview

The `ledger_closed` method is used to fetch the unique identifiers of the most recently closed ledger. Note that the ledger might not be validated and immutable yet, so use this method when you need information about the latest ledger and not necessarily the final state.

{% embed url="https://codepen.io/tatum-devrel/pen/MWzRPbb" %}

### Parameters

This method does not require any parameters.

### Return Object

The `ledger_closed` method returns an object with the following fields:

* `ledger_hash` (String): The unique hash of this ledger version, in hexadecimal.
* `ledger_index` (Unsigned Integer): The ledger index of this ledger version.

### JSON-RPC Request Example

Here's an example of the `ledger_closed` method request:

```json
{
   "id": 2,
   "command": "ledger_closed"
}
```

### JSON-RPC Response Example

Here's an example of a successful response:

```json
{
  "id": 1,
  "status": "success",
  "type": "response",
  "result": {
    "ledger_hash": "17ACB57A0F73B5160713E81FE72B2AC9F6064541004E272BD09F257D57C30C02",
    "ledger_index": 6643099
  }
}
```

In this response, `ledger_hash` is the unique identifier of the ledger, and `ledger_index` is the index number of this ledger version.
