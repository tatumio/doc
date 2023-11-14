# freezebalancev2

### How to use it

{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum
import { TatumSDK, Tron, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Tron>({network: Network.TRON})

const res = await tatum.rpc.freezeBalanceV2('TZ4UXDV5ZhNW7fb2AMSbgfAEZ7hWsnYS2g', 10000000, 'ENERGY', {
  visible: true,
})

await tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}

### Overview

The `freezeBalanceV2` method is a feature of Stake2.0 on the TRON blockchain. It allows you to stake a specific amount of TRX to obtain bandwidth or energy, and in return, you receive an equivalent amount of TRON Power (TP) according to the staked amount. This method can be useful in various use cases, such as securing network resources or participating in network governance by voting with TRON Power.

### Parameters

* `ownerAddress`(string):  The account address in default hexString format.
* `frozenBalance`(integer):  The amount of TRX to stake, in sun units.
* `resource`(string): The type of TRX stake, either 'BANDWIDTH' or 'ENERGY'.
* `options` (object, optional): This optional parameter contains the following properties:
  * `permissionId`(integer, optional): This is used for multi-signature transactions.
  * `visible`(string, optional):. Default is false. This parameter indicates whether addresses are in base58check format.

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

Since the transaction type is FreezeBalanceV2Contract, the fields contained in `raw_data.contract[0].parameter.value` in the transaction are as follows:

* `owner_address`: The account address.
* `resource`: The resource type.
* `frozen_balance`: The staked amount in sun units.



### HTTP Request Example

Here is an example of a CURL request to the `freezeBalanceV2` method:

```json
{
  "owner_address": "TZ4UXDV5ZhNW7fb2AMSbgfAEZ7hWsnYS2g",
  "frozenBalance": 1000000,
  "resource": "BANDWIDTH",
  "visible": true
}
```

### HTTP Response Example

The response to a successful request is a `200 OK` status code, and it returns the transaction object. If the request fails, you will receive a `400 Bad Request` status code with an error message.
