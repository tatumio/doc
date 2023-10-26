# getProgramAccounts

### How to use it

{% code overflow="wrap" lineNumbers="true" %}
```javascript
// yarn add @tatumio/tatum

import { TatumSDK, Solana, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Solana>({ network: Network.SOLANA })

const res = await tatum.rpc.getProgramAccounts('BPFLoaderUpgradeab1e11111111111111111111111')

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}

### Overview

The `getProgramAccounts` RPC method retrieves all accounts owned by a specific program on the Solana blockchain. This method can be useful when monitoring the state of a program or tracking the accounts associated with a particular smart contract.

Currently pagination is not supported. Requests to `getProgramAccounts` should include the `dataSlice` and/or `filters` parameters to improve response time and return only intended results.

### Parameters

The `getProgramAccounts` method accepts a program ID and an optional object:

* `programId`(string, required): Pubkey of program, as base-58 encoded string
  * Example: `"BPFLoaderUpgradeab1e11111111111111111111111"`
* `options` (object, optional): Configuration object containing the following fields:
  * `commitment` (string, optional): Specifies the confirmation level of data to be fetched.
    * Values: `finalized` `confirmed` `processed`
  * `minContextSlot` (number, optional): The minimum slot that the request can be evaluated at
    * Example: `123456`
  * `withContext` (boolean, optional): Whether to wrap the result in an RpcResponse JSON object
    * Example: `true`
  * `encoding` (string, optional): The encoding format for the returned Account data
    * Example: `base58` `base64` `base64+zstd` `jsonParsed`
  * `dataSlice` (object, optional): Limit the returned account data using the provided \`offset: number\` and \`length: number\` fields;
    * only available for "base58", "base64" or "base64+zstd" encodings.
    * Example: `{ offset: 0, length: 100 }`
  * `filters` (array, optional): An array of filter objects to filter the accounts based on certain conditions.
    * Example: `[{ memcmp: { offset: 0, bytes: "base64" } }`

### Return object

The `getProgramAccounts` method returns an array of objects, each containing the following fields:

* `pubkey`: The public key of the account.
* `account`: An object containing:
  * `data`: The account's data, encoded according to the requested format.
  * `executable`: Whether the account is executable.
  * `lamports`: The account's current balance.
  * `owner`: The account's owner public key.
  * `rentEpoch`: The epoch at which the account will owe rent again.
  * `size`: The data size of the account

If `withContext` is set to true, the response will also include a `context` object:

* `context`: An object containing details about the context in which the data was fetched.
  * `slot`: The slot at which the data was fetched.

### JSON-RPC Request Example

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "getProgramAccounts",
  "params": [
    "BPFLoaderUpgradeab1e11111111111111111111111",
    {
      "commitment": "finalized",
      "minContextSlot": 123456,
      "withContext": true,
      "encoding": "base64",
      "dataSlice": { "offset": 0, "length": 100 },
      "filters": [{ "memcmp": { "offset": 0, "bytes": "base64" } }]
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
    "value": [
      {
        "pubkey": "9ehXDD5bnhSpFVRf99veikjgq8VajtRH7e3D9aVPLqYd",
        "account": {
          "data": "base64 encoded data",
          "executable": false,
          "lamports": 10000,
          "owner": "BPFLoaderUpgradeab1e11111111111111111111111",
          "rentEpoch": 10
          "size": 120
        }
      }
      //... more accounts
    ]
  }
}
```
