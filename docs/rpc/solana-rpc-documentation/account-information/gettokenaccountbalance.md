# getTokenAccountBalance

### How to use it

{% code overflow="wrap" lineNumbers="true" %}
```javascript
// yarn add @tatumio/tatum

import { TatumSDK, Solana, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Solana>({ network: Network.SOLANA })

const res = await tatum.rpc.getTokenAccountBalance('DhzDoryP2a4rMK2bcWwJxrE2uW6ir81ES8ZwJJPPpxDN')

await tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}

### Overview

The `getTokenAccountBalance` method provides the ability to fetch the current balance of a given SPL Token account. It is used when you want to know the amount of tokens held in a specific token account. The token account is specified by its public key.

{% embed url="https://codepen.io/tatum-devrel/pen/KKrEzqq" %}

### Parameters

This method accepts two parameters:

* `pubkey` (string, required): Pubkey of Token account to query, as base-58 encoded string
  * Example: `"DhzDoryP2a4rMK2bcWwJxrE2uW6ir81ES8ZwJJPPpxDN"`
* `options` (object, optional): Configuration object containing the following fields:
  * `commitment` (string, optional): Specifies the confirmation level of data to be fetched.
    * Values: `finalized` `confirmed` `processed`

### Return object

The `getTokenAccountBalance` method returns an object containing the following fields:

* `value`: An object containing:
  * `amount`: The raw balance without decimals, a string representation of number
  * `decimals`: Number of base 10 digits to the right of the decimal place
  * `uiAmount`: Number or null. The balance, using mint-prescribed decimals **DEPRECATED**
  * `uiAmountString`: The balance as a string, using mint-prescribed decimals

If `withContext` is set to true, the response will also include a `context` object:

* `context`: An object containing details about the context in which the data was fetched.
  * `slot`: The slot at which the data was fetched.

### JSON-RPC Request Example

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "getTokenAccountBalance",
  "params": [
    "rf1BiGeXwwQoi8Z2ueFYTEXSwuJYfV2Jpn",
    {
      "commitment": "finalized",
      "encoding": "base64"
    }
  ]
}
```

### JSON-RPC Response Example

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": {
    "context": {
      "slot": 123456
    },
    "value": {
      "amount": "10000",
      "decimals": 6,
      "uiAmount": 0.01,
      "uiAmountString": "0.01"
    }
  }
}
```
