# createaccount

### How to use it

The `createAccount` method allows you to create a new TRON account by using an already activated account. Here's an example of how to use this method with the Tatum SDK:

<pre class="language-typescript" data-overflow="wrap" data-line-numbers><code class="lang-typescript"><strong>// yarn add @tatumcom/js
</strong>
import { TatumSDK, Tron, Network } from '@tatumcom/js'

const tatum = await TatumSDK.init&#x3C;Tron>({network: Network.TRON})

const res = await tatum.rpc.createAccount('TZ4UXDV5ZhNW7fb2AMSbgfAEZ7hWsnYS2g', 'TFgY1uN8buRxAtV2r6Zy5sG3ACko6pJT1y', {
  visible: true,
})

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
</code></pre>

### Overview

The `createAccount` method allows the creation of new accounts on the TRON blockchain network. This method utilizes an already activated account to create a new account. It is essential to note that the expiration time of the HTTP API creation transaction is one minute. This means you need to complete the signing and broadcast of the transaction within one minute after the creation.

Use cases for this method include creating new users or creating a new account for different operations within your application.

### Parameters

The `createAccount` method takes the following parameters:

* `owner_address` (string): The address of the activated account used to create the new account. It should be converted to a hex string.
* `account_address` (string): The address of the new account to be created. This should also be converted to a hex string and should be calculated in advance.
* `options` (object, optional): This optional parameter contains the following properties:
  * `visible` (boolean, optional): This field indicates whether the address is in base58 format or not.
  * `permission_id` (integer, optional): This field is used for multi-signature operations.

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

Since the transaction type is `TransferContract`, the fields contained in `raw_data.contract[0].parameter.value` in the transaction are as follows:

* `owner_address` (string): The address of the transaction initiator.
* `account_address` (string): The address of the activated account.
* `type` (integer): The account type. External account type is 0 and this field will not be displayed in the return value.

### HTTP Request Example

Below is an example of an HTTP request for the `createAccount` method:

```json
{
  "owner_address": "TZ4UXDV5ZhNW7fb2AMSbgfAEZ7hWsnYS2g",
  "account_address": "TFgY1uN8buRxAtV2r6Zy5sG3ACko6pJT1y",
  "visible": true
}
```

### HTTP Response Example

The response from the `createAccount` method will return the transaction details for creating a new account. Below is an example of a successful response:

```json
{
  "result": true,
  "txid": "08a8c7d7a67f6a8a60c2020c9f22033877fa5b8877662d16f5f2c368465046fb",
  "raw_data": {
    "contract": [
      {
        "parameter": {
          "value": {
            "owner_address": "TZ4UXDV5ZhNW7fb2AMSbgfAEZ7hWsnYS2g",
            "account_address": "TFgY1uN8buRxAtV2r6Zy5sG3ACko6pJT1y"
          },
          "type_url": "type.googleapis.com/protocol.AccountCreateContract"
        },
        "type": "AccountCreateContract"
      }
    ],
    "ref_block_bytes": "4df2",
    "ref_block_hash": "6eb26e5ebc0a6922",
    "expiration": 1623332388000,
    "timestamp": 1623332327858
  },
  "signature": [
    "da2d3cff56f3b43c430fe5a3e8a67a8e1e5c3402a5a64a6e1e19e45a223bd50a1a4e8c6275db608dfc6c60bc86b4b69053c5e1af37e2714d1bea716d2a66c04a00"
  ],
  "raw_data_hex": "0a024df2220c6eb26e5ebc0a69228c928afbef8c2d5a65080112640a2d747970652e676f6f676c65617069732e636f6d2f70726f746f636f6c2e4163636f756e74437265617465436f6e747261637412330a1541ef67873a4a8a6154c92020ef5a102a202e6a567bd121541b9a9c9c081a8f4e2926ac24d30070f8bf8c2d"
}
```
