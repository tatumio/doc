# tx\_history

### How to use it

```javascript
// yarn add @tatumio/tatum

import { TatumSDK, Xrp, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Xrp>({network: Network.XRP})

const res = await tatum.rpc.txHistory(0)

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```

### Overview

The `txHistory` method retrieves some of the most recent transactions made on the XRP Ledger. This is particularly useful for tracking and verifying transaction history, auditing purposes, and other applications where historical transaction data is required.

**Note:** This method is deprecated and may be removed without further notice.

In this example, the `txHistory` method is called with the parameter `start` set to `0`. This will return the most recent transactions.

{% embed url="https://codepen.io/tatum-devrel/pen/dyQLQeo" %}

### Parameters

The `txHistory` method accepts the following parameter:

* `start`: Unsigned Integer. This parameter specifies the number of transactions to skip over, starting from the most recent one.

### Return Object

The method returns a Promise that resolves to an `XrpResult` object. This object contains the following fields:

* `index`: Unsigned Integer. The value of `start` used in the request.
* `status`: String. The status of the request. A value of "success" indicates that the request was successful.
* `txs`: Array. An array of transaction objects.

### JSON-RPC Request Example

```json
{
    "method": "txHistory",
    "params": [
        {
            "start": 0
        }
    ]
}
```

### JSON-RPC Response Example

```json
{
    "result": {
        "index": 0,
        "status": "success",
        "txs": [
            {
                "Account": "rPJnufUfjS22swpE7mWRkn2VRNGnHxUSYc",
                "TransactionType": "OfferCreate",
                // other transaction fields...
            },
            {
                "Account": "rwpxNWdpKu2QVgrh5LQXEygYLshhgnRL1Y",
                "TransactionType": "OfferCreate",
                // other transaction fields...
            }
        ]
    }
}
```
