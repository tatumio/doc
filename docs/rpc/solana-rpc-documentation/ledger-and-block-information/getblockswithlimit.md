# getBlocksWithLimit

### How to Use It

{% code overflow="wrap" lineNumbers="true" %}
```javascript
// yarn add @tatumio/tatum

import { TatumSDK, Solana, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Solana>({ network: Network.SOLANA })

const res = await tatum.rpc.getBlocksWithLimit(5, 3)

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}

### Overview

The `getBlocksWithLimit` method returns a list of confirmed blocks starting at a given slot and up to a specified limit. This can be helpful when you need to retrieve a specific number of recent blocks for transaction analysis or blockchain data verification purposes.

### Parameters

This method requires and optionally accepts the following parameters:

* `startSlot` (number, required): This is the slot from which the method will start returning blocks.
* `limit` (number, optional): This is the number of blocks to be returned starting from the `startSlot`. If not provided, the method will return all blocks from the `startSlot` to the end of the blockchain. Note that `limit` must be no more than 500,000 blocks higher than the `startSlot`.
* `options` (object, optional): This object can contain the following fields:
  * `commitment`(string, optional): Specifies the level of commitment to apply when fetching data.
    * Values: `finalized` `confirmed` Note that `processed` is not supported.

### Return Object

The method returns an array of integers, each representing a confirmed block starting from the `startSlot` and up to the `limit` blocks, inclusive.

### JSON-RPC Request Example

```json
{
  "jsonrpc": "2.0",
  "id":1,
  "method":"getBlocksWithLimit",
  "params":[5, 3]
}
```

### JSON-RPC Response Example

```json
{
  "jsonrpc": "2.0",
  "result": [5, 6, 7],
  "id": 1
}
```
