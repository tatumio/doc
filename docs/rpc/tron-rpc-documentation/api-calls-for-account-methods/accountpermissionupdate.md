# accountpermissionupdate

### How to use it

{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Tron, Network, TronPermission, AccountPermissionUpdateOptions } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Tron>({network: Network.TRON})

const owner: TronPermission = {
  type: 0,
  permissionName: "owner",
  threshold: 1,
  operations: "",
  keys: [
    {
      address: "TZ4UXDV5ZhNW7fb2AMSbgfAEZ7hWsnYS2g",
      weight: 1
    }
  ]
}

const active: TronPermission = {
  "type": 2,
  "permission_name": "active0",
  "threshold": 2,
  "operations": "7fff1fc0037e0000000000000000000000000000000000000000000000000000",
  "keys": [
    {
      "address": "TZ4UXDV5ZhNW7fb2AMSbgfAEZ7hWsnYS2g",
      "weight": 1
    },
    {
      "address": "TPswDDCAWhJAZGdHPidFg5nEf8TkNToDX1",
      "weight": 1
    }
  ]
}

const res = await tatum.rpc.accountPermissionUpdate('TZ4UXDV5ZhNW7fb2AMSbgfAEZ7hWsnYS2g', [active], owner, {
  visible: true
})

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}

### Overview

The `accountPermissionUpdate` method is used to update an account's permissions on the TRON network. These permissions include the owner permission, account witness permissions, and a list of active permissions. The response is an unsigned transaction, with the transaction type being `AccountPermissionUpdateContract`.

### Parameters

* `ownerAddress` (string): The address of the owner.
* `actives` (TronPermission\[]): An array of active permissions for the account.
* `owner` (TronPermission): The owner permission for the account.
* `options` (object, optional): This optional parameter contains the following properties:
  * `visible` (boolean, optional): Optional parameter to specify whether the address is in base58 format.

Each `TronPermission` object has the following properties:

* `type` (number): The permission type.
* `permissionName` (string): The permission name.
* `threshold` (number): The threshold.
* `operations` (string): The operations the permission has.
* `keys` (Array<{ address: string, weight: number }>): An array of objects that represent the addresses and their respective weights that jointly own the permission. Up to 5 keys are allowed.

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

Since the transaction type is `AccountPermissionUpdateContract`, the fields contained in `raw_data.contract[0].parameter.value` in the transaction are as follows:

* `owner_address` (string): The owner's account address.
* `owner` (Permission): The owner permission of the account.
* `witness` (Permission): Account witness permissions.
* `actives` (Permission\[]): List of active permissions for the account.

### HTTP Request Example

```json
{
  "owner_address": "TZ4UXDV5ZhNW7fb2AMSbgfAEZ7hWsnYS2g",
  "actives": [
    {
      "type": 2,
      "permission_name": "active0",
      "threshold": 2,
      "operations": "7fff1fc0037e0000000000000000000000000000000000000000000000000000",
      "keys": [
        {
          "address": "TZ4UXDV5ZhNW7fb2AMSbgfAEZ7hWsnYS2g",
          "weight": 1
        },
        {
          "address": "TPswDDCAWhJAZGdHPidFg5nEf8TkNToDX1",
          "weight": 1
        }
      ]
    }
  ],
  "owner": {
    "type": 0,
    "permission_name": "owner",
    "threshold": 1,
    "operations": "",
    "keys": [
      {
        "address": "TZ4UXDV5ZhNW7fb2AMSbgfAEZ7hWsnYS2g",
        "weight": 1
      }
    ]
  },
  "visible": true
}
```

### HTTP Response Example

```json
{
  "visible": true,
  "txID": "f0fcda10229a8e289666c4d4c8756ad86e6df84966226bd9bc98e1607a4826b0",
  "raw_data": {
    "contract": [
      {
        "parameter": {
          "value": {
            "owner": {
              "keys": [
                {
                  "address": "TZ4UXDV5ZhNW7fb2AMSbgfAEZ7hWsnYS2g",
                  "weight": 1
                }
              ],
              "threshold": 1,
              "permission_name": "owner"
            },
            "owner_address": "TZ4UXDV5ZhNW7fb2AMSbgfAEZ7hWsnYS2g",
            "actives": [
              {
                "operations": "7fff1fc0037e0000000000000000000000000000000000000000000000000000",
                "keys": [
                  {
                    "address": "TZ4UXDV5ZhNW7fb2AMSbgfAEZ7hWsnYS2g",
                    "weight": 1
                  },
                  {
                    "address": "TPswDDCAWhJAZGdHPidFg5nEf8TkNToDX1",
                    "weight": 1
                  }
                ],
                "threshold": 2,
                "type": "Active",
                "permission_name": "active0"
              }
            ]
          },
          "type_url": "type.googleapis.com/protocol.AccountPermissionUpdateContract"
        },
        "type": "AccountPermissionUpdateContract"
      }
    ],
    "ref_block_bytes": "aeab",
    "ref_block_hash": "90861e40e6675e8e",
    "expiration": 1684491273000,
    "timestamp": 1684491216214
  },
  "raw_data_hex": "0a02aeab220890861e40e6675e8e40a886849c83315aea01082e12e5010a3c747970652e676f6f676c65617069732e636f6d2f70726f746f636f6c2e4163636f756e745065726d697373696f6e557064617465436f6e747261637412a4010a1541fd49eda0f23ff7ec1d03b52c3a45991c24cd440e12241a056f776e657220013a190a1541fd49eda0f23ff7ec1d03b52c3a45991c24cd440e1001226508021a0761637469766530200232207fff1fc0037e00000000000000000000000000000000000000000000000000003a190a1541fd49eda0f23ff7ec1d03b52c3a45991c24cd440e10013a190a154198927ffb9f554dc4a453c64b2e553a02d6df514b100170d6ca809c8331"
}
```

