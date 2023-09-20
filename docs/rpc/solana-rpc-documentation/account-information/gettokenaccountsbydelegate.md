# getTokenAccountsByDelegate

### How to use it

{% code overflow="wrap" lineNumbers="true" %}
```javascript
// yarn add @tatumio/tatum

import { TatumSDK, Solana, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Solana>({ network: Network.SOLANA })

const delegate = "GgPpTKg78vmzgDtP1DNn72CHAYjRdKY7AV6zgszoHCSa";

const res = await tatum.rpc.getTokenAccountsByDelegate(delegate)

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}

### Overview

The `getTokenAccountsByDelegate` method returns all SPL Token accounts by a specified delegate. This can be useful when you need to retrieve all token accounts associated with a specific delegate address, typically in situations where you are managing or auditing the accounts managed by a particular delegate.

### Parameters

* `delegate` (string, required): Pubkey of account delegate to query, as base-58 encoded string
  * Example: `"GgPpTKg78vmzgDtP1DNn72CHAYjRdKY7AV6zgszoHCSa"`
* `config`(object, optional): An optional object containing either of the following:
  * `mint`(string): Pubkey of the specific token Mint to limit accounts to, as base-58 encoded string
    * Example: `{ mint: 'So11111111111111111111111111111111111111112' }`
  * `programId` (string): Pubkey of the Token program that owns the accounts, as base-58 encoded string
    * Example: `{ programId: 'So11111111111111111111111111111111111111112' }`
* `options` (object, optional): Configuration object containing the following fields:
  * `commitment` (string, optional): Specifies the confirmation level of data to be fetched.
    * Values: `finalized` `confirmed` `processed`
  * `minContextSlot` (number, optional): The minimum slot that the request can be evaluated at
    * Example: `1000`
  * `dataSlice` (object, optional): limit the returned account data using the provided `offset` (number) and `length` (number) fields; only available for `base58`, `base64` or `base64+zstd` encodings.
    * Example: `{ "offset": 0, "length": 100 }`
  * `encoding` (string, optional): The encoding for the account data.
    * Values: `base58` `base64` `base64+zstd` `jsonParsed`

### Return object

The result will be an RpcResponse JSON object with `value` equal to an array of JSON objects, which will contain:

* `pubkey`: Public key of the account.
* `account`: A JSON object, with the following sub fields:
  * `executable`: Whether the account is executable.
  * `owner`: Base-58 encoded Pubkey of the program this account has been assigned to
  * `lamports`: Number of lamports in the account.
  * `data`: Token state data associated with the account, either as encoded binary data or in JSON format `{program: state}`
  * `rentEpoch`: The epoch at which the account will next owe rent.
  * `size`: The data size of the account

### JSON-RPC Request Example

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "getTokenAccountsByDelegate",
  "params": [
    "28YTZEwqtMHWrhWcvv34se7pjS7wctgqzCPB3gReCFKp"
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
        "account": {
          "data": {
            "program": "spl-token",
            "parsed": {
              "info": {
                "tokenAmount": {
                  "amount": "1",
                  "decimals": 1,
                  "uiAmount": 0.1,
                  "uiAmountString": "0.1"
                },
                "delegate": "4Nd1mBQtrMJVYVfKf2PJy9NZUZdTAsp7D4xWLs4gDB4T",
                "delegatedAmount": {
                  "amount": "1",
                  "decimals": 1,
                  "uiAmount": 0.1,
                  "uiAmountString": "0.1"
                },
                "state": "initialized",
                "isNative": false,
                "mint": "3wyAj7Rt1TWVPZVteFJPLa26JmLvdb1CAKEFZm3NY75E",
                "owner": "CnPoSPKXu7wJqxe59Fs72tkBeALovhsCxYeFwPCQH9TD"
              },
              "type": "account"
            },
            "space": 165
          },
          "executable": false,
          "lamports": 1726080,
          "owner": "TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA",
          "rentEpoch": 4,
          "space": 165
        },
        "pubkey": "28YTZEwqtMHWrhWcvv34se7pjS7wctgqzCPB3gReCFKp"
      }
    ]
  },
  "id": 1
}
```
