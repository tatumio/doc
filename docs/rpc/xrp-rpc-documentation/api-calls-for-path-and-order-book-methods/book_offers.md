# book\_offers

### How to use it

<pre class="language-javascript"><code class="lang-javascript">// yarn add @tatumio/tatum
<strong>
</strong><strong>import { TatumSDK, Xrp, Network } from '@tatumio/tatum'
</strong>
const tatum = await TatumSDK.init&#x3C;Xrp>({network: Network.XRP})

const takerGets = { currency: 'XRP' }
const takerPays = { currency: 'USD', issuer: 'rvYAfWj5gh67oV6fW32ZzP3Aw4Eubs59B' }

const res = await tatum.rpc.bookOffers(takerGets, takerPays, { taker: 'r9cZA1mLK5R5Am25ArfXFmqgNwjZgnfk59', limit: 10 })

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
</code></pre>

### Overview

The `book_offers` method is used to fetch a list of offers between two different currencies on the XRP Ledger. This method is crucial for trading and asset management applications as it provides an in-depth view of the market depth for a specific trading pair.

{% embed url="https://codepen.io/tatum-devrel/pen/NWEmELX" %}

### Parameters

* `takerGets` (Object): The asset the account taking the offer would receive, as a currency without an amount.
* `takerPays` (Object): The asset the account taking the offer would pay, as a currency without an amount.
* `options` (BookOffersOptions): Optional parameters which includes ledger details, pagination, and the taker address.

### Return Object

The `book_offers` method returns an object that provides information about a list of offers in the order book. The object contains the following fields:

* `ledger_current_index`: (Omitted if `ledger_index` is provided) A ledger index that represents the ledger index of the current in-progress ledger version, which was used to retrieve this information.
* `ledger_index`: (Omitted if `ledger_current_index` is provided) A ledger index that represents the ledger index of the ledger version that was used when retrieving this data, as requested.
* `ledger_hash`: (May be omitted) A hash that represents the identifying hash of the ledger version that was used when retrieving this data, as requested.
* `offers`: An array of offer objects, each of which has the fields of an Offer object.

Each offer object in the `offers` array can include the following fields:

* `owner_funds`: A string that represents the amount of the `TakerGets` currency the side placing the offer has available to be traded. (XRP is represented as drops; any other currency is represented as a decimal value.) If a trader has multiple offers in the same book, only the highest-ranked offer includes this field.
* `taker_gets_funded`: (Only included in partially-funded offers) A currency amount that represents the maximum amount of currency that the taker can get, given the funding status of the offer.
* `taker_pays_funded`: (Only included in partially-funded offers) A currency amount that represents the maximum amount of currency that the taker would pay, given the funding status of the offer.
* `quality`: A string that represents the exchange rate, as the ratio of `taker_pays` divided by `taker_gets`. For fairness, offers that have the same quality are automatically taken first-in, first-out. (In other words, if multiple people offer to exchange currency at the same rate, the oldest offer is taken first.)

### JSON-RPC Request Example

```json
{
    "method": "book_offers",
    "params": [
        {
            "taker": "r9cZA1mLK5R5Am25ArfXFmqgNwjZgnfk59",
            "taker_gets": {
                "currency": "XRP"
            },
            "taker_pays": {
                "currency": "USD",
                "issuer": "rvYAfWj5gh67oV6fW32ZzP3Aw4Eubs59B"
            },
            "limit": 10
        }
    ]
}
```

### JSON-RPC Response Example

```json
{
    "result": {
        "ledger_current_index": 8696243,
        "offers": [],
        "status": "success",
        "validated": false
    }
}
```
