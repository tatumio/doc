# account\_lines

### How to use it&#x20;

```javascript
// yarn add @tatumio/tatum

import { TatumSDK, Xrp, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Xrp>({network: Network.XRP})

const res = await tatum.rpc.accountLines('r9cZA1mLK5R5Am25ArfXFmqgNwjZgnfk59', {
  ledgerIndex: 'validated',
  peer: 'r3vi7mWxru9rJCxETCyA1CHvzL96eZWx5z',
  limit: 10,
  marker: 'example_marker',
})

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```

### Overview

The `account_lines` method returns information about an account's trust lines, which contain balances in all non-XRP currencies and assets. All information retrieved is relative to a particular version of the ledger.

{% embed url="https://codepen.io/tatum-devrel/pen/abQxawN" %}

### Parameters

* `account`: (String) A unique identifier for the account, most commonly the account's Address.
* `options`: (AccountLinesOptions) An object with optional parameters:
  * `ledgerHash`: (Optional, String) A 20-byte hex string for the ledger version to use.
  * `ledgerIndex`: (Optional, LedgerIndex) The ledger index of the ledger to use, or a shortcut string to choose a ledger automatically. Can be 'validated', 'closed', 'current', or a number.
  * `peer`: (Optional, String) The Address of a second account. If provided, show only lines of trust connecting the two accounts.
  * `limit`: (Optional, Number) Limit the number of results to retrieve.
  * `marker`: (Optional, unknown) Value from a previous paginated response. Resume retrieving data where that response left off.

### Return Object

The response object has the following properties:

* `account`: (String) Unique Address of the account this request corresponds to. This is the "perspective account" for the purpose of the trust lines.
* `lines`: (Array) Array of trust line objects, as described below. If the number of trust lines is large, only returns up to the limit at a time.
* `ledger_current_index`: (Optional, Integer) The ledger index of the current open ledger, which was used when retrieving this information.
* `ledger_index`: (Optional, Integer) The ledger index of the ledger version that was used when retrieving this data.
* `ledger_hash`: (Optional, String) The identifying hash of the ledger version that was used when retrieving this data.
* `marker`: (Optional, Marker) Server-defined value indicating the response is paginated. Pass this to the next call to resume where this call left off.

Each trust line object has some combination of the following fields:

* `account`: (String) The unique Address of the counterparty to this trust line.
* `balance`: (String) Representation of the numeric balance currently held against this line. A positive balance means that the perspective account holds value; a negative balance means that the perspective account owes value.
* `currency`: (String) A Currency Code identifying what currency this trust line can hold.
* `limit`: (String) The maximum amount of the given currency that this account is willing to owe the peer account.
* `limit_peer`: (String) The maximum amount of currency that the counterparty account is willing to owe the perspective account.
* `quality_in`: (Unsigned Integer) Rate at which the account values incoming balances on this trust line, as a ratio of this value per 1 billion units.
* `quality_out`: (Unsigned Integer) Rate at which the account values outgoing balances on

this trust line, as a ratio of this value per 1 billion units.

* `no_ripple`: (Optional, Boolean) If true, this account has enabled the No Ripple flag for this trust line.
* `no_ripple_peer`: (Optional, Boolean) If true, the peer account has enabled the No Ripple flag for this trust line.
* `authorized`: (Optional, Boolean) If true, this account has authorized this trust line.
* `peer_authorized`: (Optional, Boolean) If true, the peer account has authorized this trust line.
* `freeze`: (Optional, Boolean) If true, this account has frozen this trust line.
* `freeze_peer`: (Optional, Boolean) If true, the peer account has frozen this trust line.

### JSON-RPC Request Example

```json
{
  "id": 1,
  "command": "account_lines",
  "account": "r9cZA1mLK5R5Am25ArfXFmqgNwjZgnfk59",
  "ledger_index": "validated",
  "peer": "r3vi7mWxru9rJCxETCyA1CHvzL96eZWx5z",
  "limit": 10,
  "marker": "example_marker"
}
```

### JSON-RPC Response Example

```json
{
    "id": 1,
    "status": "success",
    "type": "response",
    "result": {
        "account": "r9cZA1mLK5R5Am25ArfXFmqgNwjZgnfk59",
        "lines": [
            {
                "account": "r3vi7mWxru9rJCxETCyA1CHvzL96eZWx5z",
                "balance": "0",
                "currency": "ASP",
                "limit": "0",
                "limit_peer": "10",
                "quality_in": 0,
                "quality_out": 0
            },
            {
                "account": "r3vi7mWxru9rJCxETCyA1CHvzL96eZWx5z",
                "balance": "0",
                "currency": "XAU",
                "limit": "0",
                "limit_peer": "0",
                "no_ripple": true,
                "no_ripple_peer": true,
                "quality_in": 0,
                "quality_out": 0
            }
        ],
        "ledger_index": 1000000
    }
}
```
