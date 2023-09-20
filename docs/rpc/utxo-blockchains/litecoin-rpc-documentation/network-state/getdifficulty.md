# getdifficulty

### How to use it

{% tabs %}
{% tab title="TypeScript/JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Litecoin, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Litecoin>({network: Network.LITECOIN})

const result = await tatum.rpc.getDifficulty()

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Overview

`getdifficulty` is a Litecoin RPC method that returns the current mining difficulty. The mining difficulty is a measure of how difficult it is to find a new block compared to the easiest it can ever be. This method can be used to monitor the mining difficulty, which adjusts every 2016 blocks to maintain a consistent block creation rate of approximately 10 minutes per block.

{% embed url="https://codepen.io/tatum-devrel/pen/qBQvbxp" %}

### Parameters

This method does not require any parameters.

### Return Object

A return object is a floating-point number that represents the current mining difficulty.

### JSON Examples

Request example:

{% code overflow="wrap" lineNumbers="true" %}
```json
{
  "jsonrpc": "2.0",
  "method": "getdifficulty",
  "id": 1
}
```
{% endcode %}

Response example:

{% code overflow="wrap" lineNumbers="true" %}
```json
{
    "result": 48712405953118.43,
    "error": null,
    "id": 1
}
```
{% endcode %}

\
