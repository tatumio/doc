# updatesetting

### How to use it

{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Tron, Network, VisibleAndPermissionIdOptions } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Tron>({network: Network.TRON})

const ownerAddress = 'TSNEe5Tf4rnc9zPMNXfaTFKHSANinZseWnPcX'
const contractAddress = 'TG3XXyExBkPp9nzdajDZsozEu4BkaSJozs'
const consumeUserResourcePercent = 10
const options: VisibleAndPermissionIdOptions = {
  visible: true,
}

const res = await tatum.rpc.updateSetting(ownerAddress, contractAddress, consumeUserResourcePercent, options)

await tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}

### Overview

The `updateSetting` method is used to update the `consume_user_resource_percent` parameter of a smart contract on the TRON blockchain. This setting controls how much of a user's resource balance is consumed when they interact with the contract.

### Parameters

The following parameters are required for the `updateSetting` method:

* `ownerAddress` (string): Account address. Transaction creator's address, in hex string format.
* `contractAddress` (string): Contract address. The address of the contract to be modified, in hex string format.
* `consumeUserResourcePercent` (integer): User Energy Proportion. Consume user's resource percentage. It should be an integer between \[0, 100]. if 0, means it does not consume user's resource until the developer's resource has been used up.
* `options` (optional): Additional options
  * `visible` (boolean, optional): Whether the address is in base58 format.
  * `permission_id` (integer, optional): For multi-signature use.

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

Since the transaction type is `UpdateSettingContract`, the fields contained in `raw_data.contract[0].parameter.value` in the transaction are as follows:

* `owner_address` (string): Account address.
* `contract_address` (string): Contract address.
* `consume_user_resource_percent` (integer): User energy proportion.

### HTTP Request Example

```json
{
  "owner_address": "TSNEe5Tf4rnc9zPMNXfaTFKHSANinZseWnPcX",
  "contract_address": "TG3XXyExBkPp9nzdajDZsozEu4BkaSJozs",
  "consume_user_resource_percent": 10,
  "visible": true
}
```

### HTTP Response Example

```json
{
  "visible": true,
  "txID": "1bdf05c55b6034743aef2a02906b3a1bfd98832bf0dc35caa96ccf701de972a0",
  "raw_data": {
    "contract": [
      {
        "parameter": {
          "value": {
            "consume_user_resource_percent": 10,
            "owner_address": "TSNEe5Tf4rnc9zPMNXfaTF5fZfHDDH8oyW",
            "contract_address": "TG3XXyExBkPp9nzdajDZsozEu4BkaSJozs"
          },
          "type_url": "type.googleapis.com/protocol.UpdateSettingContract"
        },
        "type": "UpdateSettingContract"
      }
    ],
    "ref_block_bytes": "ea5d",
    "ref_block_hash": "049f1eb82a28ee3d",
    "expiration": 1684766970000,
    "timestamp": 1684766911523
  },
  "raw_data_hex": "0a02ea5d2208049f1eb82a28ee3d4090a1bf9f84315a6a082112660a32747970652e676f6f676c65617069732e636f6d2f70726f746f636f6c2e55706461746553657474696e67436f6e747261637412300a1541b3dcf27c251da9363f1a4888257c16676cf54edf12154142a1e39aefa49290f2b3f9ed688d7cecf86cd6e0180a70a3d8bb9f8431"
}
```
