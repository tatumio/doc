# getchaintips

### How to use it

{% tabs %}
{% tab title="TypeScript/JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Litecoin, Network } from '@tatumio/tatums'

const tatum = await TatumSDK.init<Litecoin>({network: Network.LITECOIN})

const result = await tatum.rpc.getChainTips()

await tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Overview

`getchaintips` is a Litecoin RPC method that returns information about all known tips in the block tree. This method is useful for identifying and analyzing potential forks or alternative chains in the Litecoin network. It can be used to monitor the health and status of the network or to investigate discrepancies in blockchain data.

{% embed url="https://codepen.io/tatum-devrel/pen/mdQoVpz" %}

### Parameters

This method does not require any parameters.

### Return Object

The return object is an array of JSON objects, with each object representing a chain tip. The fields in each object are:

* `height`: The height of the chain tip in the block chain.
* `hash`: The hash of the block corresponding to the chain tip.
* `branchlen`: The length of the branch connected to the main chain.
* `status`: The status of the chain tip, which can be one of the following values:
  * `active`: The tip is part of the main chain.
  * `valid-fork`: The tip is part of a valid but inactive fork.
  * `valid-headers`: The tip is part of a valid fork but with incomplete block data.
  * `headers-only`: The tip is a fork with valid headers but incomplete block data and an invalid parent block.
  * `invalid`: The tip is part of an invalid fork.
  * `unknown`: The tip has an unknown validation state.

### JSON Examples

Request example:

{% code overflow="wrap" lineNumbers="true" %}
```json
{
  "jsonrpc": "2.0",
  "method": "getchaintips",
  "id": 1
}
```
{% endcode %}

Response example:

{% code overflow="wrap" lineNumbers="true" %}
```json
{
    "result": [
        {
            "height": 787067,
            "hash": "0000000000000000000348522f4f24304bfcadece8b34c0696faa4f87ec4fdc4",
            "branchlen": 0,
            "status": "active"
        },
        {
            "height": 784121,
            "hash": "000000000000000000046a2698233ed93bb5e74ba7d2146a68ddb0c2504c980d",
            "branchlen": 1,
            "status": "invalid"
        },
        {
            "height": 783830,
            "hash": "0000000000000000000366d2c12772a350f507879a5325203424e58ec440249b",
            "branchlen": 1,
            "status": "valid-headers"
        },
        {
            "height": 783478,
            "hash": "0000000000000000000446f7d3093688ae697386fed3f52a63812678ea6b251d",
            "branchlen": 1,
            "status": "valid-headers"
        },
        {
            "height": 783426,
            "hash": "00000000000000000002ec935e245f8ae70fc68cc828f05bf4cfa002668599e4",
            "branchlen": 1,
            "status": "invalid"
        },
        {
            "height": 782333,
            "hash": "00000000000000000001a1abda3a2eb4acc211f64f8748d1a7635aad80690b7a",
            "branchlen": 1,
            "status": "valid-headers"
        },
        {
            "height": 782129,
            "hash": "000000000000000000036f461ab63c78f08401d3907a67fd2237166d8a373193",
            "branchlen": 1,
            "status": "valid-headers"
        },
        {
            "height": 781487,
            "hash": "0000000000000000000125e5d7c0d2e1b83982e5284ea21e08f5a73b8109d41b",
            "branchlen": 1,
            "status": "valid-fork"
        },
        {
            "height": 781277,
            "hash": "0000000000000000000388f42000fa901c01f2bfae36042bbae133ee430e6485",
            "branchlen": 1,
            "status": "valid-fork"
        },
        {
            "height": 780994,
            "hash": "00000000000000000001b666391fe81859e96fdfdbb83f1a1eafb7951c738c77",
            "branchlen": 1,
            "status": "valid-headers"
        },
        {
            "height": 777172,
            "hash": "0000000000000000000215ac1b6fd564d8d4707631f6b77273521eb1e242cf28",
            "branchlen": 1,
            "status": "valid-headers"
        },
        {
            "height": 776941,
            "hash": "00000000000000000004cc87382e38118248ec926716565d50d63f0637c22c07",
            "branchlen": 1,
            "status": "valid-headers"
        },
        {
            "height": 772981,
            "hash": "0000000000000000000682990a0dae862b48e0451d619938215dd47ed9560200",
            "branchlen": 1,
            "status": "valid-headers"
        },
        {
            "height": 771745,
            "hash": "00000000000000000004370a77a30add64bba97c26a90ca9643b45a75219b2a6",
            "branchlen": 1,
            "status": "valid-headers"
        },
        {
            "height": 771627,
            "hash": "00000000000000000005a92bdb6f9d55ea8d2b42579e0db6ca7764f97b6910e1",
            "branchlen": 1,
            "status": "valid-headers"
        },
        {
            "height": 763445,
            "hash": "000000000000000000065d0f6847466feeeaffa9663895cedde33aa12c262e00",
            "branchlen": 1,
            "status": "valid-headers"
        },
        {
            "height": 759781,
            "hash": "000000000000000000025edbf5ea025e4af2674b318ba82206f70681d97ca162",
            "branchlen": 1,
            "status": "valid-fork"
        },
        {
            "height": 741082,
            "hash": "00000000000000000004e2891d08337eb9263b703eb1c897e05dc59e8b246a9b",
            "branchlen": 1,
            "status": "headers-only"
        },
        {
            "height": 737096,
            "hash": "00000000000000000002b07a9a9f066d463844960542d96e88b4815e063fab08",
            "branchlen": 1,
            "status": "headers-only"
        },
        {
            "height": 733430,
            "hash": "00000000000000000006ead1cff09f279f7beb31a7290c2a603b0776d98dc334",
            "branchlen": 1,
            "status": "valid-headers"
        },
        {
            "height": 730848,
            "hash": "000000000000000000029ec31578132d01696910f299f8d104f29b8f8bbdc24f",
            "branchlen": 1,
            "status": "valid-headers"
        },
        {
            "height": 723102,
            "hash": "00000000000000000006a970fdd8e537521747aff917d909bf3a78b4b68143e1",
            "branchlen": 1,
            "status": "valid-headers"
        },
        {
            "height": 715276,
            "hash": "00000000000000000009b160476c5f407ccd4957e20346b862d8fc46004759f0",
            "branchlen": 1,
            "status": "valid-headers"
        },
        {
            "height": 715139,
            "hash": "0000000000000000000407bc4e26035c137869cdb677dfcab268b3faf7d7b5d1",
            "branchlen": 1,
            "status": "headers-only"
        },
        {
            "height": 714637,
            "hash": "00000000000000000009f819d004fea5bcb77bda25f4906d0a39e79c9ba19590",
            "branchlen": 1,
            "status": "valid-fork"
        },
        {
            "height": 714367,
            "hash": "0000000000000000000b2e70d7675bc7b4e89d384d0e6e1a7ecc2779e1d93244",
            "branchlen": 1,
            "status": "valid-headers"
        }
    ],
    "error": null,
    "id": 1
}
```
{% endcode %}

\
