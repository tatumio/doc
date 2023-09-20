# gateway\_balances

### How to use it

```javascript
// yarn add @tatumio/tatum

import { TatumSDK, Xrp, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Xrp>({network: Network.XRP})

const res = await tatum.rpc.gatewayBalances('rMwjYedjc7qqtKYVLiAccJSmCwih4LnE2q', {
  hotwallet: ['rKm4uWpg9tfwbVSeATv4KxDe6mpE9yPkgJ', 'ra7JkEzrgeKHdzKgo4EUUVBnxggY4z37kt'],
  ledgerIndex: 'validated',
  strict: true
})

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```

### Overview

The `gateway_balances` method allows you to calculate the total balances issued by a given account, excluding amounts held by operational addresses if needed. This method is beneficial when you want to retrieve the total amount of assets issued by a given Ripple address, especially useful for gateway businesses who need to keep track of the amount of each currency they have issued.

{% embed url="https://codepen.io/tatum-devrel/pen/yLQrxKB" %}

### Parameters

* `account` (string): The Ripple address to check. This should be the issuing address.
* `strict` (boolean, optional): If true, only accept an address or public key for the account parameter. Defaults to false.
* `hotwallet` (string or array, optional): An operational address or an array of such addresses to exclude from the balances issued.
* `ledger_hash` (string, optional): A 20-byte hex string for the ledger version to use.
* `ledger_index` (string or unsigned integer, optional): The ledger index of the ledger version to use, or a shortcut string to choose a ledger automatically.

### Return Object

The `gateway_balances` method returns an object that contains the following fields:

* `account`: The address of the account that issued the balances.
* `obligations`: Total amounts issued to addresses not excluded, as a map of currencies to the total value issued.
* `balances`: Amounts issued to the hotwallet addresses from the request.
* `assets`: Total amounts held that are issued by others. In the recommended configuration, the issuing address should have none.
* `ledger_hash`: The identifying hash of the ledger version that was used to generate this response.
* `ledger_index`: The ledger index of the ledger version that was used to generate this response.

### JSON-RPC Request Example

```json
{
    "method": "gateway_balances",
    "params": [
        {
            "account": "rMwjYedjc7qqtKYVLiAccJSmCwih4LnE2q",
            "hotwallet": [
                "rKm4uWpg9tfwbVSeATv4KxDe6mpE9yPkgJ",
                "ra7JkEzrgeKHdzKgo4EUUVBnxggY4z37kt"
            ],
            "ledger_index": "validated",
            "strict": true
        }
    ]
}
```

### JSON-RPC Response Example

```json
{
    "result": {
        "account": "rMwjYedjc7qqtKYVLiAccJSmCwih4LnE2q",
        "assets": {
            "r9F6wk8HkXrgYWoJ7fsv4VrUBVoqDVtzkH": [
                {
                    "currency": "BTC",
                    "value": "5444166510000000e-26"
                }
            ],
            "rPFLkxQk6xUGdGYEykqe7PR25Gr7mLHDc8": [
                {
                    "currency": "EUR",
                    "value": "4000000000000000e-27"
                }
            ],
            "rPU6VbckqCLW4kb51CWqZdxvYyQrQVsnSj": [
                {
                    "currency": "BTC",
                    "value": "1029900000000000e-26"
                }
            ],
            "rpR95n1iFkTqpoy1e878f4Z1pVHVtWKMNQ": [
                {
                    "currency": "BTC",
                    "value": "4000000000000000e-30"
                }
            ],
            "rwmUaXsWtXU4Z843xSYwgt1is97bgY8yj6": [
                {
                    "currency": "BTC",
                    "value": "8700000000000000e-30"
                }
            ]
        },
        "balances": {
            "rKm4uWpg9tfwbVSeATv4KxDe6mpE9yPkgJ": [
                {
                    "currency": "EUR",
                    "value": "29826.1965999999"
                }
            ],
            "ra7JkEzrgeKHdzKgo4EUUVBnxggY4z37kt": [
                {
                    "currency": "USD",
                    "value": "13857.70416"
                }
            ]
        },
        "ledger_hash": "980FECF48CA4BFDEC896692C31A50D484BDFE865EC101B00259C413AA3DBD672",
        "ledger_index": 14483212,
        "obligations": {
            "BTC": "5908.324927635318",
            "EUR": "992471.7419793958",
            "GBP": "4991.38706013193",
            "USD": "1997134.20229482"
        },
        "status": "success",
        "validated": true
    }
}
```
