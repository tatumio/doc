# account\_info

### How to use it

```javascript
// yarn add @tatumio/tatum

import { TatumSDK, Xrp, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Xrp>({network: Network.XRP})

const res = await tatum.rpc.accountInfo('rG1QQv2nh2gr7RCZ1P8YYcBUKCCN633jCn', {
  ledgerIndex: 'current',
  strict: true,
  queue: true,
  signerLists: true
})

await tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```

### Overview

The `accountInfo` method retrieves information about an account, its activity, and its XRP balance. All information retrieved is relative to a particular version of the ledger.

{% embed url="https://codepen.io/tatum-devrel/pen/RwqOYKL" %}

### Parameters

The method accepts two parameters:

* `account` (**required**): A unique identifier for the account, most commonly the account's Address.
* `options` (**optional**): An object with the following properties:
  * `ledgerHash`: A 20-byte hex string for the ledger version to use.
  * `ledgerIndex`: The ledger index of the ledger to use, or a shortcut string to choose a ledger automatically.
  * `queue`: If true, also returns stats about queued transactions associated with this account. Can only be used when querying for the data from the current open ledger.
  * `signerLists`: If true, also returns any SignerList objects associated with this account.
  * `strict`: If true, then the `account` field only accepts a public key or XRP Ledger address. Otherwise, `account` can be a secret or passphrase (not recommended). The default is false.

### Return Object

The `accountInfo` method returns object with following fields:

* `account_data`: This is an object that contains the AccountRoot ledger object with this account's information, as stored in the ledger.
* `signer_lists`: This is an array of SignerList ledger objects associated with this account for Multi-Signing. This field is omitted unless the request specified signer\_lists and at least one SignerList is associated with the account. Since an account can own at most one SignerList, this array must have exactly one member if it is present.
* `ledger_current_index`: This is the ledger index of the current in-progress ledger, which was used when retrieving this information. This is omitted if ledger\_index is provided instead.
* `ledger_index`: This is the ledger index of the ledger version used when retrieving this information. The information does not contain any changes from ledger versions newer than this one. This is omitted if ledger\_current\_index is provided instead.
* `queue_data`: This is an object that contains information about queued transactions sent by this account. This information describes the state of the local rippled server, which may be different from other servers in the peer-to-peer XRP Ledger network. Some fields may be omitted because the values are calculated "lazily" by the queuing mechanism. This is omitted unless queue specified as true and querying the current open ledger.
* `validated`: This is a boolean value that is true if this data is from a validated ledger version. If omitted or set to false, this data is not final.

The `queue_data` parameter, if present, contains the following fields:

* `txn_count`: The number of queued transactions from this address.
* `auth_change_queued`: Whether a transaction in the queue changes this address's ways of authorizing transactions. If true, this address can queue no further transactions until that transaction has been executed or dropped from the queue.
* `lowest_sequence`: The lowest Sequence Number among transactions queued by this address.
* `highest_sequence`: The highest Sequence Number among transactions queued by this address.
* `max_spend_drops_total`: The integer amount of drops of XRP that could be debited from this address if every transaction in the queue consumes the maximum amount of XRP possible.
* `transactions`: An array containing information about each queued transaction from this address. Each object in the `transactions` array, if present, may contain any or all of the following fields:
  * `auth_change`: Whether this transaction changes this address's ways of authorizing transactions.
  * `fee`: The Transaction Cost of this transaction, in drops of XRP.
  * `fee_level`: The transaction cost of this transaction, relative to the minimum cost for this type of transaction, in fee levels.
  * `max_spend_drops`: The maximum amount of XRP, in drops, this transaction could send or destroy.
  * `seq`: The Sequence Number of this transaction.

\


### JSON-RPC Request Example

Here's an example of how the JSON-RPC request might look like:

```json
{
  "id": 2,
  "command": "account_info",
  "account": "rG1QQv2nh2gr7RCZ1P8YYcBUKCCN633jCn",
  "strict": true,
  "ledger_index": "current",
  "queue": true
}
```

### JSON-RPC Response Example

Here's an example of how the JSON-RPC response might look like:

```json
{
  "id": 5,
  "status": "success",
  "type": "response",
  "result": {
        "account_data": {
            "Account": "rG1QQv2nh2gr7RCZ1P8YYcBUKCCN633jCn",
            "Balance": "999999999960",
            "Flags": 8388608,
            "LedgerEntryType": "AccountRoot",
            "OwnerCount": 0,
            "PreviousTxnID": "4294BEBE5B569A18C0A2702387C9B1E7146DC3A5850C1E87204951C6FDAA4C42",
            "PreviousTxnLgrSeq": 3,
            "Sequence": 6,
            "index": "92FA6A9FC8EA6018D5D16532D7795C91BFB0831355BDFDA177E86C8BF997985F"
        },
        "ledger_current_index": 4,
        "queue_data": {
            "auth_change_queued": true,
            "highest_sequence": 10,
            "lowest_sequence": 6,
            "max_spend_drops_total": "500",
            "transactions": [
                {
                    "auth_change": false,
                    "fee": "100",
                    "fee_level": "2560",
                    "max_spend_drops": "100",
                    "seq": 6
                },
                ... (trimmed for length) ...
                {
                    "LastLedgerSequence": 10,
                    "auth_change": true,
                    "fee": "100",
                    "fee_level": "2560",
                    "max_spend_drops": "100",
                    "seq": 10
                }
            ],
            "txn_count": 5
        },
        "status": "success",
        "validated": false
    }
}
```
