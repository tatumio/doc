# noripple\_check

### How to use it

```javascript
// yarn add @tatumio/tatum

import { TatumSDK, Xrp, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Xrp>({network: Network.XRP})

const result = await tatum.rpc.norippleCheck('r9cZA1mLK5R5Am25ArfXFmqgNwjZgnfk59', 'gateway', {
  transactions: true,
  limit: 2
})

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```

### Overview

The `noripple_check` method provides a quick way to check the status of the Default Ripple field for an account and the No Ripple flag of its trust lines, compared with the recommended settings. This can be useful for developers and administrators who want to ensure that their accounts are configured correctly, especially when managing the accounts of large or complex financial organisations.

{% embed url="https://codepen.io/tatum-devrel/pen/poQBOLM" %}

### Parameters

* `account` (String): A unique identifier for the account, most commonly the account's address.
* `role` (String): Whether the address refers to a gateway or user. Recommendations depend on the role of the account. Issuers must have Default Ripple enabled and must disable No Ripple on all trust lines. Users should have Default Ripple disabled, and should enable No Ripple on all trust lines.
* `transactions` (Boolean, optional): If true, include an array of suggested transactions, as JSON objects, that you can sign and submit to fix the problems. Defaults to false.
* `limit` (Number, optional): The maximum number of trust line problems to include in the results. Defaults to 300.

### Return Object

The `noripple_check` method returns an object with the following fields:

* `ledger_current_index` (Number): The ledger index of the ledger used to calculate these results.
* `problems` (Array): Array of strings with human-readable descriptions of the problems. This includes up to one entry if the account's Default Ripple setting is not as recommended, plus up to limit entries for trust lines whose No Ripple setting is not as recommended.
* `transactions` (Array): If the request specified transactions as true, this is an array of JSON objects, each of which is the JSON form of a transaction that should fix one of the described problems. The length of this array is the same as the problems array, and each entry is intended to fix the problem described at the same index into that array.

### JSON-RPC Request Example

```json
{
    "method": "noripple_check",
    "params": [
        {
            "account": "r9cZA1mLK5R5Am25ArfXFmqgNwjZgnfk59",
            "ledger_index": "current",
            "limit": 2,
            "role": "gateway",
            "transactions": true
        }
    ]
}
```

### JSON-RPC Response Example

```json
{
    "result": {
        "ledger_current_index": 14380381,
        "problems": [
            "You should immediately set your default ripple flag",
            "You should clear the no ripple flag on your XAU line to r3vi7mWxru9rJCxETCyA1CHvzL96eZWx5z",
            "You should clear the no ripple flag on your USD line to rMwjYedjc7qqtKYVLiAccJSmCwih4LnE2q"
        ],
        "status": "success",
        "transactions": [
            {
                "Account": "r9cZA1mLK5R5Am25ArfXFmqgNwjZgnfk59",
                "Fee": 10000,
                "Sequence": 1406,
                "SetFlag": 8,
                "TransactionType": "AccountSet"
            },
            {
                "Account": "r9cZA1mLK5R5Am25ArfXFmqgNwjZgnfk59",
                "Fee": 10000,
                "Flags": 262144,
                "LimitAmount": {
                    "currency": "XAU",
                    "issuer": "r3vi7mWxru9rJCxETCyA1CHvzL96eZWx5z",
                    "value": "0"
                },
                "Sequence": 1407,
                "TransactionType": "TrustSet"
            },
            {
                "Account": "r9cZA1mLK5R5Am25ArfXFmqgNwjZgnfk59",
                "Fee": 10000,
                "Flags": 262144,
                "LimitAmount": {
                    "currency": "USD",
                    "issuer": "rMwjYedjc7qqtKYVLiAccJSmCwih4LnE2q",
                    "value": "5"
                },
                "Sequence": 1408,
                "TransactionType": "TrustSet"
            }
        ],
        "validated": false
    }
}
```
