# updateaccount

### How to use it

{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Tron, Network, VisibleAndPermissionIdOptions } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Tron>({network: Network.TRON})

const res = await tatum.rpc.updateAccount('TZ4UXDV5ZhNW7fb2AMSbgfAEZ7hWsnYS2g', '0x7570646174654e616d6531353330383933343635353139', {
  visible: true,
  permissionId: 1
})

await tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}

### Overview

The `updateAccount` method is used to modify the name of a TRON account. It's a powerful feature for personalizing and organizing accounts. After successfully updating, the response would be an unsigned transaction JSON object. The transaction type is `AccountUpdateContract`.

### Parameters

* `ownerAddress` (string): The account address to be modified. It should be converted to a hex string.
* `accountName` (string): The name of the account. It should be converted to a hex string.
* `options` (object, optional): This optional parameter contains the following properties:
  * `visible` (boolean, optional): Optional parameter to specify whether the address is in base58 format.
  * `permissionId` (integer, optional): Optional parameter used for multi-signature accounts.

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

Since the transaction type is `AccountUpdateContract`, the fields contained in `raw_data.contract[0].parameter.value` in the transaction are as follows:

* `owner_address` (string): The address of the transaction initiator.
* `account_name` (string): The account name.

### HTTP Request Example

```json
{
  "owner_address": "TZ4UXDV5ZhNW7fb2AMSbgfAEZ7hWsnYS2g",
  "account_name": "0x7570646174654e616d6531353330383933343635353139",
  "visible": true
}
```

### HTTP Response Example

```json
{
  "visible": true,
  "txID": "a00fd4a6fbb6dd42061b184cfd9bbbcd4faae5cf94c06dedb1c55c7b168c37cb",
  "raw_data": {
    "contract": [
      {
        "parameter": {
          "value": {
            "account_name": "0x7570646174654e616d6531353330383933343635353139",
            "owner_address": "TZ4UXDV5ZhNW7fb2AMSbgfAEZ7hWsnYS2g"
          },
          "type_url": "type.googleapis.com/protocol.AccountUpdateContract"
        },
        "type": "AccountUpdateContract"
      }
    ],
    "ref_block_bytes": "ad91",
    "ref_block_hash": "c7f32299fd0bae0e",
    "expiration": 1684490307000,
    "timestamp": 1684490248394
  },
  "raw_data_hex": "0a02ad912208c7f32299fd0bae0e40b88bc99b83315a8301080a127f0a32747970652e676f6f676c65617069732e636f6d2f70726f746f636f6c2e4163636f756e74557064617465436f6e747261637412490a30307837353730363436313734363534653631366436353331333533333330333833393333333433363335333533313339121541fd49eda0f23ff7ec1d03b52c3a45991c24cd440e70cac1c59b8331"
}
```
