# account\_offers

### How to use it

```javascript
// yarn add @tatumio/tatum

import { TatumSDK, Xrp, Network } from '@tatumio/tatum'

// Initialize the SDK for the XRP network
const tatum = await TatumSDK.init<Xrp>({network: Network.XRP})

// Use the account_offers method
const res = await tatum.rpc.accountOffers('rpP2JgiMyTF5jR5hLG3xHCPi1knBb1v9cM', {
  ledgerIndex: 'validated',
})

await tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```

### Overview

The `account_offers` method retrieves a list of offers made by a given account that are outstanding as of a particular ledger version. It is typically used for monitoring the open offers that a particular account has made on the XRP Ledger's decentralised exchange.

{% embed url="https://codepen.io/tatum-devrel/pen/mdQgGpx" %}

### Parameters

The `account_offers` method accepts the following parameters:

* `account`: A unique identifier for the account, most commonly the account's Address.
* `ledger_hash` (Optional): A 20-byte hex string identifying the ledger version to use.
* `ledger_index` (Optional): The ledger index of the ledger to use, or a shortcut string to choose a ledger automatically.
* `limit` (Optional): Limit the number of Offers to retrieve. The server may return fewer than this number of results. Must be within the inclusive range 10 to 400. The default is 200.
* `marker` (Optional): Value from a previous paginated response. Resume retrieving data where that response left off.
* `strict` (Optional): If true, then the account field only accepts a public key or XRP Ledger address. Otherwise, account can be a secret or passphrase (not recommended). The default is false.

### Return Object

The response follows the standard format, with a successful result containing the following fields:

* `account`: Unique Address identifying the account that made the offers
* `offers`: Array of objects, where each object represents an offer made by this account that is outstanding as of the requested ledger version.
* `ledger_current_index` (Optional): The ledger index of the current in-progress ledger version, which was used when retrieving this data.
* `ledger_index` (Optional): The ledger index of the ledger version that was used when retrieving this data, as requested.
* `ledger_hash` (Optional): The identifying hash of the ledger version that was used when retrieving this data.
* `marker` (Optional): Server-defined value indicating the response is paginated. Pass this to the next call to resume where this call left off.

### JSON-RPC Request Example

```json
{
    "method": "account_offers",
    "params": [
        {
            "account": "rpP2JgiMyTF5jR5hLG3xHCPi1knBb1v9cM"
        }
    ]
}
```

### JSON-RPC Response Example

```json
{
    "result": {
        "account": "rpP2JgiMyTF5jR5hLG3xHCPi1knBb1v9cM",
        "ledger_current_index": 18539596,
        "offers": [{
            "flags": 0,
            "quality": "0.000000007599140009999998",
            "seq": 6578020,
            "taker_gets": "29740867287",
            "taker_pays": {
                "currency": "USD",
                "issuer": "rMwjYedjc7qqtKYVLiAccJSmCwih4LnE2q",
                "value": "226.0050145327418"
            }
        }, {
            "flags": 0,
            "quality": "7989247009094510e-27",
            "seq": 6572128,
            "taker_gets": "2361918758",
            "taker_pays": {
                "currency": "XAU",
                "issuer": "rrh7rf1gV2pXAoqA8oYbpHd8TKv5ZQeo67",
                "value": "0.01886995237307572"
            }
        }, {
            "flags": 0,
            "quality": "0.00000004059594001318974",
            "seq": 6576905,
            "taker_gets": "3892952574",
            "taker_pays": {
                "currency": "CNY",
                "issuer": "rKiCet8SdvWxPXnAgYarFUXMh1zCPz432Y",
                "value": "158.0380691682966"
            }
        },

        ...

        ],
        "status": "success",
        "validated": false
    }
}
```
