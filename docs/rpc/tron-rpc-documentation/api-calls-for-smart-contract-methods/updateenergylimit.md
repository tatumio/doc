# updateenergylimit

### How to use it

{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Tron, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Tron>({network: Network.TRON})

const res = await tatum.rpc.updateEnergyLimit('TSNEe5Tf4rnc9zPMNXfaTF5fZfHDDH8oyW', 'TG3XXyExBkPp9nzdajDZsozEu4BkaSJozs', 100000000, {
visible: true,
})

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}

### Overview

`updateEnergyLimit` is a TRON RPC method used to update the `origin_energy_limit` parameter of a smart contract. The `origin_energy_limit` is a required parameter for deploying new contracts with a value larger than 0.

Use cases:

* Deploying new smart contracts
* Updating the energy limit for existing smart contracts

### Parameters

* `ownerAddress` (string): Account address of the transaction creator, in hex string format.
* `contractAddress` (string): Address of the contract to be modified, in hex string format.
* `originEnergyLimit` (integer): The maximum energy set by the creator. This refers to the greatest amount of energy the creator consumes during contract execution or creation process.
* `options` (object, optional): Additional options.
  * `visible` (boolean, optional): Specifies if the address is in base58 format.
  * `permission_id` (integer, optional): Used for multi-signature.

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

Since the transaction type is `UpdateEnergyLimitContract`, the fields contained in `raw_data.contract[0].parameter.value` in the transaction are as follows:

* `owner_address` (string): Account address.
* `contract_address` (string): Contract address.
* `origin_energy_limit` (string): Adjusted upper limit of energy provided by smart contract deployers in one transaction.

### HTTP Request Example

```json
{
  "owner_address": "TSNEe5Tf4rnc9zPMNXfaTF5fZfHDDH8oyW",
  "contract_address": "TG3XXyExBkPp9nzdajDZsozEu4BkaSJozs",
  "origin_energy_limit": 100000000,
  "visible": true
}
```

### HTTP Response Example

A successful response will return a `200` status code.

```json
{
  "visible": true,
  "txID": "158a188799ab507e9a4a5d673250c5e1b3ab3f8722ae9778be87c3087fc36453",
  "raw_data": {
    "contract": [
      {
        "parameter": {
          "value": {
            "owner_address": "TSNEe5Tf4rnc9zPMNXfaTF5fZfHDDH8oyW",
            "origin_energy_limit": 100000000,
            "contract_address": "TG3XXyExBkPp9nzdajDZsozEu4BkaSJozs"
          },
          "type_url": "type.googleapis.com/protocol.UpdateEnergyLimitContract"
        },
        "type": "UpdateEnergyLimitContract"
      }
    ],
    "ref_block_bytes": "ee2f",
    "ref_block_hash": "f408ae3f40e49e07",
    "expiration": 1684770300000,
    "timestamp": 1684770243112
  },
  "raw_data_hex": "0a02ee2f2208f408ae3f40e49e0740e0c08aa184315a71082d126d0a36747970652e676f6f676c65617069732e636f6d2f70726f746f636f6c2e557064617465456e657267794c696d6974436f6e747261637412330a1541b3dcf27c251da9363f1a4888257c16676cf54edf12154142a1e39aefa49290f2b3f9ed688d7cecf86cd6e01880c2d72f70a88487a18431"
}
```
