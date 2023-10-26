# getAccountInfo

### How to use it

{% code overflow="wrap" lineNumbers="true" %}
```javascript
// yarn add @tatumio/tatum

import { TatumSDK, Solana, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Solana>({ network: Network.SOLANA })

const res = await tatum.rpc.getAccountInfo('ChkH4bTk7c5NSGbxvXx89yY2oU7rFJsr3Cq1gPNCCPVe')

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}

### Overview

The `getAccountInfo` RPC method is used to fetch and retrieve specific and detailed information about a particular account on the Solana blockchain. This information includes the current state of the account, its associated data, and the account's current balance.

This method could be used in scenarios where detailed account data is required, for example, to verify transactions, check account balances, or to review the account's history.

{% embed url="https://codepen.io/tatum-devrel/pen/gOQErrY" %}

### Parameters

The `getAccountInfo` method accepts two parameters:

* `accountPubkey`(string, required): The public key of the account for which information is to be fetched.
  * Example: `"ChkH4bTk7c5NSGbxvXx89yY2oU7rFJsr3Cq1gPNCCPVe"`
* `options` (object, optional): Configuration object containing the following fields:
  * `commitment` (string, optional): Specifies the confirmation level of data to be fetched.
    * Values: `finalized` `confirmed` `processed`
  * `encoding` (string, optional): Encoding format for Account data
    * Values: `base58` `base64` `base64+zstd` `jsonParsed`

### Return object

The `getAccountInfo` method returns an object containing the following fields:

* `context`: An object containing details about the context in which the account information was fetched.
  * `slot`: The slot at which the data was fetched.
* `value`: An object containing the account's information.
  * `owner`: The public key of the account's owner.
  * `lamports`: The account's current balance.
  * `data`: data associated with the account, either as encoded binary data or JSON format `{<program>: <state>}` - depending on encoding parameter
  * `executable`: Whether the account is marked as executable.
  * `rentEpoch`: The rent epoch value of the account.
  * `size`: The data size of the account

### JSON-RPC Request Example

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "getAccountInfo",
  "params": [
    "ChkH4bTk7c5NSGbxvXx89yY2oU7rFJsr3Cq1gPNCCPVe",
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
      "owner": "Base58('11111111111111111111111111111111')",
      "lamports": 1000000,
      "data": "Base64('...')",
      "executable": false,
      "rentEpoch": 20,
      "size": 120
    }
  }
}
```
