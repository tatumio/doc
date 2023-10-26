# transferasset

### How to use it

{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Tron, Network, TransferAssetIssueByAccountOptions } from '@tatumio/tatum'
import { BigNumber } from 'bignumber.js';

const tatum = await TatumSDK.init<Tron>({network: Network.TRON})

const options: TransferAssetIssueByAccountOptions = {
  // optional parameters
};

const ownerAddress = "TZ4UXDV5ZhNW7fb2AMSbgfAEZ7hWsnYS2g";
const toAddress = "TPswDDCAWhJAZGdHPidFg5nEf8TkNToDX1";
const assetName = "31303030303031";
const amount = new BigNumber(1);

const res = await tatum.rpc.transferAsset(ownerAddress, toAddress, assetName, amount, options);

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}

### Overview

The `transferAsset` method is used to transfer TRC10 tokens from one address to another on the TRON network. This could be used in a variety of situations, such as transferring tokens to a user's account after they've made a purchase, or redistributing tokens between accounts as part of a dApp's internal logic.

### Parameters

* `ownerAddress` (string) - The account address from which the tokens are transferred.
* `toAddress` (string) - The target address to receive the transferred tokens.
* `assetName` (string) - The token ID to transfer.
* `amount` (BigNumber) - The amount of token to transfer.
* `options` (object, optional): This optional parameter contains the following properties:
  * `visible` (boolean) - Whether the address is in base58 format.
  * `extraData` (string) - Notes on the transaction, HEX format.

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

Since the transaction type is `TransferAssetContract`, the fields contained in `raw_data.contract[0].parameter.value` in the transaction are as follows:

* `owner_address` (string): Transaction initiator's address.
* `asset_name` (string): The token id to transfer
* `to_address` (string): The target address to transfer
* `amount` (integer): The amount of token to transfer.

### HTTP Request Example

```json
{
  "owner_address": "TZ4UXDV5ZhNW7fb2AMSbgfAEZ7hWsnYS2g",
  "to_address": "TPswDDCAWhJAZGdHPidFg5nEf8TkNToDX1",
  "asset_name": "31303030303031",
  "amount": 1,
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
            "to_address": "TPswDDCAWhJAZGdHPidFg5nEf8TkNToDX1",
            "asset_name: "62747474657374"
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
