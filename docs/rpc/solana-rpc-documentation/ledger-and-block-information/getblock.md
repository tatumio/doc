# getBlock

{% code overflow="wrap" lineNumbers="true" %}
```javascript
// yarn add @tatumio/tatum

import { TatumSDK, Solana, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Solana>({ network: Network.SOLANA })

const slotNumber = 430

const config = {
    encoding: "jsonParsed",
    transactionDetails: "full",
    rewards: false,
    maxSupportedTransactionVersion: 0,
}

const res = await tatum.rpc.getBlock(slotNumber, config)

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}

### Overview

The `getBlock` method returns identity and transaction information about a confirmed block in the ledger. It provides detailed data about each transaction within the block, including pre and post transaction balances, transaction status, fees charged, and more.

This method is essential for blockchain explorers or any application that needs to track and represent blockchain transaction data. For instance, it could be used by a wallet application to show transaction details or by a network analytics tool for data gathering and analysis.

{% embed url="https://codepen.io/tatum-devrel/pen/wvQOzGR" %}

### Parameters

This method takes the following parameters:

* `slot` (number, required):  Slot number
* `options` (object, optional): This object can contain the following fields:
  * `commitment`(string, optional): Specifies the level of commitment to apply when fetching data.
    * Values: `finalized` `confirmed` `processed`
  * `encoding` (string, optional): Encoding format for each returned transaction. The default is `json`. Other possible values include: `jsonParsed`, `base58`, `base64`.
  * `transactionDetails` (string, optional): Level of transaction detail to return. The default is `full`. Other possible values include: `accounts`, `signatures`, `none`.
  * `maxSupportedTransactionVersion` (number, optional): The max transaction version to return in responses.
  * `rewards` (bool, optional): Whether to populate the `rewards` array. The default includes rewards.

### Return Object

The method returns a JSON object that includes detailed information about the block and the transactions it contains. If the specified block is not confirmed, the result will be `null`.

The returned JSON object includes the following fields:

* `blockhash`: The blockhash of this block, as base-58 encoded string.
* `previousBlockhash`: The blockhash of this block's parent, as base-58 encoded string. If the parent block is not available due to ledger cleanup, this field will return "11111111111111111111111111111111".
* `parentSlot`: The slot index of this block's parent.
* `transactions`: An array of JSON objects containing detailed transaction information. This field is present if "full" transaction details are requested.
  * `transaction:`  Transaction object, either in JSON format or encoded binary data, depending on encoding parameter
  * `meta:` Transaction status metadata object, containing `null` or:
    * `err:`  Error if transaction failed, null if transaction succeeded. TransactionError definitions
    * `fee:` Fee this transaction was charged, as u64 integer
    * `preBalances:` Array of numbers representing account balances from before the transaction was processed
    * `postBalances:` Array of numbers representing account balances after the transaction was processed
    * `innerInstructions:` List of inner instructions or `null` if inner instruction recording was not enabled during this transaction
    * `preTokenBalances:` List of token balances from before the transaction was processed or omitted if token balance recording was not yet enabled during this transaction
    * `postTokenBalances:` List of token balances from after the transaction was processed or omitted if token balance recording was not yet enabled during this transaction
    * `logMessages:` Array of string log messages or `null` if log message recording was not enabled during this transaction
    * `rewards:` Transaction-level rewards, populated if rewards are requested; an array of JSON objects containing:
      * `pubkey:` The public key, as base-58 encoded string, of the account that received the reward
      * `lamports:` Number of reward lamports credited or debited by the account
      * `postBalance:` Account balance in lamports after the reward was applied
      * `rewardType:` Type of reward: "fee", "rent", "voting", "staking"
      * `commission:` Vote account commission when the reward was credited, only present for voting and staking rewards
      * DEPRECATED: `status:` Transaction status
        * `"Ok":` Transaction was successful
        * `"Err":` Transaction failed with TransactionError
      * `loadedAddresses:` Transaction addresses loaded from address lookup tables. Undefined if `maxSupportedTransactionVersion` is not set in request params.
        * `writable:` Ordered list of base-58 encoded addresses for writable loaded accounts
        * `readonly:`Ordered list of base-58 encoded addresses for readonly loaded accounts
      * `returnData:` The most-recent return data generated by an instruction in the transaction, with the following fields:
        * `programId:` The program that generated the return data, as base-58 encoded Pubkey
        * `data:` The return data itself, as base-64 encoded binary data
      * `computeUnitsConsumed:` Number of compute units consumed by the transaction
  * `version:` Transaction version. Undefined if `maxSupportedTransactionVersion` is not set in request params.
* `signatures`: An array of signatures strings, corresponding to the transaction order in the block. This field is present if "signatures" are requested for transaction details.
* `rewards`: Block-level rewards, present if rewards are requested.
* `blockTime`: Estimated production time, as Unix timestamp (seconds since the Unix epoch).
* `blockHeight`: The number of blocks beneath this block.

### JSON-RPC Request Example

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "getBlock",
  "params": [
    430,
    {
      "encoding": "json",
      "maxSupportedTransactionVersion": 0,
      "transactionDetails": "full",
      "rewards": false
    }
  ]
}
```

### JSON-RPC Response Example

```json
{
  "jsonrpc": "2.0",
  "result": {
    "blockHeight": 428,
    "blockTime": null,
    "blockhash": "3Eq21vXNB5s86c62bVuUfTeaMif1N2kUqRPBmGRJhyTA",
    "parentSlot": 429,
    "previousBlockhash": "mfcyqEXB3DnHXki6KjjmZck6YjmZLvpAByy2fj4nh6B",
    "transactions": [
      {
        "meta": {
          "err": null,
          "fee": 5000,
          "innerInstructions": [],
          "logMessages": [],
          "postBalances": [499998932500, 26858640, 1, 1, 1],
          "postTokenBalances": [],
          "preBalances": [499998937500, 26858640, 1, 1, 1],
          "preTokenBalances": [],
          "rewards": null,
          "status": {
            "Ok": null
          }
        },
        "transaction": {
          "message": {
            "accountKeys": [
              "3UVYmECPPMZSCqWKfENfuoTv51fTDTWicX9xmBD2euKe",
              "AjozzgE83A3x1sHNUR64hfH7zaEBWeMaFuAN9kQgujrc",
              "SysvarS1otHashes111111111111111111111111111",
              "SysvarC1ock11111111111111111111111111111111",
              "Vote111111111111111111111111111111111111111"
            ],
            "header": {
              "numReadonlySignedAccounts": 0,
              "numReadonlyUnsignedAccounts": 3,
              "numRequiredSignatures": 1
            },
            "instructions": [
              {
                "accounts": [1, 2, 3, 0],
                "data": "37u9WtQpcm6ULa3WRQHmj49EPs4if7o9f1jSRVZpm2dvihR9C8jY4NqEwXUbLwx15HBSNcP1",
                "programIdIndex": 4
              }
            ],
            "recentBlockhash": "mfcyqEXB3DnHXki6KjjmZck6YjmZLvpAByy2fj4nh6B"
          },
          "signatures": [
            "2nBhEBYYvfaAe16UMNqRHre4YNSskvuYgx3M6E4JP1oDYvZEJHvoPzyUidNgNX5r9sTyN1J9UxtbCXy2rqYcuyuv"
          ]
        }
      }
    ]
  },
  "id": 1
}js
```
