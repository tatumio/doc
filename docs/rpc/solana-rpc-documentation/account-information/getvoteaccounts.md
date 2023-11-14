# getVoteAccounts

### How to use it

{% code overflow="wrap" lineNumbers="true" %}
```javascript
// yarn add @tatumio/tatum

import { TatumSDK, Solana, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Solana>({ network: Network.SOLANA })

const res = await tatum.rpc.getVoteAccounts({ votePubkey: 'beefKGBWeSpHzYBHZXwp5So7wdQGX6mu4ZHCsH3uTar' })

await tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}

{% embed url="https://codepen.io/tatum-devrel/pen/rNQReoZ" %}

### Overview

The `getVoteAccounts` method is used to fetch the current list of vote accounts and their associated stake in the network. This is particularly useful when you want to understand the current validators in the Solana network and their voting records. It can be used in situations where you need to analyse the active participation in the network's consensus protocol.

### Parameters

* `options` (object, optional): Configuration object containing the following fields:
  * `commitment`(string, optional): Specifies the confirmation level of data to be fetched.
    * Example: `"confirmed"`
  * `votePubkey` (string, optional): Specifies the public key of the vote account to fetch.
    * Example: `"beefKGBWeSpHzYBHZXwp5So7wdQGX6mu4ZHCsH3uTar"`
  * `keepUnstakedDelinquents` (boolean, optional): Do not filter out delinquent validators with no stake
    * Example: `true`
  * `delinquentSlotDistance` (number, optional): Specify the number of slots behind the tip that a validator must fall to be considered delinquent. **NOTE:** For the sake of consistency between ecosystem products, _it is not recommended that this argument be specified._
    * Example: `10`

### Return object

The result field will be a JSON object of `current` and `delinquent` accounts, each containing an array of JSON objects with the following sub fields:

* `votePubkey:`Vote account address, as base-58 encoded string
* `nodePubkey:`  Validator identity, as base-58 encoded string
* `activatedStake:` The stake, in lamports, delegated to this vote account and active in this epoch
* `epochVoteAccount:` Whether the vote account is staked for this epoch
* `commission:` Percentage (0-100) of rewards payout owed to the vote account
* `lastVote:` Most recent slot voted on by this vote account
* `epochCredits:` Latest history of earned credits for up to five epochs, as an array of arrays containing: `[epoch, credits, previousCredits]`.
* `rootSlot:` Current root slot for this vote account

### JSON-RPC Request Example

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "getTokenAccountsByOwner",
  "params": [{votePubkey: 'beefKGBWeSpHzYBHZXwp5So7wdQGX6mu4ZHCsH3uTar'}]
}
```

### JSON-RPC Response Example

```json
{
  "jsonrpc": "2.0",
  "result": {
    "current": [
      {
        "commission": 0,
        "epochVoteAccount": true,
        "epochCredits": [
          [1, 64, 0],
          [2, 192, 64]
        ],
        "nodePubkey": "B97CCUW3AEZFGy6uUg6zUdnNYvnVq5VG8PUtb2HayTDD",
        "lastVote": 147,
        "activatedStake": 42,
        "votePubkey": "3ZT31jkAGhUaw8jsy4bTknwBMP8i4Eueh52By4zXcsVw"
      }
    ],
    "delinquent": []
  },
  "id": 1
}
```
