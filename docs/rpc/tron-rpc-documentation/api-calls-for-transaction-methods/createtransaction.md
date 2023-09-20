# createtransaction

### How to Use

Example SDK code:

{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumcom/js

import { TatumSDK, Tron, Network } from '@tatumcom/js'

const tatum = await TatumSDK.init<Tron>({ network: Network.TRON })

const res = await tatum.rpc.createTransaction('ra5nK24KXen9AHvsdFTKHSANinZseWnPcX', 'rz6oqD16GHJmfRwK2viGm6jEM2r7QqzVvP', 1000, { visible: true })

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}

### Overview

The `createTransaction` method is used to create a TRON transaction. It allows you to transfer TRX (TRON native cryptocurrency) from one address to another.

Use cases:

* Transfer TRX from one TRON address to another.

### Parameters

* `ownerAddress` (string): The initiator's address for the transaction.
* `toAddress` (string): The destination address for the transaction.
* `amount` (BigNumber): The amount of TRX to transfer, in sun (the smallest unit of TRX, where 1 TRX = 1,000,000 sun).
* `options` (optional): Additional options for the transaction.
  * `visible` (boolean, optional): Specifies whether the address is in base58 format. Default: false.
  * `permission_id` (number, optional): The permission ID for multi-signature use.
  * `extra_data` (string, optional): Additional data for the transaction in HEX format.

### Return Object

`transaction` (`TransferContract`):&#x20;

* `raw_data.contract` - The main content of the transaction,`contract` is a list, but only one element is used at present. Different types of transactions have different contract contents. For example, for a TRX transfer type transaction, the contract will include the transfer amount, receiver address and other information. TRON supports multiple types of contracts, please refer to the official documentation [Types of Transaction](https://developers.tron.network/docs/tron-protocol-transaction#types-of-transaction).
* `raw_data.ref_block_bytes` - The height of the transaction reference block, using the 6th to 8th (exclusive) bytes of the reference block height, a total of 2 bytes. The reference block is used in the TRON TAPOS mechanism, which can prevent a replay of a transaction on forks that do not include the referenced block. Generally, the latest solidified block is used as the reference block.
* `raw_data.ref_block_hash` - The hash of the transaction reference block, using the 8th to 16th (exclusive) bytes of the reference block hash, a total of 8 bytes. The reference block is used in the TRON TAPOS mechanism, which can prevent a replay of a transaction on forks that do not include the referenced block. Generally, the latest solidified block is used as the reference block.
* `raw_data.expiration` - Transaction expiration time, beyond which the transaction will no longer be packed. If the transaction is created by calling the java-tron API, its expiration time will be automatically set by the node to the value of adding 60 seconds to the timestamp of the node's latest block. The expiration time interval can be modified in the node's configuration file, the maximum value cannot exceed 24 hours.
* `raw_data.data` - Transaction memo.
* `raw_data.timestamp` - Transaction timestamp, set as the transaction creation time.
* `raw_data.fee_limit` - The maximum energy cost allowed for the execution of smart contract transactions. Only deploying and triggering smart contract transactions need to be set, others not.
* `signature` - The sender's signature for the transaction. This proves that the transaction could only have come from the sender and was not sent fraudulently.
* `txID` - transaction id

Since the transaction type is `TransferContract`, the fields contained in `raw_data.contract[0].parameter.value` in the transaction are as follows:

* `owner_address` (string): Transaction initiator's address.
* `to_address` (string): Destination address.
* `amount` (int64): Transfer amount in sun.

### HTTP Request Example

Example of the JSON request body for the HTTP request:

```json
{
  "owner_address": "TZ4UXDV5ZhNW7fb2AMSbgfAEZ7hWsnYS2g",
  "to_address": "TPswDDCAWhJAZGdHPidFg5nEf8TkNToDX1",
  "amount": 1000,
  "visible": true
}
```

### HTTP Response Example

```json
{
  "visible": true,
  "txID": "094d59ae6c22cb6f206f4b263eec54a1dbfc1d1704d0c43a31d90b8b66ee4fbb",
  "raw_data": {
    "contract": [
      {
        "parameter": {
          "value": {
            "amount": 1000,
            "owner_address": "TZ4UXDV5ZhNW7fb2AMSbgfAEZ7hWsnYS2g",
            "to_address": "TPswDDCAWhJAZGdHPidFg5nEf8TkNToDX1"
          },
          "type_url": "type.googleapis.com/protocol.TransferContract"
        },
        "type": "TransferContract"
      }
    ],
    "ref_block_bytes": "ab93",
    "ref_block_hash": "88c6e64972349f0f",
    "expiration": 1684488576000,
    "timestamp": 1684488517323
  },
  "raw_data_hex": "0a02ab93220888c6e64972349f0f4080b8df9a83315a66080112620a2d747970652e676f6f676c65617069732e636f6d2f70726f746f636f6c2e5472616e73666572436f6e747261637412310a1541fd49eda0f23ff7ec1d03b52c3a45991c24cd440e12154198927ffb9f554dc4a453c64b2e553a02d6df514b18e80770cbeddb9a8331"
}
```
