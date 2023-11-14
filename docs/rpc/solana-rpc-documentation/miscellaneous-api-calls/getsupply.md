# getSupply

{% code overflow="wrap" lineNumbers="true" %}
```javascript
// yarn add @tatumio/tatum

import { TatumSDK, Solana, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Solana>({ network: Network.SOLANA })

const res = await tatum.rpc.getSupply()

await tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}

### Overview

The `getSupply` method returns information about the current supply of lamports in the Solana network. It provides insights into the distribution of lamports, such as the total supply, the amount in circulation, and the amount that is not circulating. This can be useful for anyone interested in the macroeconomics of the Solana network or in tracking the circulation of lamports over time.

{% embed url="https://codepen.io/tatum-devrel/pen/QWJoKoj?editors=1011" %}

### Parameters

* `options` (object, optional): A configuration object containing:
  * `commitment`(string, optional): Specifies the level of commitment to apply when fetching data.
  * `excludeNonCirculatingAccountsList` (bool, optional): If true, the returned array of non-circulating accounts will be empty.

### Return Object

The result field will be a JSON object containing:

* `total`: Total supply in lamports.
* `circulating`: Circulating supply in lamports.
* `nonCirculating`: Non-circulating supply in lamports.
* `nonCirculatingAccounts`: An array of account addresses of non-circulating accounts, as strings. If `excludeNonCirculatingAccountsList` is enabled, the returned array will be empty.

### JSON-RPC Request Example

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "getSupply"
}
```

### JSON-RPC Response Example

```json
{
  "jsonrpc": "2.0",
  "result": {
    "context": {
      "slot": 1114
    },
    "value": {
      "circulating": 16000,
      "nonCirculating": 1000000,
      "nonCirculatingAccounts": [
        "FEy8pTbP5fEoqMV1GdTz83byuA8EKByqYat1PKDgVAq5",
        "9huDUZfxoJ7wGMTffUE7vh1xePqef7gyrLJu9NApncqA",
        "3mi1GmwEE3zo2jmfDuzvjSX9ovRXsDUKHvsntpkhuLJ9",
        "BYxEJTDerkaRWBem3XgnVcdhppktBXa2HbkHPKj2Ui4Z"
      ],
      "total": 1016000
    }
  },
  "id": 1
}
```
