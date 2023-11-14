# getMultipleAccounts

### How to use it

{% code overflow="wrap" lineNumbers="true" %}
```javascript
// yarn add @tatumio/tatum

import { TatumSDK, Solana, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Solana>({ network: Network.SOLANA })

const accounts = [
    "GPHrLJNBeFDkHEChoN6CyHFLroen7jVU3HBmJQXvqGQa",
    "4DBehwe4U1gHaE575LZVnjN1MfyPSyWjidadRJoQcyAR",
  ];

const res = await tatum.rpc.getMultipleAccounts(accounts)

await tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}

### Overview

The `getMultipleAccounts` RPC method fetches information about multiple accounts. This is handy when you need to retrieve data about multiple accounts simultaneously, such as for a portfolio management application or a multi-account wallet.

{% embed url="https://codepen.io/tatum-devrel/pen/xxQBVOJ?editors=1011" %}

### Parameters

The `getMultipleAccounts` method accepts an array of public keys and an optional `GetMultipleAccountsOptions` object:

* `publicKeys`(array of strings, required): An array of public keys of the accounts to be fetched.
  * Example: `["accountPubkey1", "accountPubkey2"]`
* `options` (object, optional): Configuration object containing the following fields:
  * `commitment` (string, optional): Specifies the confirmation level of data to be fetched.
    * Values: `finalized` `confirmed` `processed`
  * `minContextSlot` (number, optional): The minimum slot to include in the response.
    * Example: `1000`
  * `dataSlice` (object, optional): The range of data to include in the response.
    * `offset` (number, optional): The starting index of the data slice.
      * Example: `0`
    * `length` (number, optional): The length of the data slice.
      * Example: `100`
  * `encoding` (string, optional): The encoding for the account data.
    * Values: `base58` `base64` `base64+zstd` `jsonParsed`

### Return object

The result will be a JSON object with `value` equal to an array of:

* `null` - if the account at that Pubkey doesn't exist, or
* `object` - a JSON object containing:
  * `data`: `[string, encoding]|object` - data associated with the account, either as encoded binary data or JSON format `{program: state}` - depending on encoding parameter
  * `executable`: A boolean indicating whether the account is executable.
  * `lamports`: The current balance of the account, in lamports.
  * `owner`: The public key of the account's owner.
  * `rentEpoch:`The epoch at which this account will next owe rent, as u64
  * `size:`The data size of the account

### JSON-RPC Request Example

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "getMultipleAccounts",
  "params": [
    ["accountPubkey1", "accountPubkey2"],
    {
      "commitment": "finalized",
      "minContextSlot": 1000,
      "dataSlice": { "offset": 0, "length": 100 },
      "encoding": "base64"
    }
  ]
}
```

### JSON-RPC Response Example

```json
{
   "jsonrpc":"2.0",
   "id":1,
   "result":{
      "context":{
         "slot":123456
      },
      "value":[
         {
            "owner": "Base58('11111111111111111111111111111111')",
            "lamports": 1000000,
            "data": "Base64('...')",
            "executable": false,
            "rentEpoch": 20,
            "size": 120
         },
         {
            "owner": "Base58('11111111111111111111111111111111')",
            "lamports": 1000000,
            "data": "Base64('...')",
            "executable": false,
            "rentEpoch": 20,
            "size": 120
         }
      ]
   }
}
```
