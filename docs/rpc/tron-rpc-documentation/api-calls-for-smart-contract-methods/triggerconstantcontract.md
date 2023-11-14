# triggerconstantcontract

### How to use it

{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Tron, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Tron>({network: Network.TRON})

const res = await tatum.rpc.triggerConstantContract(
  'TZ4UXDV5ZhNW7fb2AMSbgfAEZ7hWsnYS2g', 
  'TG3XXyExBkPp9nzdajDZsozEu4BkaSJozs', 
  'balanceOf(address)', 
  '000000000000000000000000a614f803b6fd780986a42c78ec9c7f77e6ded13c', 
  {
    visible: true,
  }
)

await tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}

### Overview

The `triggerConstantContract` method is used to interact with smart contracts on the TRON blockchain. It allows you to invoke either readonly (view or pure) or non-readonly functions of a contract for contract data queries or estimating energy consumption. Notably, this operation does not generate an on-chain transaction and does not change the status of the current node.

### Parameters

* `ownerAddress` (string): The owner's address that triggers the contract. Use base58check format if visible=true, otherwise use hex format.
* `contractAddress` (string): The smart contract address. Use base58check format if visible=true, otherwise use hex format.
* `functionSelector` (string): The function call; must not be left blank.
* `parameter` (string): The parameter encoding must be in accordance with the ABI rules.
* `options` (object, optional): Optional settings for the contract trigger, including:
  * `callValue` (integer, optional): The amount of TRX transferred to the contract with this transaction, in sun. This field may be used when estimating energy consumption.
  * `visible` (boolean, optional): Optional. Whether the address is in base58 format.

### Return Object

* `result`
  * `result` - When error ocuurs, this is empty, otherwise true.
  * `code` - Error code.
  * `message -` Error message.
* `energy_used` (integer): The estimated energy consumption.
* `constant_result` (array of strings): The result list of triggered functions.
* `transaction`: Transaction information. For details, refer to GetTransactionByID.
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
  "owner_address": "TZ4UXDV5ZhNW7fb2AMSbgfAEZ7hWsnYS2g",
  "contract_address": "TG3XXyExBkPp9nzdajDZsozEu4BkaSJozs",
  "function_selector": "balanceOf(address)",
  "parameter": "000000000000000000000000a614f803b6fd780986a42c78ec9c7f77e6ded13c",
  "visible": true
}
```

### HTTP Response Example

```json
{
  "result": {
    "result": true
  },
  "energy_used": 541,
  "constant_result": [
    "00000000000000000000000000000000000000000000000000000000000186a0"
  ],
  "transaction": {
    "ret": [
      {}
    ],
    "visible": true,
    "txID": "342791a4015feba921cea6e7c3e3d5ba4d1ede50f3508a686e643709b14abce2",
    "raw_data": {
      "contract": [
        {
          "parameter": {
            "value": {
              "data": "70a08231000000000000000000000000a614f803b6fd780986a42c78ec9c7f77e6ded13c",
              "owner_address": "TZ4UXDV5ZhNW7fb2AMSbgfAEZ7hWsnYS2g",
              "contract_address": "TG3XXyExBkPp9nzdajDZsozEu4BkaSJozs"
            },
            "type_url": "type.googleapis.com/protocol.TriggerSmartContract"
          },
          "type": "TriggerSmartContract"
        }
      ],
      "ref_block_bytes": "e80d",
      "ref_block_hash": "7547cc93d09e65de",
      "expiration": 1684764945000,
      "timestamp": 1684764885358
    },
    "raw_data_hex": "0a02e80d22087547cc93d09e65de40e8d4c39e84315a8e01081f1289010a31747970652e676f6f676c65617069732e636f6d2f70726f746f636f6c2e54726967676572536d617274436f6e747261637412540a1541fd49eda0f23ff7ec1d03b52c3a45991c24cd440e12154142a1e39aefa49290f2b3f9ed688d7cecf86cd6e0222470a08231000000000000000000000000a614f803b6fd780986a42c78ec9c7f77e6ded13c70ee82c09e8431"
  }
}
```

