# getblockheader

### How to use it

{% tabs %}
{% tab title="TypeScript/JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Litecoin, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Litecoin>({network: Network.LITECOIN})

const result = await tatum.rpc.getBlockHeader("0000000000000000001b4fedbfb3672963c37f965686c2bf6350e32e77f9941f", true)

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Overview

`getblockheader` is a Litecoin RPC method that returns information about a specified block header. This method is useful for obtaining a high-level view of a specific block, including its hash, previous block hash, merkle root, timestamp, difficulty target, and nonce, without having to fetch the entire block's contents.

{% embed url="https://codepen.io/tatum-devrel/pen/ExOMPom" %}

### Parameters

*   `blockhash`: The hash of the block for which the header information is requested. This is a string parameter.

    Example: `"`0000000000000000001b4fedbfb3672963c37f965686c2bf6350e32e77f9941f`"`
*   `verbose` (optional): A boolean parameter that specifies whether to return the header information in a JSON object (true) or as a serialized hex-encoded string (false). Default is true.

    Example: `true`

### Return Object

If `verbose` is set to true (default), the return object is a JSON object containing the following fields:

* `hash`: The hash of the block.
* `confirmations`: The number of confirmations for the block.
* `height`: The height of the block in the block chain.
* `version`: The block version.
* `versionHex`: The block version formatted as a hex string.
* `merkleroot`: The merkle root of the block.
* `time`: The block timestamp in UNIX format.
* `mediantime`: The median block time of the last 11 blocks in UNIX timestamp format.
* `nonce`: The nonce value for the block.
* `bits`: The encoded difficulty target for the block.
* `difficulty`: The actual difficulty target for the block as a decimal number.
* `chainwork`: The total work in the block chain up to this block.
* `nTx`: The number of transactions in the block.
* `previousblockhash`: The hash of the previous block.
* `nextblockhash`: The hash of the next block (only present if there is a next block).

If `verbose` is set to false, the return object is a serialized hex-encoded string of the block header.

### JSON Examples

Request example:

{% code overflow="wrap" lineNumbers="true" %}
```json
{
  "jsonrpc": "2.0",
  "method": "getblockheader",
  "params": ["0000000000000000001b4fedbfb3672963c37f965686c2bf6350e32e77f9941f", true],
  "id": 1
}
```
{% endcode %}

Response example:

{% code overflow="wrap" lineNumbers="true" %}
```json
{
    "result": {
        "hash": "0000000000000000001b4fedbfb3672963c37f965686c2bf6350e32e77f9941f",
        "confirmations": 199945,
        "height": 587123,
        "version": 549453824,
        "versionHex": "20c00000",
        "merkleroot": "06bc20da616f96fef435445cbf1bbcc9ff00896dd30c73b875aed7e06902666d",
        "time": 1564152126,
        "mediantime": 1564151358,
        "nonce": 444284193,
        "bits": "171f3a08",
        "difficulty": 9013786945891.682,
        "chainwork": "00000000000000000000000000000000000000000768b223a5622f8f0f1ac0a0",
        "nTx": 1820,
        "previousblockhash": "0000000000000000001683477bc3c17ab029412183952cb4a37f49968e16e6a8",
        "nextblockhash": "00000000000000000007aeb07bc2fe4dbd0b55fc4be751050589b59fe95352fc"
    },
    "error": null,
    "id": 1
}
```
{% endcode %}

\
