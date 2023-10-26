# isBlockhashValid

### How to Use It

{% code overflow="wrap" lineNumbers="true" %}
```javascript
// yarn add @tatumio/tatum

import { TatumSDK, Solana, Network, Commitment } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Solana>({ network: Network.SOLANA })

const blockhash = 'J7rBdM6AecPDEZp8aPq5iPSNKVkU5Q76F3oAV4eW5wsW'
const options = {
  commitment: Commitment.Processed,
  minContextSlot: 5
} // optional

const res = await tatum.rpc.isBlockhashValid(blockhash, options)

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}

### Overview

The `isBlockhashValid` method evaluates the validity of a specified blockhash. This can be used to confirm if a blockhash is still valid on the network.

{% embed url="https://codepen.io/tatum-devrel/pen/vYQPKoW" %}

### Parameters

* `blockhash`(string, required): The blockhash of the block to evaluate, as a base-58 encoded string.
  * Example: `'J7rBdM6AecPDEZp8aPq5iPSNKVkU5Q76F3oAV4eW5wsW'`
* `options`: (object, optional) Configuration object containing the following fields:
  * `commitment`: (string, optional) Specifies the level of commitment to apply when fetching data.
    * Values: `finalized` `confirmed` `processed`
  * `minContextSlot`: (number, optional) The minimum slot that the request can be evaluated at.
    * Example: `5`

### Return Object

The return object contains a `bool` value indicating if the blockhash is still valid.

### JSON-RPC Request Example

```json
{
  "id": 45,
  "jsonrpc": "2.0",
  "method": "isBlockhashValid",
  "params": [
    "J7rBdM6AecPDEZp8aPq5iPSNKVkU5Q76F3oAV4eW5wsW", {"commitment":"processed"}
  ]
}
```

### JSON-RPC Response Example

```json
{
  "jsonrpc": "2.0",
  "result": {
    "context": {
      "slot": 2483
    },
    "value": false
  },
  "id": 1
}
```
