# account\_objects

### How to use it

```javascript
// yarn add @tatumio/tatum

import { TatumSDK, Xrp, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Xrp>({network: Network.XRP})

const res = await tatum.rpc.accountObjects('r9cZA1mLK5R5Am25ArfXFmqgNwjZgnfk59', {
  ledger_index: 'validated',
  type: 'state',
  deletion_blockers_only: false,
  limit: 10
})

await tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```

### Overview

The `accountObjects` method returns the raw ledger format for all objects owned by an account. This includes Offer objects for orders that are currently live, unfunded, or expired but not yet removed, RippleState objects for trust lines where this account's side is not in the default state, the account's SignerList, if the account has multi-signing enabled, Escrow objects for held payments that have not yet been executed or canceled, PayChannel objects for open payment channels, Check objects for pending Checks, DepositPreauth objects for deposit preauthorizations, Ticket objects for Tickets, and NFTokenPage objects for collections of NFTs.

{% embed url="https://codepen.io/tatum-devrel/pen/bGQJxYQ" %}

### Parameters

#### Main Parameters

* `account`: A unique identifier for the account, most commonly the account's Address.

#### Optional Parameters (part of `options?: AccountObjectsOptions` object)

* `deletion_blockers_only`: If true, the response only includes objects that would block this account from being deleted. The default is false.
* `ledger_hash`: A 20-byte hex string for the ledger version to use.
* `ledger_index`: The ledger index of the ledger to use, or a shortcut string to choose a ledger automatically.
* `limit`: The maximum number of objects to include in the results. Must be within the inclusive range 10 to 400 on non-admin connections. The default is 200.
* `marker`: Value from a previous paginated response. Resume retrieving data where that response left off.
* `type`: Filter results by a ledger entry type. The valid types are: check, deposit\_preauth, escrow, nft\_offer, offer, payment\_channel, signer\_list, state (trust line), and ticket.

### Return Object

The returned object will be a successful result containing the account's address and an array of objects owned by this account.&#x20;

Here are the fields in the response:

* `account`: This is a string that represents the unique address of the account that this request corresponds to.
* `account_objects`: This is an array of objects owned by the account. Each object is in its raw ledger format. The specific fields in each object can vary depending on the type of the object. Common ledger object types include Offer, RippleState, AccountRoot, and others.
* `ledger_hash`: This is a string that may be omitted. It represents the identifying hash of the ledger that was used to generate this response.
* `ledger_index`: This is a number that may be omitted. It represents the ledger index of the ledger version that was used to generate this response.
* `ledger_current_index`: This is a number that may be omitted. It represents the ledger index of the current in-progress ledger version, which was used to generate this response.
* `limit`: This is a number that may be omitted. It represents the limit that was used in this request, if any.
* `marker`: This is a server-defined value indicating the response is paginated. You can pass this to the next call to resume where this call left off. It is omitted when there are no additional pages after this one.
* `validated`: This is a boolean. If included and set to true, the information in this response comes from a validated ledger version. Otherwise, the information is subject to change.

### JSON-RPC Request Example

```json
{
  "method": "account_objects",
  "params": [
    {
      "account": "r9cZA1mLK5R5Am25ArfXFmqgNwjZgnfk59",
      "ledger_index": "validated",
      "type": "state",
      "deletion_blockers_only": false,
      "limit": 10
    }
  ]
}
```

### JSON-RPC Response Example

```json
{
    "result": {
        "account": "r9cZA1mLK5R5Am25ArfXFmqgNwjZgnfk59",
        "account_objects": [
            {
                "Balance": {
                    "currency": "ASP",
                    "issuer": "rrrrrrrrrrrrrrrrrrrrBZbvji",
                    "value": "0"
                },
                "Flags": 65536,
                "HighLimit": {
                    "currency": "ASP",
                    "issuer": "r9cZA1mLK5R5Am25ArfXFmqgNwjZgnfk59",
                    "value": "0"
                },
                "HighNode": "0000000000000000",
                "LedgerEntryType": "RippleState",
                "LowLimit": {
                    "currency": "ASP",
                    "issuer": "r3vi7mWxru9rJCxETCyA1CHvzL96eZWx5z",
                    "value": "10"
                },
                "LowNode": "0000000000000000",
                "PreviousTxnID": "BF7555B0F018E3C5E2A3FF9437A1A5092F32903BE246202F988181B9CED0D862",
                "PreviousTxnLgrSeq": 1438879,
                "index": "2243B0B630EA6F7330B654EFA53E27A7609D9484E535AB11B7F946DF3D247CE9"
            },
            {
                "Balance": {
                    "currency": "XAU",
                    "issuer": "rrrrrrrrrrrrrrrrrrrrBZbvji",
                    "value": "0"
                },
                "Flags": 3342336,
                "HighLimit": {
                    "currency": "XAU",
                    "issuer": "r9cZA1mLK5R5Am25ArfXFmqgNwjZgnfk59",
                    "value": "0"
                },
                "HighNode": "0000000000000000",
                "LedgerEntryType": "RippleState",
                "LowLimit": {
                    "currency": "XAU",
                    "issuer": "r3vi7mWxru9rJCxETCyA1CHvzL96eZWx5z",
                    "value": "0"
                },
                "LowNode": "0000000000000000",
                "PreviousTxnID": "79B26D7D34B950AC2C2F91A299A6888FABB376DD76CFF79D56E805BF439F6942",
                "PreviousTxnLgrSeq": 5982530,
                "index": "9ED4406351B7A511A012A9B5E7FE4059FA2F7650621379C0013492C315E25B97"
            },
            {
                "Balance": {
                    "currency": "USD",
                    "issuer": "rrrrrrrrrrrrrrrrrrrrBZbvji",
                    "value": "0"
                },
                "Flags": 1114112,
                "HighLimit": {
                    "currency": "USD",
                    "issuer": "rMwjYedjc7qqtKYVLiAccJSmCwih4LnE2q",
                    "value": "0"
                },
                "HighNode": "0000000000000000",
                "LedgerEntryType": "RippleState",
                "LowLimit": {
                    "currency": "USD",
                    "issuer": "r9cZA1mLK5R5Am25ArfXFmqgNwjZgnfk59",
                    "value": "5"
                },
                "LowNode": "0000000000000000",
                "PreviousTxnID": "6FE8C824364FB1195BCFEDCB368DFEE3980F7F78D3BF4DC4174BB4C86CF8C5CE",
                "PreviousTxnLgrSeq": 10555014,
                "index": "2DECFAC23B77D5AEA6116C15F5C6D4669EBAEE9E7EE050A40FE2B1E47B6A9419"
            }
        ],
        "ledger_hash": "4C99E5F63C0D0B1C2283B4F5DCE2239F80CE92E8B1A6AED1E110C198FC96E659",
        "ledger_index": 14380380,
        "limit": 10,
        "marker": "F60ADF645E78B69857D2E4AEC8B7742FEABC8431BD8611D099B428C3E816DF93,94A9F05FEF9A153229E2E997E64919FD75AAE2028C8153E8EBDB4440BD3ECBB5",
        "status": "success",
        "validated": true
    }
}
```
