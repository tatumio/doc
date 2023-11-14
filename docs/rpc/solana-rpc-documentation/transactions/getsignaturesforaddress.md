# getSignaturesForAddress

### How to Use It

{% code overflow="wrap" lineNumbers="true" %}
```javascript
// yarn add @tatumio/tatum

import { TatumSDK, Solana, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Solana>({ network: Network.SOLANA })

const address = 'H8UvHwUaXKmHyr1UzEy1y5F5KjU6kGXMDFddxEjqJ2Sn'
const options = {limit: 10} // optional

const res = await tatum.rpc.getSignaturesForAddress(address, options)

await tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}

### Overview

The `getSignaturesForAddress` method fetches the signatures for confirmed transactions that include the given address in their `accountKeys` list. Returns signatures backwards in time from the provided signature or most recent confirmed block. This is especially useful for tracking the transaction history of an address, auditing transactions, or for debugging purposes.

### Parameters

* `address`(string, required): The address for which to fetch the transaction signatures.
  * Example: `"H8UvHwUaXKmHyr1UzEy1y5F5KjU6kGXMDFddxEjqJ2Sn"`
* `options` (object, optional): Configuration object containing the following fields:
  * `commitment` (string, optional): Specifies the confirmation level of data to be fetched.
    * Values: `finalized` `confirmed` `processed`
  * `minContextSlot` (number, optional): The minimum slot that the request can be evaluated at
    * Example: `1000`
  * `limit`(number, optional): The maximum number of signatures to return (between 1 and 1,000).
    * Example: `10`
  * `before`(string, optional): Start searching backwards from this transaction signature. If not provided the search starts from the top of the highest max confirmed block.
    * Example: `"5Z7dVQaRBAjBjJZVhdJygdAEyRm3N8D1BQot9aJuthFU"`
  * `until`(string, optional): Search until this transaction signature, if found before limit reached
    * Example: `"5Z7dVQaRBAjBjJZVhdJygdAEyRm3N8D1BQot9aJuthFU"`

### Return Object

An array of `<object>`, ordered from **newest** to **oldest** transaction, containing transaction signature information with the following fields:

* `signature`: The transaction's signature as base-58 encoded string.
* `slot`: The slot in which the transaction was processed.
* `err`: Error if transaction failed, null if transaction succeeded.
* `memo:` Memo associated with the transaction, null if no memo is present
* `blockTime:` Estimated production time, as Unix timestamp (seconds since the Unix epoch) of when transaction was processed. null if not available.
* `confirmationStatus:` The transaction's cluster confirmation status; Either `processed`, `confirmed`, or `finalized`.&#x20;

### JSON-RPC Request Example

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "getSignaturesForAddress",
  "params": [
    "Vote111111111111111111111111111111111111111",
    {
      "limit": 1
    }
  ]
}
```

### JSON-RPC Response Example

```json
{
  "jsonrpc": "2.0",
  "result": [
    {
      "err": null,
      "memo": null,
      "signature": "5h6xBEauJ3PK6SWCZ1PGjBvj8vDdWG3KpwATGy1ARAXFSDwt8GFXM7W5Ncn16wmqokgpiKRLuS83KUxyZyv2sUYv",
      "slot": 114,
      "blockTime": null
    }
    // More signatures...
  ],
  "id": 1
}
```
