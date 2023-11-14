# sendrawtransaction

### How to use it

{% tabs %}
{% tab title="TypeScript/JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Dogecoin, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Dogecoin>({network: Network.DOGECOIN})

const result = await tatum.rpc.sendRawTransaction("02000000013412cdab3412cdab3412cdab3412cdab3412cdab3412cdab3412cdab3412cdab0000000000fdffffff0140420f00000000001976a91462e907b15cbf27d5425399ebf6f0fb50ebb88f1888ac00000000")

await tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Overview

The `sendrawtransaction` method submits a serialized raw transaction to the Dogecoin network. If the transaction is well-formed and valid, it will be propagated to the network and included in a mined block.

This method is commonly used in conjunction with [`createrawtransaction`](../../bitcoin-rpc-documentation/transactions/createrawtransaction.md), or other methods to construct and sign raw transactions before broadcasting them.

### Parameters

The `sendrawtransaction` method accepts the following parameters:

* `hexstring`: A string representing the serialized raw transaction in hexadecimal format.

### Return Object

The `sendrawtransaction` method returns a string containing the transaction ID (txid) of the broadcasted transaction.

### JSON Examples

Request example:

{% code overflow="wrap" lineNumbers="true" %}
```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "sendrawtransaction",
  "params": ["02000000013412cdab3412cdab3412cdab3412cdab3412cdab3412cdab3412cdab3412cdab0000000000fdffffff0140420f00000000001976a91462e907b15cbf27d5425399ebf6f0fb50ebb88f1888ac00000000"]
}
```
{% endcode %}

Response example:

{% code overflow="wrap" lineNumbers="true" %}
```json
{
  "result": "c7ad51e46a39d136adc2bb7536a236136cc206ab3c8dabcd4277d4cadcf674f2",
  "error": null,
  "id": 1
}

```
{% endcode %}

\
