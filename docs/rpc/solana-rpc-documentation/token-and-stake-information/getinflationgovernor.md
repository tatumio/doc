# getInflationGovernor

### How to Use It

{% code overflow="wrap" lineNumbers="true" %}
```javascript
// yarn add @tatumio/tatum

import { TatumSDK, Solana, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Solana>({ network: Network.SOLANA })

const res = await tatum.rpc.getInflationGovernor()

await tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}

### Overview

The `getInflationGovernor` method is used to retrieve the current inflation governor in the Solana blockchain.

{% embed url="https://codepen.io/tatum-devrel/pen/rNQRMVO?editors=1011" %}

### Parameters

* `options` (object, optional): Configuration object containing the following fields:
  * `commitment`(string, optional): Specifies the level of commitment to apply when fetching data.
    * Values: `finalized` `confirmed` `processed`

### Return Object

The method returns a JSON object with the following fields:

* `initial`: The initial inflation percentage from time 0.
* `terminal`: Terminal inflation percentage.
* `taper`: Rate per year at which inflation is lowered. The rate reduction is derived using the target slot time in the genesis config.
* `foundation`: Percentage of total inflation allocated to the foundation.
* `foundationTerm`: Duration of foundation pool inflation in years.

### JSON-RPC Request Example

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "getInflationGovernor"
}
```

### JSON-RPC Response Example

```json
{
  "jsonrpc": "2.0",
  "result": {
    "foundation": 0.05,
    "foundationTerm": 7,
    "initial": 0.15,
    "taper": 0.15,
    "terminal": 0.015
  },
  "id": 1
}
```
