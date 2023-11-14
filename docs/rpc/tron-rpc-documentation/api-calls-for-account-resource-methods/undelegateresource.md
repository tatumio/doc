# undelegateresource

### How to use it

You can interact with the `unDelegateResource` method using the Tatum SDK. Here is an example on how you can do it:

{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Tron, Network, BigNumber, TronStakeType, VisibleAndPermissionIdOptions } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Tron>({network: Network.TRON})

const res = await tatum.rpc.unDelegateResource('TZ4UXDV5ZhNW7fb2AMSbgfAEZ7hWsnYS2g', 'TPswDDCAWhJAZGdHPidFg5nEf8TkNToDX1', new BigNumber(1000000), TronStakeType.BANDWIDTH, true, {
visible: true,
})

await tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}

### Overview

The `unDelegateResource` method allows for cancelling the delegation of bandwidth or energy resources to other accounts in Stake2.0 on the TRON blockchain. This could be useful in scenarios where the original owner needs to reclaim staked resources.

### Parameters

The `unDelegateResource` method accepts the following parameters:

* `ownerAddress` (string): The account address of the owner. By default, it should be in the hexString format.
* `receiverAddress` (string): The address of the account that is receiving the resource.
* `balance` (integer): The amount of TRX staked for resources to be delegated. The unit is sun. Example: 1000000
* `resource` (TronStakeType): The type of resource, can either be 'BANDWIDTH' or 'ENERGY'
* `lock` (boolean): This parameter signifies whether the resources should be locked or not.
* `options` (object, optional): This optional parameter contains the following properties:
  * `visible` (boolean, optional): This parameter signifies whether the address is in base58 format.
  * `permissionId` (integer, optional): This parameter is used for multi-signature purpose.

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

Since the transaction type is `UnDelegateResourceContract`, the fields contained in `raw_data.contract[0].parameter.value` in the transaction are as follows:

* `owner_address`: The address of the account that delegated the resources.
* `resource`: The type of delegated resource.
* `receiver_address`: The address of the account that received the delegated resources.
* `balance`: The amount of TRX staked for resources that were delegated.

### HTTP Request Example

```json
{
  "owner_address": "TZ4UXDV5ZhNW7fb2AMSbgfAEZ7hWsnYS2g",
  "receiver_address": "TPswDDCAWhJAZGdHPidFg5nEf8TkNToDX1",
  "balance": 1000000,
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
            "owner_address": "TZ4UXDV5ZhNW7fb2AMSbgfAEZ7hWsnYS2g",
            "receiver_address": "TPswDDCAWhJAZGdHPidFg5nEf8TkNToDX1",
            "balance": 1000000,
            "resource": "BANDWIDTH",
            "lock": false,
          },
          "type_url": "type.googleapis.com/protocol.UnDelegateResource"
        },
        "type": "UnDelegateResource"
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
