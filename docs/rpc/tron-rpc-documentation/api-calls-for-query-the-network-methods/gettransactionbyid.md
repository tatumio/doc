# gettransactionbyid

### How to Use it

{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Tron, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Tron>({network: Network.TRON})

const transaction = await tatum.rpc.getTransactionById('7c2d4206c03a883dd9066d620335dc1be272a8dc733cfa3f6d10308faa37facc', {
visible: true,
})

await tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}

### Overview

The `getTransactionById` method is used to query transaction information using a transaction ID on the TRON network. This can be beneficial in several use cases, such as retrieving details about a specific transaction, verifying the transaction status, and checking the transaction content.

{% embed url="https://codepen.io/tatum-devrel/pen/wvQZNOG" %}

### Parameters

* `value` (string): ID of the transaction to be queried.
* `options` (object, optional): This optional parameter contains the following properties:
  * `visible` (boolean, optional): Whether the address is in base58 format.

### Return Object

The method returns a Promise resolving to a Transaction object containing:



* `raw_data.contract` - The main content of the transaction, contract is a list, but only one element is used at present. Different types of transactions have different contract contents. For example, for a TRX transfer type transaction, the contract will include the transfer amount, receiver address and other information. TRON supports multiple types of contracts, please refer to the official documentation [Types of Transaction](https://developers.tron.network/docs/tron-protocol-transaction#types-of-transaction).
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
 "value": "0x94eea63bb6774c1565a5a5adc37cc8b73bb5292c63f7829231e195314d338b98",
 "visible": true
}
```

### HTTP Response Example

```json
{
  "ret": [
    {
      "contractRet": "SUCCESS"
    }
  ],
  "signature": [
    "90f1b82fecfef333afc338d243bfd7e6506fc400f5cbb74034d2eff58ba04d520b5d12ab34f8dfd4d29e999ca1f86184670df41e0aa6131b38e52289acb6499000"
  ],
  "txID": "7c2d4206c03a883dd9066d620335dc1be272a8dc733cfa3f6d10308faa37facc",
  "raw_data": {
    "contract": [
      {
        "parameter": {
          "value": {
            "amount": 2000000,
            "owner_address": "TMmYhZ5XyjWwkPSLizzMoqyQLVrwqDdH5Y",
            "to_address": "TEouV6gdGqZvFDde6dDKHBJgbVFV2NW48T"
          },
          "type_url": "type.googleapis.com/protocol.TransferContract"
        },
        "type": "TransferContract"
      }
    ],
    "ref_block_bytes": "b663",
    "ref_block_hash": "fb1feb948ee9fff2",
    "expiration": 1681403964000,
    "fee_limit": 500000,
    "timestamp": 1681368025716
  },
  "raw_data_hex": "0a02b6632208fb1feb948ee9fff240e0d4f1dbf7305a67080112630a2d747970652e676f6f676c65617069732e636f6d2f70726f746f636f6c2e5472616e73666572436f6e747261637412320a1541816cf60987aa124eed29db9a057e476861b8d8dc1215413516435fb1e706c51efff614c7e14ce2625f28e51880897a70f494e0caf7309001a0c21e"
}
```
