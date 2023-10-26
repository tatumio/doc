# ripple\_path\_find

### How to use it

```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Xrp, Network, CurrencyAmount, RipplePathFindOptions } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Xrp>({network: Network.XRP})

const destinationAmount: CurrencyAmount = {
  currency: 'USD',
  issuer: 'rvYAfWj5gh67oV6fW32ZzP3Aw4Eubs59B',
  value: '0.001',
}

const res = await tatum.rpc.ripplePathFind(
  'r9cZA1mLK5R5Am25ArfXFmqgNwjZgnfk59',
  'r9cZA1mLK5R5Am25ArfXFmqgNwjZgnfk59',
  destinationAmount
)

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```

### Overview

The `ripple_path_find` method is a simplified version of the `path_find` method that provides a single response with a payment path that can be used immediately. It tries to find the cheapest path or combination of paths for making a payment, but it is not guaranteed that the paths returned are, in fact, the best paths.

The method is available in both the WebSocket and JSON-RPC APIs. However, the results tend to become outdated as time passes. Instead of making multiple calls to stay updated, it is recommended to use the `path_find` method to subscribe to continued updates where possible.

One thing to note is that pathfinding results from untrusted servers need to be handled with care. A server could be modified to return less-than-optimal paths to earn money for its operators. A server may also return poor results when under heavy load. If you do not have your own server that you can trust with pathfinding, you should compare the results of pathfinding from multiple servers run by different parties, to minimize the risk of a single server returning poor results.

### Parameters

The `ripple_path_find` method includes the following parameters:

* `source_account`: Unique address of the account that would send funds in a transaction
* `destination_account`: Unique address of the account that would receive funds in a transaction
* `destination_amount`: Currency Amount that the destination account would receive in a transaction. Special case: New in: rippled 0.30.0 You can specify "-1" (for XRP) or provide -1 as the contents of the value field (for non-XRP currencies). This requests a path to deliver as much as possible, while spending no more than the amount specified in send\_max (if provided).
* `send_max`: (Optional) Currency Amount that would be spent in the transaction. Cannot be used with source\_currencies. New in: rippled 0.30.0
* `source_currencies`: (Optional) Array of currencies that the source account might want to spend. Each entry in the array should be a JSON object with a mandatory currency field and optional issuer field, like how currency amounts are specified. Cannot contain more than 18 source currencies. By default, uses all source currencies available up to a maximum of 88 different currency/issuer pairs.
* `ledger_hash`: (Optional) A 20-byte hex string for the ledger version to use. (See Specifying Ledgers)
* `ledger_index`: (Optional) The ledger index of the ledger to use, or a shortcut string to choose a ledger automatically. (See Specifying Ledgers)

### Return Object

The `ripple_path_find` method returns a result object that includes:

* `alternatives`: Array of objects with possible paths to take. If empty, then there are no paths connecting the source and destination accounts.
* `destination_account`: Unique address of the account that would receive a payment transaction
* `destination_currencies`: Array of strings representing the currencies that the destination accepts, as 3-letter codes like "USD" or as 40-character hex like "015841551A748AD2C1F76FF6ECB0CCCD00000000"

Each element in the alternatives array is an object that represents a path from one possible source currency (held by the initiating account) to the destination account and currency. This object has the following fields:

* `paths_computed`: Array of arrays of objects defining payment paths
* `source_amount`: Currency Amount that the source would have to send along this path for the destination to receive the desired amount

### JSON-RPC Request Example

```json
{
    "method": "ripple_path_find",
    "params": [
        {
            "destination_account": "r9cZA1mLK5R5Am25ArfXFmqgNwjZgnfk59",
            "destination_amount": {
                "currency": "USD",
                "issuer": "rvYAfWj5gh67oV6fW32ZzP3Aw4Eubs59B",
                "value": "0.001"
            },
            "source_account": "r9cZA1mLK5R5Am25ArfXFmqgNwjZgnfk59",
            "source_currencies": [
                {
                    "currency": "XRP"
                },
                {
                    "currency": "USD"
                }
            ]
        }
    ]
}
```

### JSON-RPC Response Example

```json
{
    "result": {
        "alternatives": [
            {
                "paths_computed": [
                    [
                        {
                            "currency": "USD",
                            "issuer": "rpDMez6pm6dBve2TJsmDpv7Yae6V5Pyvy2",
                            "type": 48,
                            "type_hex": "0000000000000030"
                        },
                        {
                            "account": "rpDMez6pm6dBve2TJsmDpv7Yae6V5Pyvy2",
                            "type": 1,
                            "type_hex": "0000000000000001"
                        },
                        {
                            "account": "rfDeu7TPUmyvUrffexjMjq3mMcSQHZSYyA",
                            "type": 1,
                            "type_hex": "0000000000000001"
                        },
                        {
                            "account": "rvYAfWj5gh67oV6fW32ZzP3Aw4Eubs59B",
                            "type": 1,
                            "type_hex": "0000000000000001"
                        }
                    ]
                ],
                "source_amount": "207414"
            }
        ],
        "destination_account": "r9cZA1mLK5R5Am25ArfXFmqgNwjZgnfk59",
        "destination_currencies": [
            "USD",
            "JOE",
            "BTC",
            "DYM",
            "CNY",
            "EUR",
            "015841551A748AD2C1F76FF6ECB0CCCD00000000",
            "MXN",
            "XRP"
        ],
        "status": "success"
    }
}
```
