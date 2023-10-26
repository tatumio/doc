# participateassetissue

### How to use It

{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Tron, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Tron>({network: Network.TRON})

const res = await tatum.rpc.participateAssetIssue(
    'TPswDDCAWhJAZG5nEf8TkNToDX1', 
    'TZ4UXDV5ZhNW7fb2AMSbgfAEZ7hWsnYS2g', 
    '1000001031303030303031', 
    100000, 
    {
    visible: true,
    }
)

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}

### Overview

The `participateAssetIssue` method allows an account to participate in a token issuance on the TRON blockchain. This participation involves purchasing the issued tokens with TRX, the native currency of TRON. The method returns an unsigned transaction object which contains the details of the ParticipateAssetIssueContract.

### Parameters

* `toAddress` (string): The issuer's address.
* `ownerAddress` (string): The account address participating in the token issuance.
* `assetName` (string): The token ID.
* `amount` (integer): The amount of TRX used to purchase the issued token. The unit is in sun.
* `options` (object, optional): Additional options, which include:
  * `visible` (boolean, optional): Specifies whether the address is in base58 format.

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

Since the transaction type is `ParticipateAssetIssueContract`, the fields contained in `raw_data.contract[0].parameter.value` in the transaction are as follows:

* `owner_address` - Account address participating in the token issuance. (Type: string)
* `to_address` - The issuer's address. (Type: string)
* `asset_name` - Token ID. (Type: string)
* `amount` - The amount of TRX used to purchase the issued token. Unit is in sun. (Type: integer

### HTTP Request Example

```json
{
  "to_address": "TPswDDCAWhJAZGdHPidFg5nEf8TkNToDX1",
  "owner_address": "TZ4UXDV5ZhNW7fb2AMSbgfAEZ7hWsnYS2g",
  "asset_name": "1000001031303030303031",
  "amount": 100000,
  "visible": true
}
```

### HTTP Response Example

```json
{
  "visible": true,
  "txID": "1789f68952b601243e09fc851eeed547cc1c9e16b0fc2cb6bf219aa07a1a8a9c",
  "raw_data": {
    "contract": [
      {
        "parameter": {
          "value": {
            "start_time": 2684752341111,
            "trx_num": 1,
            "frozen_supply": [
              {
                "frozen_amount": 1,
                "frozen_days": 2
              }
            ],
            "total_supply": 100,
            "num": 1,
            "name": "asdfasdfadsf",
            "end_time": 2684752345111,
            "description": "0x4578616d706c654465736372697074696f6e",
            "owner_address": "TZ4UXDV5ZhNW7fb2AMSbgfAEZ7hWsnYS2g",
            "abbr": "asdfsdf",
            "url": "0x7777772e6578616d706c652e636f6d"
          },
          "type_url": "type.googleapis.com/protocol.ParticipateAssetIssueContract"
        },
        "type": "ParticipateAssetIssueContract"
      }
    ],
    "ref_block_bytes": "e206",
    "ref_block_hash": "034cf77f0ad4956a",
    "expiration": 1684759677000,
    "timestamp": 1684759617932
  },
  "raw_data_hex": "0a02e2062208034cf77f0ad4956a40c890829c84315acd01080612c8010a2f747970652e676f6f676c65617069732e636f6d2f70726f746f636f6c2e41737365744973737565436f6e74726163741294010a1541fd49eda0f23ff7ec1d03b52c3a45991c24cd440e120c6173646661736466616473661a076173646673646620642a04080110023001400148f7d0d6bd914e5097f0d6bd914ea201263078343537383631366437303663363534343635373336333732363937303734363936663665aa01203078373737373737326536353738363136643730366336353265363336663664708cc3fe9b8431"
}
```
