# getLatestBlockhash

### How to Use It

{% code overflow="wrap" lineNumbers="true" %}
```javascript
// yarn add @tatumio/tatum

import { TatumSDK, Solana, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Solana>({ network: Network.SOLANA })

const res = await tatum.rpc.getLatestBlockhash({commitment: 'processed'})

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}

### Overview

The `getLatestBlockhash` method returns the latest blockhash of the ledger. The blockhash is essential for transaction processing to ensure transaction uniqueness and to provide cryptographic security for the ledger. This method is critical in scenarios where the latest blockhash is needed for transaction signing or to confirm the most recent state of the blockchain.

{% embed url="https://codepen.io/tatum-devrel/pen/eYQXdVd?editors=1111" %}

### Parameters

* `options` (object, optional): This object can contain the following fields:
  * `commitment`(string, optional): Specifies the level of commitment to apply when fetching data.
    * Values: `finalized` `confirmed` `processed`
  * `minContextSlot` (number, optional): The minimum slot that the request can be evaluated at.

### Return Object

The method returns a `RpcResponse` JSON object with `value` field set to a JSON object including:

* `blockhash`: The latest blockhash as a base-58 encoded string.
* `lastValidBlockHeight` : The last block height at which the blockhash will be valid.

### JSON-RPC Request Example

```json
{
  "id":1,
  "jsonrpc":"2.0",
  "method":"getLatestBlockhash",
  "params":[
    {
      "commitment":"processed"
    }
  ]
}
```

### JSON-RPC Response Example

```json
{
  "jsonrpc": "2.0",
  "result": {
    "context": {
      "slot": 2792
    },
    "value": {
      "blockhash": "EkSnNWid2cvwEVnVx9aBqawnmiCNiDgp3gUdkDPTKN1N",
      "lastValidBlockHeight": 3090
    }
  },
  "id": 1
}
```
