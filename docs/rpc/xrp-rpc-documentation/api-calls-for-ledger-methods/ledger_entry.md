# ledger\_entry

### How to use it

```javascript
// yarn add @tatumio/tatum

import { TatumSDK, Xrp, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Xrp>({network: Network.XRP})

const res = await tatum.rpc.ledgerEntry({
  ledgerIndex: 'validated',
  index: '7DB0788C020F02780A673DC74757F23823FA3014C1866E72CC4CD8B226CD6EF4'
})

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```

In this example, we're initializing the SDK for the XRP network and calling the `ledgerEntry` method with a specific ledger index and object ID.

### Overview

The `ledgerEntry` method of Tatum SDK facilitates interaction with the XRP Ledger. This method allows you to retrieve a single ledger object from the XRP Ledger in its raw format. It is a powerful and flexible tool with numerous use-cases such as obtaining account details, checking the state of an offer, retrieving trust lines, and much more.

This method is comprehensive and can retrieve several different types of data. The specific type of item you wish to retrieve can be selected by passing the appropriate parameters.

{% embed url="https://codepen.io/tatum-devrel/pen/QWJPZmE" %}

### Parameters

The `ledgerEntry` method accepts a parameter of `LedgerEntryOptions` type, which may contain the following fields:

* `index`: the object ID of a single object to retrieve from the ledger, as a 64-character (256-bit) hexadecimal string.
* `accountRoot`: the classic address of the AccountRoot object to retrieve.
* `directory`: the object ID of the directory or an object requiring either `dir_root` or `owner` as a sub-field, plus optionally a `sub_index` sub-field.
* `offer`: the unique object ID to the Offer or an object requiring the sub-fields `account` and `seq` to uniquely identify the offer.
* `rippleState`: an object specifying the RippleState (trust line) object to retrieve, with the `accounts` and `currency` sub-fields required.
* `check`: the object ID of a Check object to retrieve.
* `escrow`: the object ID of the Escrow or an object requiring `owner` and `seq` sub-fields.
* `paymentChannel`: the object ID of a PayChannel object to retrieve.
* `depositPreauth`: the object ID of the DepositPreauth object or an object requiring `owner` and `authorized` sub-fields.
* `ticket`: the object ID of the Ticket or an object requiring `account` and `ticket_seq` sub-fields.
* `nftPage`: the object ID of an NFT Page to retrieve.

### Return Object

The `ledger_entry` response provides information about a specific ledger object and follows the standard format. A successful result contains the following fields:

* `index`: A string representing the unique ID of the ledger object.
* `ledger_index`: An unsigned integer representing the ledger index of the ledger that was used when retrieving this data.
* `node`: An object containing the data of the ledger object, according to the ledger format. This field is omitted if the "binary": true parameter is specified.
* `node_binary`: A string representing the binary representation of the ledger object in hexadecimal format. This field is included only if the "binary": true parameter is specified.

### JSON-RPC Request Example

```json
{
  "method": "ledger_entry",
  "params": [
    {
      "index": "7DB0788C020F02780A673DC74757F23823FA3014C1866E72CC4CD8B226CD6EF4",
      "ledger_index": "validated"
    }
  ]
}
```

In this example, we're requesting a ledger entry for a particular object ID and using the 'validated' ledger index.

### JSON-RPC Response Example

```json
{
  "result": {
    "ledger_index": 464,
    "nft_page": "7DB0788C020F02780A673DC74757F23823FA3014C1866E72CC4CD8B226CD6EF4",
    "ledger_index": "validated"
  }]
}
```
