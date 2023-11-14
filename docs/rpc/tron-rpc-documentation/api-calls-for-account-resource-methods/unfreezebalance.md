# unfreezebalance

### How to use it&#x20;

{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Tron, Network, TronStakeType, UnFreezeAccountOptions } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Tron>({network: Network.TRON})

const ownerAddress = 'TZZyXU3pYgKkcc6RBVYHzY1JRLyPeN5BWy'

const res = await tatum.rpc.unfreezeBalance(ownerAddress, TronStakeType.ENERGY, {
  visible: true,
})

await tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}

### Overview

The `unfreezeBalance` method is used to unstake previously staked TRX and release the obtained bandwidth or energy and TP. This operation will automatically cancel all votes.

### Parameters

* `owner_address` (string): The owner address (default in hexString format).
* `resource` (string): The type of TRX stake, either 'BANDWIDTH' or 'ENERGY'.
* `options` (object, optional): This optional parameter contains the following properties:
  * `receiver_address` (string, optional): Optional parameter for the address that will lose the resource (default in hexString format).
  * `permission_id` (integer, optional): For multi-signature use.
  * `visible` (boolean, optional): Defaults to false. Whether addresses are in base58 format.

### Return Object

* `raw_data.contract` - The main content of the transaction, contract is a list, but only one element is used at present. Different types of transactions have different contract contents. For example, for a TRX transfer type transaction, the contract will include the transfer amount, receiver address and other information. TRON supports multiple types of contracts, please refer to the official documentation [Types of Transaction](https://developers.tron.network/docs/tron-protocol-transaction#types-of-transaction).
* `raw_data.ref_block_bytes` - The height of the transaction reference block, using the 6th to 8th (exclusive) bytes of the reference block height, a total of 2 bytes. The reference block is used in the TRON TAPOS mechanism, which can prevent a replay of a transaction on forks that do not include the referenced block. Generally, the latest solidified block is used as the reference block.
* `raw_data.ref_block_hash` - The hash of the transaction reference block, using the 8th to 16th (exclusive) bytes of the reference block hash, a total of 8 bytes. The reference block is used in the TRON TAPOS mechanism, which can prevent a replay of a transaction on forks that do not include the referenced block. Generally, the latest solidified block is used as the reference block.
* `raw_data.expiration` - Transaction expiration time, beyond which the transaction will no longer be packed. If the transaction is created by calling the java-tron API, its expiration time will be automatically set by the node to the value of adding 60 seconds to the timestamp of the node's latest block. The expiration time interval can be modified in the node's configuration file, the maximum value cannot exceed 24 hours.
* `raw_data.data` - Transaction memo.
* `raw_data.timestamp` - Transaction timestamp, set as the transaction creation time.
* `raw_data.fee_limit` - The maximum energy cost allowed for the execution of smart contract transactions. Only deploying and triggering smart contract transactions need to be set, others not.
* `signature` - The sender's signature for the transaction. This proves that the transaction could only have come from the sender and was not sent fraudulentl
* `txID` - transaction id

Since the transaction type is `UnfreezeBalanceContract`, the fields contained in `raw_data.contract[0].parameter.value` in the transaction are as follows:

* `owner_address`: The owner address.
* `resource`: The type of TRX stake, either 'BANDWIDTH' or 'ENERGY'.
* `receiver_address`: The address that will lose the resource.

### HTTP Request Example

```json
{
  "owner_address": "TZ4UXDV5ZhNW7fb2AMSbgfAEZ7hWsnYS2g",
  "resource": "BANDWIDTH",
  "visible": true
}
```

### HTTP Response Example

```json
{
  "visible": false,
  "txID": "efb6ff6dba6e5998d7258a63436e4717428892f02df2adb6deea8550d36e5e34",
  "raw_data": {
    "contract": [
      {
        "parameter": {
          "value": {
            "resource": "BANDWIDTH",
            "owner_address": "4100776428620856ae1d71562812b734e356b68551"
          },
          "type_url": "type.googleapis.com/protocol.UnfreezeBalanceContract"
        },
        "type": "UnfreezeBalanceContract"
      }
    ],
    "ref_block_bytes": "3041",
    "ref_block_hash": "3d1b89e6c7c34b52",
    "expiration": 1649176881000,
    "timestamp": 1649176821557
  },
  "raw_data_hex": "0a02304122083d1b89e6c7c34b5240e8cee8d4ff2f5a5a080b12560a32747970652e676f6f676c65617069732e636f6d2f70726f746f636f6c2e467265657a6542616c616e6365436f6e747"
}
```
