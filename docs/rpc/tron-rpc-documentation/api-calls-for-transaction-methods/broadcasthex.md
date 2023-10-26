# broadcasthex

### How to use it

{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumcom/js

import { TatumSDK, Tron, Network } from '@tatumcom/js'

const tatum = await TatumSDK.init<Tron>({network: Network.TRON})

const res = await tatum.rpc.broadcastHex('transactionHex')

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}

### Overview

The `broadcastHex` method is used to broadcast a signed transaction to the TRON network. This is a crucial step in performing operations on the blockchain, such as transferring TRX tokens or interacting with smart contracts.

The method requires the signed transaction in hexadecimal format.

### Parameters

`transaction` (string): The signed transaction in hexadecimal format. This is a required parameter.

### Return Object

The response object contains the following fields:

`result` (boolean): Whether the broadcast was successful. true - successful; false - failed, and this field will not be displayed in the returned result.

`txid` (string): The Transaction ID of the broadcasted transaction.

`code` (string): The error code in case the broadcast fails.

`message` (string): Detailed error information in case the broadcast fails.

`transaction` (Transaction):&#x20;

* `raw_data.contract` - The main content of the transaction,`contract` is a list, but only one element is used at present. Different types of transactions have different contract contents. For example, for a TRX transfer type transaction, the contract will include the transfer amount, receiver address and other information. TRON supports multiple types of contracts, please refer to the official documentation [Types of Transaction](https://developers.tron.network/docs/tron-protocol-transaction#types-of-transaction).
* `raw_data.ref_block_bytes` - The height of the transaction reference block, using the 6th to 8th (exclusive) bytes of the reference block height, a total of 2 bytes. The reference block is used in the TRON TAPOS mechanism, which can prevent a replay of a transaction on forks that do not include the referenced block. Generally, the latest solidified block is used as the reference block.
* `raw_data.ref_block_hash` - The hash of the transaction reference block, using the 8th to 16th (exclusive) bytes of the reference block hash, a total of 8 bytes. The reference block is used in the TRON TAPOS mechanism, which can prevent a replay of a transaction on forks that do not include the referenced block. Generally, the latest solidified block is used as the reference block.
* `raw_data.expiration` - Transaction expiration time, beyond which the transaction will no longer be packed. If the transaction is created by calling the java-tron API, its expiration time will be automatically set by the node to the value of adding 60 seconds to the timestamp of the node's latest block. The expiration time interval can be modified in the node's configuration file, the maximum value cannot exceed 24 hours.
* `raw_data.data` - Transaction memo.
* `raw_data.timestamp` - Transaction timestamp, set as the transaction creation time.
* `raw_data.fee_limit` - The maximum energy cost allowed for the execution of smart contract transactions. Only deploying and triggering smart contract transactions need to be set, others not.
* `signature` - The sender's signature for the transaction. This proves that the transaction could only have come from the sender and was not sent fraudulently.
* `txID` - transaction id

### HTTP Request Example

```json
{
  "transaction": "0A8A010A0202DB2208C89D4811359A28004098A4E0A6B52D5A730802126F0A32747970652E676F6F676C65617069732E636F6D2F70726F746F636F6C2E5472616E736665724173736574436F6E747261637412390A07313030303030311215415A523B449890854C8FC460AB602DF9F31FE4293F1A15416B0580DA195542DDABE288FEC436C7D5AF769D24206412418BF3F2E492ED443607910EA9EF0A7EF79728DAAAAC0EE2BA6CB87DA38366DF9AC4ADE54B2912C1DEB0EE6666B86A07A6C7DF68F1F9DA171EEE6A370B3CA9CBBB00"
}
```

### HTTP Response Example

```json
{
  "result": false,
  "code": "TAPOS_ERROR",
  "txid": "38a0482d6d5a7d1439a50b848d68cafa7d904db48b82344f28765067a5773e1d",
  "message": "Tapos check error.",
  "transaction": "{\"raw_data\": {\"ref_block_bytes\": \"02db\",\"ref_block_hash\": \"c89d4811359a2800\",\"expiration\": 1560496575000,\"contract\": [{\"type\": \"TransferAssetContract\",\"parameter\": {\"type_url\": \"type.googleapis.com/protocol.TransferAssetContract\",\"value\": \"0a07313030303030311215415a523b449890854c8fc460ab602df9f31fe4293f1a15416b0580da195542ddabe288fec436c7d5af769d242064\"}}]},\"signature\": [\"8bf3f2e492ed443607910ea9ef0a7ef79728daaaac0ee2ba6cb87da38366df9ac4ade54b2912c1deb0ee6666b86a07a6c7df68f1f9da171eee6a370b3ca9cbbb00\"]}"
}
```
