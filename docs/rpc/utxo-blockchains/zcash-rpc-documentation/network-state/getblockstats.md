# getblockstats

### How to use it

{% tabs %}
{% tab title="TypeScript/JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, ZCash, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<ZCash>({network: Network.ZCASH})

const result = await tatum.rpc.getBlockStats("0000000000000000001b4fedbfb3672963c37f965686c2bf6350e32e77f9941f")

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Overview

`getblockstats` is a method that returns various statistics about a specified block. This method is useful for obtaining detailed information about a block, including the number of transactions, transaction volume, fees, and other related data. The results can be used for data analysis, monitoring, and understanding the state of the network at a specific block height.

{% embed url="https://codepen.io/tatum-devrel/pen/ExOrMba" %}
Try this function
{% endembed %}

### Parameters

*   `hash_or_height`: The block hash or block height for which the statistics are requested. This parameter can be either a string (block hash) or an integer (block height).

    Example (block hash): `"0000000000000000000f92fb968a8d1a2a9c2039e6e99f8c7a0ee3421a44a7d6"`

    Example (block height): `685230`
*   `stats` (optional): An array of strings indicating the statistics to be included in the response. If not specified, all available statistics will be returned.

    Example: `["txs", "avgfee"]`

### Return Object

The return object is a JSON object containing the requested statistics as key-value pairs. The available statistics are:

* `avgfee`: The average transaction fee in satoshis.
* `avgfeerate`: The average fee rate in satoshis per virtual byte.
* `avgtxsize`: The average transaction size in bytes.
* `blockhash`: The hash of the block.
* `height`: The height of the block in the block chain.
* `ins`: The total number of inputs in all transactions.
* `maxfee`: The maximum transaction fee in satoshis.
* `maxfeerate`: The maximum fee rate in satoshis per virtual byte.
* `maxtxsize`: The maximum transaction size in bytes.
* `medianfee`: The median transaction fee in satoshis.
* `mediantime`: The median time for the block in UNIX timestamp format.
* `mediantxsize`: The median transaction size in bytes.
* `minfee`: The minimum transaction fee in satoshis.
* `minfeerate`: The minimum fee rate in satoshis per virtual byte.
* `mintxsize`: The minimum transaction size in bytes.
* `outs`: The total number of outputs in all transactions.
* `subsidy`: The block reward in satoshis.
* `swtotal_size`: The total size of all SegWit transactions in bytes.
* `swtotal_weight`: The total weight of all SegWit transactions.
* `swtxs`: The total number of SegWit transactions.
* `time`: The block timestamp in UNIX format.
* `total_size`: The total size of all transactions in bytes.
* `total_weight`: The total weight of all transactions.
* `totalfee`: The total transaction fees in satoshis.
* `txs`: The total number of transactions in the block.
* `utxo_increase`: The increase in the number of unspent transaction outputs.
* `utxo_size_inc`: The increase in the size of the UTXO set.

### JSON Examples

Request example:

{% code overflow="wrap" lineNumbers="true" %}
```json
{
  "jsonrpc": "2.0",
  "method": "getblockstats",
  "params": ["0000000000000000001b4fedbfb3672963c37f965686c2bf6350e32e77f9941f"],
  "id": 1
}
```
{% endcode %}

Response example:

{% code overflow="wrap" lineNumbers="true" %}
```json
{
    "result": {
        "avgfee": 10220,
        "avgfeerate": 18,
        "avgtxsize": 619,
        "blockhash": "0000000000000000001b4fedbfb3672963c37f965686c2bf6350e32e77f9941f",
        "feerate_percentiles": [
            6,
            9,
            9,
            15,
            48
        ],
        "height": 587123,
        "ins": 3615,
        "maxfee": 419448,
        "maxfeerate": 393,
        "maxtxsize": 17196,
        "medianfee": 9528,
        "mediantime": 1564151358,
        "mediantxsize": 374,
        "minfee": 136,
        "minfeerate": 1,
        "mintxsize": 189,
        "outs": 3617,
        "subsidy": 1250000000,
        "swtotal_size": 323742,
        "swtotal_weight": 777804,
        "swtxs": 616,
        "time": 1564152126,
        "total_out": 342467209172,
        "total_size": 1127251,
        "total_weight": 3991840,
        "totalfee": 18590521,
        "txs": 1820,
        "utxo_increase": 2,
        "utxo_size_inc": 4000
    },
    "error": null,
    "id": 1
}
```
{% endcode %}

\
