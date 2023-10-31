# ledger

{% hint style="warning" %}
XRP only maintains history from ledger 32570, for more info see [onxrp.com/missing-genesis-block-xrpl/](https://onxrp.com/missing-genesis-block-xrpl/)
{% endhint %}

### How to use it

```javascript
import { TatumSDK, Xrp, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Xrp>({network: Network.XRP})

const res = await tatum.rpc.ledger({
  ledgerIndex: 'validated',
  full: false,
  accounts: false,
  transactions: false,
  expand: false,
  ownerFunds: false,
})

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```

### Overview

The `ledger` RPC method is used to retrieve information about the public ledger in XRP. You can specify various options to customize the returned information, such as the ledger version, whether to include full information on the entire ledger, the ledger's entire state data, information on transactions in the specified ledger version, and so on.

Use cases for this method include retrieving information about a specific ledger, examining the transactions that have occurred in a specific ledger version, examining the state data of a ledger, and more.

{% embed url="https://codepen.io/tatum-devrel/pen/GRwLXGG?editors=1111" %}

### Parameters

The `ledger` method takes an optional `LedgerOptions` object. This object can contain the following fields:

* `full` (boolean): If true, return full information on the entire ledger.
* `accounts` (boolean): If true, return the ledger's entire state data.
* `transactions` (boolean): If true, return information on transactions in the specified ledger version.
* `expand` (boolean): Provide full JSON-formatted information for transaction/account information instead of only hashes.
* `ownerFunds` (boolean): If true, include owner\_funds field in the metadata of OfferCreate transactions in the response.
* `binary` (boolean): If true, return the requested ledger object's contents as a hex string in the XRP Ledger's binary format.

### Return Object

The method returns a promise that resolves to an `XrpResult` object. This object contains information about the ledger, including the following fields:

* `ledger.account_hash`: A string representing the hash of all account state information in this ledger, as hexadecimal.
* `ledger.accountState`: An array of all the account-state information in this ledger. This field is omitted unless explicitly requested.
* `ledger.close_flags`: An integer representing a bitmap of flags relating to the closing of this ledger.
* `ledger.close_time`: An integer representing the time this ledger was closed, in seconds since the Ripple Epoch.
* `ledger.close_time_human`: A string representing the time this ledger was closed, in human-readable format. Always uses the UTC time zone.
* `ledger.close_time_resolution`: An integer representing how ledger close times are rounded. Ledger close times are rounded to within this many seconds.
* `ledger.closed`: A boolean indicating whether or not this ledger has been closed.
* `ledger.ledger_hash`: A string representing the unique identifying hash of the entire ledger.
* `ledger.ledger_index`: A string representing the Ledger Index of this ledger, as a quoted integer.
* `ledger.parent_close_time`: An integer representing the time at which the previous ledger was closed.
* `ledger.parent_hash`: A string representing the unique identifying hash of the ledger that came immediately before this one.
* `ledger.total_coins`: A string representing the total number of XRP drops in the network, as a quoted integer. This decreases as transaction costs destroy XRP.
* `ledger.transaction_hash`: A string representing the hash of the transaction information included in this ledger, as hexadecimal.
* `ledger.transactions`: An array of transactions applied in this ledger version. By default, members are the transactions' identifying Hash strings. If the request specified `expand` as true, members are full representations of the transactions instead, in either JSON or binary depending on whether the request specified binary as true.

Within the `queue_data` object, which is an array of objects describing queued transactions, you can find the following fields:

* `account`: The Address of the sender for this queued transaction.
* `tx`: By default, this is a string containing the identifying hash of the transaction. If transactions are expanded in binary format, this is an object whose only field is `tx_blob`, containing the binary form of the transaction as a decimal string. If transactions are expanded in JSON format, this is an object containing the transaction object including the transaction's identifying hash in the `hash` field.
* `retries_remaining`: The number of times this transaction can be retried before being dropped.
* `preflight_result`: The tentative result from preliminary transaction checking. This is always `tesSUCCESS`.
* `last_result`: If this transaction was left in the queue after getting a retriable (ter) result, this is the exact ter result code it got. This field may be omitted.
* `auth_change`: Indicates whether this transaction changes this address's ways of authorizing transactions. This field may be omitted.
* `fee`: The Transaction Cost of this transaction, in drops of XRP. This field may be omitted.
* `fee_level`: The transaction cost of this transaction, relative to the minimum cost for this type of transaction, in fee levels. This field may be omitted.
* `max_spend_drops`: The maximum amount of XRP, in drops, this transaction could potentially send or destroy. This field may be omitted.



### JSON-RPC Request Example

Here is an example of a JSON-RPC request using the `ledger` method:

```json
{
  "method": "ledger",
  "params": [
    {
      "ledger_index": "validated",
      "accounts": false,
      "full": false,
      "transactions": false,
      "expand": false,
      "owner_funds": false
    }
  ]
}
```

### JSON-RPC Response Example

Here is an example of a successful JSON-RPC response:

```json
{
  "result": {
    "ledger": {
      "accepted": true,
      "account_hash": "B258A8BB4743FB74CBBD6E9F67E4A56C4432EA09E5805E4CC2DA26F2DBE8F3D1",
      "close_flags": 0,
      "close_time": 638329271,
      "close_time_human": "2020-Mar-24 01:41:11.000000000 UTC",
      "close_time_resolution": 10,
      "closed": true,
      "hash": "3652D7FD0576BC452C0D2E9B747BDD733075971D1A9A1D98125055DEF428721A",
      "ledger_hash": "3652D7FD0576BC452C0D2E9B747BDD733075971D1A9A1D98125055DEF428721A",
      "ledger_index": "54300940",
      "parent_close_time": 638329270,
      "parent_hash": "AE996778246BC81F85D5AF051241DAA577C23BCA04C034A7074F93700194520D",
      "seqNum": "54300940",
      "totalCoins": "99991024049618156",
      "total_coins": "99991024049618156",
      "transaction_hash": "FC6FFCB71B2527DDD630EE5409D38913B4D4C026AA6C3B14A3E9D4ED45CFE30D"
    },
    "ledger_hash": "3652D7FD0576BC452C0D2E9B747BDD733075971D1A9A1D98125055DEF428721A",
    "ledger_index": 54300940,
    "status": "success",
    "validated": true
  }
}
```
