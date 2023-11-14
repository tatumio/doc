# createassetissue

### How to use it

{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Tron, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Tron>({network: Network.TRON})

const options = {
  freeAssetNetLimit: 10,
  publicFreeAssetNetLimit: 10,
  frozenSupply: {
    frozen_amount: 1,
    frozen_days: 2
  },
  precision: 2,
  description: "A new token",
}

const res = await tatum.rpc.createAssetIssue(
  'TZ4UXDV5ZhNW7fb2AMSbgfAEZ7hWsnYS2g',
  'MyToken',
  'MTK',
  1000000,
  1,
  1,
  1621629260000,
  1621629860000,
  'https://www.mytoken.com',
  options
)

await tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}

### Overview

The `createAssetIssue` RPC method allows you to create a new token on the TRON network. You need to specify various parameters like the name, abbreviation, total supply, and more.

Use cases for this method include creating new tokens for ICOs or for a DeFi project.

### Parameters

* `ownerAddress` (string): The address of the issuer.
* `name` (string): The name of the token.
* `abbr` (string): The abbreviation of the token.
* `totalSupply` (integer): The total supply of the token.
* `trxNum` (integer): Define the price by the ratio of trx\_num/num(The unit of 'trx\_num' is SUN).
* `num` (integer): Define the price by the ratio of trx\_num/num.
* `startTime` (integer): The ICO start time.
* `endTime` (integer): The ICO end time.
* `url` (string): The official website URL of the token.
* `options` (optional): Additional options for the transaction.
  * `freeAssetNetLimit` (integer, optional): Token free asset net limit.
  * `publicFreeAssetNetLimit` (integer, optional): Token public free asset net limit.
  * `frozenSupply` (object, optional): Object with parameters:
    * `frozen_amount` (integer): The number of tokens to be frozen.
    * `frozen_days` (integer): The number of days to freeze.
  * `precision` (integer, optional): The precision of the token.
  * `description` (string, optional): The description of the token.

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

Since the transaction type is `AssetIssueContract`, the fields contained in `raw_data.contract[0].parameter.value` in the transaction are as follows:

* `owner_address`: Issuer address.
* `name`: Token name.
* `abbr`: Token abbreviation.
* `total_supply`: Total supply of the token.
* `frozen_supply`: The number of tokens to be frozen as specified by the issuer when the token is issued.
* `trx_num`: Defines the price by the ratio of trx\_num/num (The unit of 'trx\_num' is SUN).
* `precision`: Precision of the token value.
* `num`: Defines the price by the ratio of trx\_num/num (The unit of 'trx\_num' is SUN).
* `start_time`: ICO start time.
* `end_time`: ICO end time.
* `description`: Description of the token.
* `url`: Official website URL of the token, default is hexString.
* `free_asset_net_limit`: Token free asset net limit.
* `public_free_asset_net_limit`: Token public free asset net limit for an account.
* `public_free_asset_net_usage`: The total number of token free bandwidth used by all token owners.
* `public_latest_free_net_time`: The timestamp of the last consumption of this token's free bandwidth.

### HTTP Request Example

```json
{
    "owner_address": "TZ4UXDV5ZhNW7fb2AMSbgfAEZ7hWsnYS2g",
    "name": "MyToken",
    "abbr": "MTK",
    "description": "A new token",
    "url": "https://www.mytoken.com",
    "frozen_supply": {
        "frozen_amount": 1,
        "frozen_days": 2
    },
    "visible": true,
    "total_supply": 1000000,
    "trx_num": 1,
    "num": 1,
    "start_time": 1621629260000,
    "end_time": 1621629860000
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
          "type_url": "type.googleapis.com/protocol.AssetIssueContract"
        },
        "type": "AssetIssueContract"
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
