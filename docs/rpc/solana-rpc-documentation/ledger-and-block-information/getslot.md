# getSlot

### How to Use It

{% code overflow="wrap" lineNumbers="true" %}
```javascript
// yarn add @tatumio/tatum

import { TatumSDK, Solana, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Solana>({ network: Network.SOLANA })

const res = await tatum.rpc.getSlot()

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}

### Overview

The `getSlot` method returns the slot that has reached the given or default commitment level. Slots are a fundamental concept in the Solana blockchain, representing the passing of time in the ledger. This method is helpful for tracking the progress of the blockchain and can be used in numerous cases, such as determining the current state of the ledger, or for timekeeping purposes in a DApp.

{% embed url="https://codepen.io/tatum-devrel/pen/gOQEwvZ" %}

### Parameters

* `options` (object, optional): A configuration object containing:
  * `commitment`(string, optional): Specifies the level of commitment to apply when fetching data.
    * Values: `finalized` `confirmed` `processed`
  * `minContextSlot` (number, optional): The minimum slot that the request can be evaluated at.

### Return Object

The method returns an integer, representing the current slot that has reached the given or default commitment level.

### JSON-RPC Request Example

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "getSlot"
}
```

### JSON-RPC Response Example

```json
{
  "jsonrpc": "2.0",
  "result": 1234,
  "id": 1
}
```
