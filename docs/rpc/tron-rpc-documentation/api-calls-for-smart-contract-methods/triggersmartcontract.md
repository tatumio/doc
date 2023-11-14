# triggersmartcontract

### How to Use It

Here is an example of how you can use the `triggerSmartContract` method with the Tatum SDK.

{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Tron, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Tron>({network: Network.TRON})

const options = {
  feeLimit: 1000000000,
  callValue: 0,
}

const result = await tatum.rpc.triggerSmartContract(
  'TZ4UXDV5ZhNW7fb2AMSbgfAEZ7hWsnYS2g', 
  'TG3XXyExBkPp9nzdajDZsozEu4BkaSJozs', 
  'transfer(address,uint256)', 
  '00000000000000000000004115208EF33A926919ED270E2FA61367B2DA3753DA0000000000000000000000000000000000000000000000000000000000000032',
  options
)

await tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}

### Overview

The `triggerSmartContract` method is used to call a smart contract function on the TRON network. The function parameters are encoded according to the ABI rules and the method returns an unsigned transaction, ready to be signed and broadcasted to the network. This method can be used for interacting with deployed smart contracts and triggering their functions.

### Parameters

* `ownerAddress`(string): Account address triggering the contract, converted to a hex string.
* `contractAddress`(string): Smart contract address, converted to a hex string.
* `functionSelector`(string): Function call from the smart contract. Must not be left blank.
* `parameter`(string): Function parameters, encoded according to the ABI rules.
* `options`: (object, optional): Additional options for the contract triggering.
  * `feeLimit`(integer, optional):  Maximum TRX consumption, measured in SUN (1 TRX = 1,000,000 SUN).
  * `callValue`(integer, optional): Amount of TRX transferred with this transaction, measured in SUN.
  * `permission_id`(integer, optional): For multi-signature.
  * `visible`(boolean, optional): Whether the address is in base58check format.

### Return Object

* `result`
  * `result` - When error ocuurs, this is empty, otherwise true.
  * `code` - Error code.
  * `message -` Error message.
* `transaction`&#x20;
  * `raw_data.contract` - The main content of the transaction,`contract` is a list, but only one element is used at present. Different types of transactions have different contract contents. For example, for a TRX transfer type transaction, the contract will include the transfer amount, receiver address and other information. TRON supports multiple types of contracts, please refer to the official documentation [Types of Transaction](https://developers.tron.network/docs/tron-protocol-transaction#types-of-transaction).
  * `raw_data.ref_block_bytes` - The height of the transaction reference block, using the 6th to 8th (exclusive) bytes of the reference block height, a total of 2 bytes. The reference block is used in the TRON TAPOS mechanism, which can prevent a replay of a transaction on forks that do not include the referenced block. Generally, the latest solidified block is used as the reference block.
  * `raw_data.ref_block_hash` - The hash of the transaction reference block, using the 8th to 16th (exclusive) bytes of the reference block hash, a total of 8 bytes. The reference block is used in the TRON TAPOS mechanism, which can prevent a replay of a transaction on forks that do not include the referenced block. Generally, the latest solidified block is used as the reference block.
  * `raw_data.expiration` - Transaction expiration time, beyond which the transaction will no longer be packed. If the transaction is created by calling the java-tron API, its expiration time will be automatically set by the node to the value of adding 60 seconds to the timestamp of the node's latest block. The expiration time interval can be modified in the node's configuration file, the maximum value cannot exceed 24 hours.
  * `raw_data.data` - Transaction memo.
  * `raw_data.timestamp` - Transaction timestamp, set as the transaction creation time.
  * `raw_data.fee_limit` - The maximum energy cost allowed for the execution of smart contract transactions. Only deploying and triggering smart contract transactions need to be set, others not.
  * `signature` - The sender's signature for the transaction. This proves that the transaction could only have come from the sender and was not sent fraudulently.
  * `txID` - transaction id

Since the transaction type is `TriggerSmartContract`, the fields contained in `transaction.raw_data.contract[0].parameter.value` in the transaction are as follows:

* `owner_address`: string. Account address.
* `contract_address`: string. Contract address.
* `call_value`: integer. The amount of TRX passed into the contract.
* `data`: string. Operating parameters.
* `call_token_value`: integer. The amount of TRC-10 transferred into the contract.
* `token_id`: integer. TRC-10 token id.

### HTTP Request Example

Here is an example of an HTTP request to trigger a smart contract:

```json
{
  "owner_address": "TZ4UXDV5ZhNW7fb2AMSbgfAEZ7hWsnYS2g",
  "contract_address": "TG3XXyExBkPp9nzdajDZsozEu4BkaSJozs",
  "function_selector": "transfer(address,uint256)",
  "parameter": "00000000000000000000004115208EF33A926919ED270E2FA61367B2DA3753DA0000000000000000000000000000000000000000000000000000000000000032",
  "fee_limit": 1000000000,
  "call_value": 0,
  "visible": true
}
```

### HTTP Response Example

```json
{
  "result": {
    "result": true
  },
  "transaction": {
    "visible": true,
    "txID": "27318af0aca1e748919c9f28a40c66776d468d06ec936cad1f56130df7704db7",
    "raw_data": {
      "contract": [
        {
          "parameter": {
            "value": {
              "data": "a9059cbb00000000000000000000004115208ef33a926919ed270e2fa61367b2da3753da0000000000000000000000000000000000000000000000000000000000000032",
              "owner_address": "TZ4UXDV5ZhNW7fb2AMSbgfAEZ7hWsnYS2g",
              "contract_address": "TG3XXyExBkPp9nzdajDZsozEu4BkaSJozs"
            },
            "type_url": "type.googleapis.com/protocol.TriggerSmartContract"
          },
          "type": "TriggerSmartContract"
        }
      ],
      "ref_block_bytes": "e70f",
      "ref_block_hash": "bde2c956cedbf2ae",
      "expiration": 1684764078000,
      "fee_limit": 1000000000,
      "timestamp": 1684764019325
    },
    "raw_data_hex": "0a02e70f2208bde2c956cedbf2ae40b0df8e9e84315aae01081f12a9010a31747970652e676f6f676c65617069732e636f6d2f70726f746f636f6c2e54726967676572536d617274436f6e747261637412740a1541fd49eda0f23ff7ec1d03b52c3a45991c24cd440e12154142a1e39aefa49290f2b3f9ed688d7cecf86cd6e02244a9059cbb00000000000000000000004115208ef33a926919ed270e2fa61367b2da3753da000000000000000000000000000000000000000000000000000000000000003270fd948b9e843190018094ebdc03"
  }
}
```
