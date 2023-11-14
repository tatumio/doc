# updateasset

### How to Use It

{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Tron, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Tron>({network: Network.TRON})

const res = await tatum.rpc.updateAsset('TPswDDCAWhJAZGdHPidFg5nEf8TkNToDX1', 'https://mytokenwebsite.com', {
  description: 'My Token Description',
  new_limit: 10000,
  new_public_limit: 50000,
  permission_id: 1,
  visible: true
});

await tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}

### Overview

The `updateAsset` method is used to update basic information about a TRC10 token on the TRON network. This method could be useful when the information of a TRC10 token needs to be updated, for instance, if the token's website URL changes or the bandwidth limits for the token are adjusted.

### Parameters

* `ownerAddress`(string): The issuer's address of the token in hexString format.
* `url`(string): The token's website url in hexString format.
* `options` (optional): An object containing additional parameters:
  * `description`(string, optional): The description of the token in hexString format.
  * `new_limit`(integer, optional): Each token holder's free bandwidth limit.
  * `new_public_limit`(integer, optional): The total free bandwidth limit of the token.
  * `permission_id`(integer, optional): Used for multi-signature purposes.
  * `visible`(boolean, optional): A boolean value indicating whether the address is in base58 format.

### Return Object

* `raw_data.contract` - The main content of the transaction,`contract` is a list, but only one element is used at present. Different types of transactions have different contract contents. For example, for a TRX transfer type transaction, the contract will include the transfer amount, receiver address and other information. TRON supports multiple types of contracts, please refer to the official documentation [Types of Transaction](https://developers.tron.network/docs/tron-protocol-transaction#types-of-transaction).
* `raw_data.ref_block_bytes` - The height of the transaction reference block, using the 6th to 8th (exclusive) bytes of the reference block height, a total of 2 bytes. The reference block is used in the TRON TAPOS mechanism, which can prevent a replay of a transaction on forks that do not include the referenced block. Generally, the latest solidified block is used as the reference block.
* `raw_data.ref_block_hash` - The hash of the transaction reference block, using the 8th to 16th (exclusive) bytes of the reference block hash, a total of 8 bytes. The reference block is used in the TRON TAPOS mechanism, which can prevent a replay of a transaction on forks that do not include the referenced block. Generally, the latest solidified block is used as the reference block.
* `raw_data.expiration` - Transaction expiration time, beyond which the transaction will no longer be packed. If the transaction is created by calling the java-tron API, its expiration time will be automatically set by the node to the value of adding 60 seconds to the timestamp of the node's latest block. The expiration time interval can be modified in the node's configuration file, the maximum value cannot exceed 24 hours.
* `raw_data.data` - Transaction memo.
* `raw_data.timestamp` - Transaction timestamp, set as the transaction creation time.
* `raw_data.fee_limit` - The maximum energy cost allowed for the execution of smart contract transactions. Only deploying and triggering smart contract transactions need to be set, others not.
* `signature` - The sender's signature for the transaction. This proves that the transaction could only have come from the sender and was not sent fraudulently.
* `txID` - transaction id

Since the transaction type is `UpdateAssetContract`, the fields contained in `raw_data.contract[0].parameter.value` in the transaction are as follows:

* `owner_address`: Account address
* `description`: Description
* `url`: Token's website Url
* `new_limit`: The limit of Bandwidth point which each caller can consume
* `new_public_limit`: The limit of Bandwidth point which all callers can consume

### HTTP Request Example

```json
{
  "owner_address": "TPswDDCAWhJAZGdHPidFg5nEf8TkNToDX1",
  "description": "My Token Description",
  "url": "https://mytokenwebsite.com",
  "new_limit": 10000,
  "new_public_limit": 50000,
  "permission_id": 1,
  "visible": true
}
```

### HTTP Response Example

```json
{
  "transaction": {
    "txID": "b5e7e6e7908d295feb3e91784c68ddd0640830a27c465a4e8ee4ad87e7aff263",
    "raw_data": {
      "contract": [
        {
          "parameter": {
            "value": {
              "owner_address": "TPswDDCAWhJAZGdHPidFg5nEf8TkNToDX1",
              "description": "My Token Description",
              "url": "https://mytokenwebsite.com",
              "new_limit": 10000,
              "new_public_limit": 50000
            },
            "type_url": "type.googleapis.com/protocol.UpdateAssetContract"
          },
          "type": "UpdateAssetContract"
        }
      ],
      "ref_block_bytes": "09f6",
      "ref_block_hash": "fec5e58087511d2a",
      "expiration": 1570676090000,
      "timestamp": 1570676035768
    },
    "raw_data_hex": "0a0209f62202..."
  }
}
```
