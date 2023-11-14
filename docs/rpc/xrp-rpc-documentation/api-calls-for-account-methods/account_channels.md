# account\_channels

### How to use it

```javascript
// yarn add @tatumio/tatum

import { TatumSDK, Xrp, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Xrp>({network: Network.XRP})

const res = await tatum.rpc.accountChannels('rf1BiGeXwwQoi8Z2ueFYTEXSwuJYfV2Jpn', {
  destinationAccount: 'ra5nK24KXen9AHvsdFTKHSANinZseWnPcX',
  ledgerIndex: 'validated',
})

await tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```

### Overview

The `account_channels` RPC method allows you to retrieve information about an account's Payment Channels on the XRP Ledger. This includes only channels where the specified account is the source (or owner) of the channel, not the destination. The information returned is relative to a particular version of the ledger.

Use cases for `account_channels` include:

* Tracking the status of open Payment Channels
* Auditing total outbound XRP from an account via Payment Channels
* Monitoring Payment Channel balances to determine if they need to be topped up

{% embed url="https://codepen.io/tatum-devrel/pen/dyQLjEX" %}

### Parameters

The `account_channels` RPC method includes the following parameters:

* `account`: The unique identifier of an account, typically the account's Address. The request returns channels where this account is the channel's owner/source.
* `destination_account` (Optional): The unique identifier of an account, typically the account's Address. If provided, filter results to payment channels whose destination is this account.
* `ledger_hash` (Optional): A 20-byte hex string for the ledger version to use.
* `ledger_index` (Optional): The ledger index of the ledger to use, or a shortcut string to choose a ledger automatically.
* `limit` (Optional): Limit the number of transactions to retrieve. Cannot be less than 10 or more than 400. The default is 200.
* `marker` (Optional): Value from a previous paginated response. Resume retrieving data where that response left off.

### Return Object

The response to the `account_channels` RPC call includes an array of Channel Objects, each containing the following fields:

* `account` (String): The address of the source/owner of the payment channels. This corresponds to the account field of the request.
* `channels` (Array of Channel Objects): Payment channels owned by this account. Each Channel Object includes:
  * `account` (String): The owner of the channel, as an Address.
  * `amount` (String): The total amount of XRP, in drops allocated to this channel.
  * `balance` (String): The total amount of XRP, in drops, paid out from this channel, as of the ledger version used.
  * `channel_id` (String): A unique ID for this channel, as a 64-character hexadecimal string. This is also the ID of the channel object in the ledger's state data.
  * `destination_account` (String): The destination account of the channel, as an Address. Only this account can receive the XRP in the channel while it is open.
  * `settle_delay` (Unsigned Integer): The number of seconds the payment channel must stay open after the owner of the channel requests to close it.
  * `public_key` (String): May be omitted. The public key for the payment channel in the XRP Ledger's base58 format.
  * `public_key_hex` (String): May be omitted. The public key for the payment channel in hexadecimal format.
  * `expiration` (Unsigned Integer): May be omitted. Time, in seconds since the Ripple Epoch, when this channel is set to expire.
  * `cancel_after` (Unsigned Integer): May be omitted. Time, in seconds since the Ripple Epoch, of this channel's immutable expiration.
  * `source_tag` (Unsigned Integer): May be omitted. A 32-bit unsigned integer to use as a source tag for payments through this payment channel.
  * `destination_tag` (Unsigned Integer): May be omitted. A 32-bit unsigned integer to use as a destination tag for payments through this channel.
* `ledger_hash` (String): May be omitted. The identifying hash of the ledger version used to generate this response.
* `ledger_index` (Number): The ledger index of the ledger version used to generate this response.
* `validated` (Boolean): May be omitted. If true, this data comes from a validated ledger version.
* `limit` (Number): May be omitted. The limit to how many channel objects were actually returned by this request.
* `marker` (Marker): May be omitted. Server-defined value for pagination. Pass this to the next call to resume getting results where this call left off.

### JSON-RPC Request Example

```json
{
    "method": "account_channels",
    "params": [{
        "account": "rf1BiGeXwwQoi8Z2ueFYTEXSwuJYfV2Jpn",
        "destination_account": "ra5nK24KXen9AHvsdFTKHSANinZseWnPcX",
        "ledger_index": "validated"
    }]
}
```

### JSON-RPC Response Example

```json
{
  "result": {
    "account": "rf1BiGeXwwQoi8Z2ueFYTEXSwuJYfV2Jpn",
    "channels": [
      {
        "account": "rf1BiGeXwwQoi8Z2ueFYTEXSwuJYfV2Jpn",
        "amount": "1000",
        "balance": "0",
        "channel_id": "C7F634794B79DB40E87179A9D1BF05D05797AE7E92DF8E93FD6656E8C4BE3AE7",
        "destination_account": "ra5nK24KXen9AHvsdFTKHSANinZseWnPcX",
        "public_key": "aBR7mdD75Ycs8DRhMgQ4EMUEmBArF8SEh1hfjrT2V9DQTLNbJVqw",
        "public_key_hex": "03CFD18E689434F032A4E84C63E2A3A6472D684EAF4FD52CA67742F3E24BAE81B2",
        "settle_delay": 60
      }
    ],
    "ledger_hash": "27F530E5C93ED5C13994812787C1ED073C822BAEC7597964608F2C049C2ACD2D",
    "ledger_index": 71766343,
    "status": "success",
    "validated": true
  }
}
```

Please note, the response may contain an array of channel objects if there are multiple channels associated with the provided account.
