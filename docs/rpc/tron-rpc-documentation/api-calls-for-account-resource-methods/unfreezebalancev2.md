# unfreezebalancev2

### How to use it

{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Tron, Network } from '@tatumio/tatum'
import { BigNumber } from 'bignumber.js'
import { TronStakeType } from '@tatumio/tatum/dist/src/blockchain'

const tatum = await TatumSDK.init<Tron>({network: Network.TRON})

const res = await tatum.rpc.unfreezeBalanceV2(
  'TZ4UXDV5ZhNW7fb2AMSbgfAEZ7hWsnYS2g',
  new BigNumber(1000000),
  TronStakeType.BANDWIDTH,
  { visible: true }
)

await tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}

### Overview

The `unfreezeBalanceV2` method is used to unlock TRX staked at the Stake 2.0 stage. After unstaking, the user needs to wait for 14 days before they can withdraw the funds. The method also withdraws any unclaimed voting rewards to the account, and if previously unstaked funds have passed the lock-up period, it also withdraws them at the same time. The voting reward withdrawn and the amount of funds withdrawn can be queried through the `gettransactioninfobyid` API.

### Parameters

The `unfreezeBalanceV2` method accepts the following parameters:

* `ownerAddress` (string): The account address
* `unfreeze_balance` (BigNumber): The amount of TRX to unstake, in sun
* `resource` (string): The resource type: 'BANDWIDTH' or 'ENERGY'
* `options` (object, optional): An object that can have the following properties:
  * `visible` (boolean): Whether the address is in base58 format
  * `permissionId` (integer): For multi-signature use, optional

### Return Object

* `raw_data.contract` - The main content of the transaction, contract is a list, but only one element is used at present. Different types of transactions have different contract contents. For example, for a TRX transfer type transaction, the contract will include the transfer amount, receiver address and other information. TRON supports multiple types of contracts, please refer to the official documentation [Types of Transaction](https://developers.tron.network/docs/tron-protocol-transaction#types-of-transaction).
* `raw_data.ref_block_bytes` - The height of the transaction reference block, using the 6th to 8th (exclusive) bytes of the reference block height, a total of 2 bytes. The reference block is used in the TRON TAPOS mechanism, which can prevent a replay of a transaction on forks that do not include the referenced block. Generally, the latest solidified block is used as the reference block.
* `raw_data.ref_block_hash` - The hash of the transaction reference block, using the 8th to 16th (exclusive) bytes of the reference block hash, a total of 8 bytes. The reference block is used in the TRON TAPOS mechanism, which can prevent a replay of a transaction on forks that do not include the referenced block. Generally, the latest solidified block is used as the reference block.
* `raw_data.expiration` - Transaction expiration time, beyond which the transaction will no longer be packed. If the transaction is created by calling the java-tron API, its expiration time will be automatically set by the node to the value of adding 60 seconds to the timestamp of the node's latest block. The expiration time interval can be modified in the node's configuration file, the maximum value cannot exceed 24 hours.
* `raw_data.data` - Transaction memo.
* `raw_data.timestamp` - Transaction timestamp, set as the transaction creation time.
* `raw_data.fee_limit` - The maximum energy cost allowed for the execution of smart contract transactions. Only deploying and triggering smart contract transactions need to be set, others not.
* `signature` - The sender's signature for the transaction. This proves that the transaction could only have come from the sender and was not sent fraudulently.
* `txID` - transaction id

Since the transaction type is UnFreezeBalanceV2Contract, the fields contained in `raw_data.contract[0].parameter.value` in the transaction are as follows:

* `owner_address`: The account address
* `resource`: The resource type
* `unfreeze_balance`: The unstake amount, unit is sun

### HTTP Request Example

```json
{
  "owner_address": "TZ4UXDV5ZhNW7fb2AMSbgfAEZ7hWsnYS2g",
  "unfreeze_balance": 1000000,
  "resource": "BANDWIDTH",
  "visible": true
}
```

### HTTP Response Example

```json
{
  "txID": "3d0a235547b08f9d5e1d465f6d7dc28da6436a8d9c3b768d1a989cac7e5c94cf",
  "raw_data": {
    "contract": [
      {
        "parameter": {
          "value": {
            "unfreeze_balance": 1000000,
            "owner_address": "TZ4UXDV5ZhNW7fb2AMSbgfAEZ7hWsnYS2g",
            "resource": "BANDWIDTH"
          },
          "type_url": "type.googleapis.com/protocol.UnfreezeBalanceContract"
        },
        "type": "UnfreezeBalanceContract"
      }
    ],
    "ref_block_bytes": "4a1b",
    "ref_block_hash": "4dc3c8c4476d5d56",
    "expiration": 1582208742000,
    "timestamp": 1582208686873,
    "fee_limit": 1000000000
  },
  "raw_data_hex": "0a024a1b22084dc3c8c4476d5d5640c8fcaf8d2d5a2e5a680801126a0a3074..."
}
```
