# clearabi

### How to use it

{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Tron, Network, VisibleOption } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Tron>({network: Network.TRON})

const res = await tatum.rpc.clearAbi('TSNEe5Tf4rnc9zPMNXfaTF5fZfHDDH8oyW', 'TG3XXyExBkPp9nzdajDZsozEu4BkaSJozs', {
visible: true,
})

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}

### Overview

The `clearAbi` method allows clearing the ABI (Application Binary Interface) information of a smart contract on the TRON blockchain. This operation is often used when there is a need to remove outdated or incorrect ABI information from a smart contract.

### Parameters

* `ownerAddress` (string): The account address that owns the smart contract. It can be in base58check format if visible is true; otherwise, it should be in hex format.
* `contractAddress` (string): The address of the smart contract. It can be in base58check format if visible is true; otherwise, it should be in hex format.
* `options` (object, optional): This is an optional parameter that can include:
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

Since the transaction type is `ClearABIContract`, the fields contained in `raw_data.contract[0].parameter.value` in the transaction are as follows:

* `owner_address` - Account address.
* `contract_address` - Contract address.

### HTTP Request Example

```json
{
  "owner_address": "TSNEe5Tf4rnc9zPMNXfaTF5fZfHDDH8oyW",
  "contract_address": "TG3XXyExBkPp9nzdajDZsozEu4BkaSJozs",
  "visible": true
}
```

### HTTP Response Example

```json
{
  "visible": true,
  "txID": "0841733f1141ecd4f932551a26db7b7a4c8077e95bfa78d28ab806d85a3114b1",
  "raw_data": {
    "contract": [
      {
        "parameter": {
          "value": {
            "owner_address": "TSNEe5Tf4rnc9zPMNXfaTF5fZfHDDH8oyW",
            "contract_address": "TG3XXyExBkPp9nzdajDZsozEu4BkaSJozs"
          },
          "type_url": "type.googleapis.com/protocol.ClearABIContract"
        },
        "type": "ClearABIContract"
      }
    ],
    "ref_block_bytes": "ee6c",
    "ref_block_hash": "1819e770abbc2e4c",
    "expiration": 1684770510000,
    "timestamp": 1684770452476
  },
  "raw_data_hex": "0a02ee6c22081819e770abbc2e4c40b0a997a184315a630830125f0a2d747970652e676f6f676c65617069732e636f6d2f70726f746f636f6c2e436c656172414249436f6e7472616374122e0a1541b3dcf27c251da9363f1a4888257c16676cf54edf12154142a1e39aefa49290f2b3f9ed688d7cecf86cd6e070fce793a18431"
}
```
