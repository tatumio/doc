# delegateresource

### How to use It

{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Tron, Network, BigNumber, TronStakeType } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Tron>({network: Network.TRON})

const res = await tatum.rpc.delegateResource('TZ4UXDV5ZhNW7fb2AMSbgfAEZ7hWsnYS2g', 'TPswDDCAWhJAZGdHPidFg5nEf8TkNToDX1', new BigNumber(1000000), TronStakeType.BANDWIDTH, false)

await tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}

### Overview

The `delegateResource` method enables the delegation of bandwidth or energy resources to other accounts in TRON's Stake2.0. This could be useful for supporting specific operations of receiver accounts or to participate in staking and earn rewards.

### Parameters

Here are the parameters for the `delegateResource` method:

* `ownerAddress` (string): The address of the account that is delegating the resources. Default format is hexString.
* `receiverAddress` (string): The address of the account that will receive the delegated resources.
* `balance` (integer): The amount of TRX staked for resources to be delegated, unit is sun.
* `resource` (string): The type of resource to delegate, either 'BANDWIDTH' or 'ENERGY'.
* `lock` (boolean): Determines whether the delegation is locked. If set to true, the delegated resources cannot be undelegated within 3 days. If the owner delegates the same type of resources using the lock to the same address, the lock time will be reset to 3 days.
* `options` (object, optional): This optional parameter contains the following properties:
  * `visible` (boolean, optional): Determines whether the address is in base58 format.
  * `permissionId` (integer, optional): Used for multi-signature transactions.

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

Since the transaction type is `DelegateResourceContract`, the fields contained in `raw_data.contract[0].parameter.value` in the transaction are as follows:

* `owner_address`: The address of the account that delegated the resources.
* `resource`: The type of delegated resource.
* `receiver_address`: The address of the account that received the delegated resources.
* `balance`: The amount of TRX staked for resources that were delegated.
* `lock`: Indicates whether the delegation was locked.

### HTTP Request Example

```json
{
  "owner_address": "TZ4UXDV5ZhNW7fb2AMSbgfAEZ7hWsnYS2g",
  "receiver_address": "TPswDDCAWhJAZGdHPidFg5nEf8TkNToDX1",
  "balance": 1000000,
  "resource": "BANDWIDTH",
  "lock": false,
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
          "type_url": "type.googleapis.com/protocol.DelegateResourceContract"
        },
        "type": "DelegateResourceContract"
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
