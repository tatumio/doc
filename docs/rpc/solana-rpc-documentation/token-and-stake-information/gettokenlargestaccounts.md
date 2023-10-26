# getTokenLargestAccounts

### How to Use It

{% code overflow="wrap" lineNumbers="true" %}
```javascript
// yarn add @tatumio/tatum

import { TatumSDK, Solana, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Solana>({ network: Network.SOLANA })

const res = await tatum.rpc.getTokenLargestAccounts()

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}

### Overview

The `getTokenLargestAccounts` method is a valuable resource for analyzing the distribution of a particular SPL (Solana Program Library) Token in the network. This method returns the 20 largest accounts of a specific SPL Token type.

The primary use case for this method is to gain insights into the distribution of a particular token. For instance, token issuers might want to monitor the distribution of their tokens and identify the largest holders.

Another use case is for research and analysis purposes. Data providers, exchange platforms, or individuals might use this information to study market behavior, make predictions, or develop trading strategies based on the ownership concentration of a specific token.

### Parameters

This method takes the following parameters:

* `pubkey` (string, required): A string that represents the Pubkey of the token Mint to query, as base-58 encoded string.
* A configuration object (optional): This object can contain the following fields:
  * `commitment` (string, optional): Specifies the level of commitment to apply when fetching data.
    * Values: `finalized` `confirmed` `processed`

### Return Object

The result will be an RpcResponse JSON object with `value` equal to an array of JSON objects containing:

* `address`: The address of the token account.
* `amount`: The raw token account balance without decimals, a string representation of u64.
* `decimals`: The number of base 10 digits to the right of the decimal place.
* `uiAmount`: The token account balance, using mint-prescribed decimals. Note: This field is deprecated.
* `uiAmountString`: The token account balance as a string, using mint-prescribed decimals.

### JSON-RPC Request Example

```json
{
  "jsonrpc": "2.0", 
  "id": 1,
  "method": "getTokenLargestAccounts",
  "params": [
    "3wyAj7Rt1TWVPZVteFJPLa26JmLvdb1CAKEFZm3NY75E"
  ]
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
    "value": [
      {
        "address": "FYjHNoFtSQ5uijKrZFyYAxvEr87hsKXkXcxkcmkBAf4r",
        "amount": "771",
        "decimals": 2,
        "uiAmount": 7.71,
        "uiAmountString": "7.71"
      },
      {
        "address": "BnsywxTcaYeNUtzrPxQUvzAWxfzZe3ZLUJ4wMMuLESnu",
        "amount": "229",
        "decimals": 2,
        "uiAmount": 2.29,
        "uiAmountString": "2.29"
      }
    ]
  },
  "id": 1
}
```
