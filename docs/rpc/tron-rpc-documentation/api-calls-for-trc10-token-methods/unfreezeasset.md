# unfreezeasset

### How to use it

<pre class="language-typescript" data-overflow="wrap" data-line-numbers><code class="lang-typescript">// yarn add @tatumio/tatum
<strong>
</strong><strong>import { TatumSDK, Tron, Network } from '@tatumio/tatum'
</strong>
const tatum = await TatumSDK.init<Tron>({network: Network.TRON})

const res = await tatum.rpc.unfreezeAsset('TPswDDCAWhJAZGdHPidFg5nEf8TkNToDX1', {
visible: true,
})

await tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
</code></pre>

### Overview

The `unfreezeAsset` method allows the unstaking of a token that has passed the minimum freeze duration on the TRON blockchain.

### Parameters

This method accepts the following parameters:

* `ownerAddress` (string): Account address. The address of the owner of the assets. This must be a hexString.&#x20;
* `options` (optional): Additional options for the transaction.
  * `permission_id` (integer, optional): This is optional and mainly used for multi-signature transactions.
  * `visible` (boolean, optional): Indicates whether the address is in base58 format. This is also optional. Default value is true.

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

Since the transaction type is `UnfreezeAssetContract`, the fields contained in `raw_data.contract[0].parameter.value` in the transaction are as follows:

* `owner_address` (string): Account address

### HTTP Request Example

```json
{
  "owner_address": "TPswDDCAWhJAZGdHPidFg5nEf8TkNToDX1",
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
            "owner_address": "TZ4UXDV5ZhNW7fb2AMSbgfAEZ7hWsnYS2g"
          },
          "type_url": "type.googleapis.com/protocol.UnfreezeAssetContract"
        },
        "type": "UnfreezeAssetContract"
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
