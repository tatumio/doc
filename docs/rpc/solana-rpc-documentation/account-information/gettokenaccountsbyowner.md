# getTokenAccountsByOwner

### How to use it

{% code overflow="wrap" lineNumbers="true" %}
```javascript
// yarn add @tatumio/tatum

import { TatumSDK, Solana, Network, Encoding } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Solana>({ network: Network.SOLANA })

const res = await tatum.rpc.getTokenAccountsByOwner(
  'GgPpTKg78vmzgDtP1DNn72CHAYjRdKY7AV6zgszoHCSa',
  {
    mint: '1YDQ35V8g68FGvcT85haHwAXv1U7XMzuc4mZeEXfrjE',
  },
  { encoding: Encoding.JsonParsed }
)

await tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}

### Overview

The `getTokenAccountsByOwner` method retrieves all SPL token accounts owned by a specified address on the Solana blockchain. It allows you to fetch a list of token accounts associated with a particular owner. This method is useful for querying the token holdings of a specific address and performing operations related to token management.

{% embed url="https://codepen.io/tatum-devrel/pen/bGQZpaB" %}

### Parameters

* `ownerAddress` (string, required): The address of the owner for whom to retrieve token accounts.
  * Example: `'rf1BiGeXwwQoi8Z2ueFYTEXSwuJYfV2Jpn'`
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
  "method": "getTokenAccountsByOwner",
  "params": [
    'GgPpTKg78vmzgDtP1DNn72CHAYjRdKY7AV6zgszoHCSa',
    {
      mint: '1YDQ35V8g68FGvcT85haHwAXv1U7XMzuc4mZeEXfrjE',
    },
    { encoding: 'jsonParsed'},
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
              "accountType": "account",
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
                "owner": "4Qkev8aNZcqFNSRhQzwyLMFSsi94jHqE8WNVTJzTP99F"
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
        "pubkey": "C2gJg6tKpQs41PRS1nC8aw3ZKNZK3HQQZGVrDFDup5nx"
      }
    ]
  },
  "id": 1
}
```
