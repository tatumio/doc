# getMinimumBalanceForRentExemption

### How to Use It

{% code overflow="wrap" lineNumbers="true" %}
```javascript
// yarn add @tatumio/tatum

import { TatumSDK, Solana, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Solana>({ network: Network.SOLANA })

const res = await tatum.rpc.getMinimumBalanceForRentExemption(50)

await tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}

### Overview

The `getMinimumBalanceForRentExemption` method returns the minimum balance required to make an account rent exempt. This is useful when setting up a new account or assessing the cost of maintaining an account in a rent-free state.

{% embed url="https://codepen.io/tatum-devrel/pen/xxQBEMp" %}

### Parameters

* `dataSize` (number, optional): The account's data length.
* `options` (object, optional): A configuration object containing:
  * `commitment`(string, optional): Specifies the level of commitment to apply when fetching data.
    * Values: `finalized` `confirmed` `processed`

### Return Object

The result field will be a number indicating the minimum lamports required in the account to remain rent free.

### JSON-RPC Request Example

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "getMinimumBalanceForRentExemption",
  "params": [50]
}
```

### JSON-RPC Response Example

```json
{
  "jsonrpc": "2.0",
  "result": 500,
  "id": 1
}
```
