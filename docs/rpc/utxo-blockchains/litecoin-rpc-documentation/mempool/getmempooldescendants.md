# getmempooldescendants

### How to use it

{% tabs %}
{% tab title="TypeScript/JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Litecoin, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Litecoin>({network: Network.LITECOIN})

const result = await tatum.rpc.getMempoolDescendants("3b3c3bc559deddb0991e1fe9fb6d9f10c1c4a0dab4a18c12e8566b37ad4f06e4")

await tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Overview

The `getmempooldescendants` RPC method allows you to retrieve information about the descendant transactions of a specified transaction in the memory pool. This method is useful for understanding the relationships between unconfirmed transactions and the possible effects of their confirmation on the overall transaction fees and network congestion.

### Parameters

* `txid`: (string, required) The transaction ID of the transaction for which you want to get its descendants.
* `verbose`: (boolean, optional, default=`false`) If set to `true`, detailed information about each descendant transaction will be returned, otherwise only the transaction IDs will be returned.

### Return Object

The return object depends on the `verbose` parameter:

* If `verbose` is `false`, the return object is an array of strings, each representing the transaction ID of a descendant.
* If `verbose` is `true`, the return object is a JSON object, where the keys are the transaction IDs of the descendants, and the values are JSON objects containing detailed information about the descendants.

### JSON Examples

Request example:

{% code overflow="wrap" lineNumbers="true" %}
```json
{
  "id": 1,
  "jsonrpc": "2.0",
  "method": "getmempooldescendants",
  "params": [
    "3b3c3bc559deddb0991e1fe9fb6d9f10c1c4a0dab4a18c12e8566b37ad4f06e4"
  ]
}

```
{% endcode %}

Response example:

{% code overflow="wrap" lineNumbers="true" %}
```json
{
  "id": 1,
  "result": [
    "1d1c1bc9a9a7d7b0990e0e1f1b5b5a5a5c5b5a5a5a5a5a5a5a5a5a5a5a5a5a5a"
  ]
}

```
{% endcode %}

\
