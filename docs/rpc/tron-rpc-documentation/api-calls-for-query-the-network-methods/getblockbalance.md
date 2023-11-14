# getblockbalance

### How to use it

{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @@tatumio/tatum
import { TatumSDK, Tron, Network, BigNumber } from '@tatumio/tatum'
import BigNumber from "bignumber.js";

const tatum = await TatumSDK.init<Tron>({network: Network.TRON})

const res = await tatum.rpc.getBlockBalance('00000000032669d53545fc1becc4d0cc9287e6324fb3a9230103aa0922f84544', new BigNumber(52849109), { visible: true })

await tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}

### Overview

The `getBlockBalance` RPC method retrieves all balance change operations in a specific block. This method is useful for tracking transactional changes and balances within a given block. At present, the interface data can only be queried through specific official nodes (47.241.20.47, 161.117.85.97, 161.117.224.116, 161.117.83.38).

### Parameters

* `hash` (string): The hash of the block for which you want to get the balance change operations. For example: '0000000001f5b9ca67c722d9263879696c92e8e383d4f0b31c15a91b8a249029'.
* `number` (integer): The number of the block for which you want to get the balance change operations. For example: 32881098.
* `options` (object, optional): This optional parameter contains the following properties:
  * `visible` (boolean, optional): Whether the address is in base58 format.

### Return Object

The method returns an object with the following properties:

* `timestamp` (integer): The timestamp of the block.
* `block_identifier.hash` (string): The hash of the block.
* `block_identifier.number` (integer): The number of the block.
* `transaction_balance_trace` (TransactionBalanceTrace\[]): An array of transaction information with balance changes. Each TransactionBalanceTrace object contains:
  * `transaction_identifier` (string): The hash of the transaction.
  * `operation` (Operation\[]): An array of operations involved in the transaction. Each operation contains:
    * `operation_identifier` (integer): The identifier of the operation.
    * `address` (string): The address involved in the operation.
    * `amount` (integer): The amount of balance increase or decrease.
  * `type` (string): The type of the transaction.
  * `status` (string): The result of the transaction.

### HTTP Request Example

```json
{
  "hash": "0000000001f5b9ca67c722d9263879696c92e8e383d4f0b31c15a91b8a249029",
  "number": 32881098,
  "visible": true
}
```

### HTTP Response Example

```json
{
  "timestamp": 1630847456000,
  "block_identifier": {
    "hash": "0000000001f5b9ca67c722d9263879696c92e8e383d4f0b31c15a91b8a249029",
    "number": 32881098
  },
  "transaction_balance_trace": [
    {
      "transaction_identifier": "ea75b733582194c3c4da8a4c962c5c5a1dfabf525e8db300678b4d18b3adc7fa",
      "operation": [
        {
          "operation_identifier": 0,
          "address": "TKJUZBU4wFm5Vc3MJboGLp7MEeYQ9xEJGy",
          "amount": -1000000
        },
        {
          "operation_identifier": 1,
          "address": "TAUN6FwrnwwmaEqYcckffC7wYmbaS6cBiX",
          "amount": 1000000
        }
      ],
      "type": "TransferContract",
      "status": "SUCCESS"
    }
  ]
}
```
