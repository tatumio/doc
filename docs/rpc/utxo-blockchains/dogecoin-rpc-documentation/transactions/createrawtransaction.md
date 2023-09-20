# createrawtransaction

### How to use it

{% tabs %}
{% tab title="TypeScript/JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Dogecoin, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Dogecoin>({network: Network.DOGECOIN})

const result = await tatum.rpc.createRawTransaction([
      {
        "txid": "abcd1234abcd1234abcd1234abcd1234abcd1234abcd1234abcd1234abcd1234",
        "vout": 0
      }
    ],
    {
      "1A1zP1eP5QGefi2DMPTfTL5SLmv7DivfNa": 0.01
    })
    
tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Overview

{% embed url="https://codepen.io/Jan-Musil-the-lessful/pen/RwqdKPR?editors=1111" %}

The `createrawtransaction` RPC method creates an unsigned raw transaction that spends a set of previous transaction outputs to a set of new addresses with specific amounts. The method can be used to create custom transactions, which can then be signed and broadcast to the Dogecoin network.

### Parameters

* `inputs`: (array, required) An array of objects, each specifying a previous transaction output to spend.
  * `txid`: (string, required) The transaction ID of the previous transaction output to spend.
  * `vout`: (numeric, required) The index of the output to spend from the previous transaction.
  * `sequence`: (numeric, optional) default=depends on the value of the 'replaceable' and 'locktime' arguments) The sequence number
* `outputs`: (object, required) An object with the key-value pairs representing the receiving address and the amount to be sent (in BTC).
* `locktime`: (numeric, optional, default=0) The lock time for the transaction. It can be used to specify the earliest time or block height at which the transaction can be included in a block.
* `replaceable`: (boolean, optional, default=false) **Marks this transaction as BIP125-replaceable.** Allows this transaction to be replaced by a transaction with higher fees. If provided, it is an error if explicit sequence numbers are incompatible.

### Return Object

* (string) A hex-encoded raw transaction.

### JSON Examples

Request example:

{% code overflow="wrap" lineNumbers="true" %}
```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "createrawtransaction",
  "params": [
    [
      {
        "txid": "abcd1234abcd1234abcd1234abcd1234abcd1234abcd1234abcd1234abcd1234",
        "vout": 0
      }
    ],
    {
      "1A1zP1eP5QGefi2DMPTfTL5SLmv7DivfNa": 0.01
    }
  ]
}
```
{% endcode %}

Response example:

{% code overflow="wrap" lineNumbers="true" %}
```json
{
  "result": "02000000013412cdab3412cdab3412cdab3412cdab3412cdab3412cdab3412cdab3412cdab0000000000fdffffff0140420f00000000001976a91462e907b15cbf27d5425399ebf6f0fb50ebb88f1888ac00000000",
  "error": null,
  "id": 1
}

```
{% endcode %}

\
