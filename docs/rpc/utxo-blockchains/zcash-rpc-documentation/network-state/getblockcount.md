# getblockcount

### How to use it

{% tabs %}
{% tab title="TypeScript/JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, ZCash, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<ZCash>({network: Network.ZCASH})

const result = await tatum.rpc.getBlockCount()

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Overview

`getblockcount` is a method that returns the number of blocks in the local best blockchain. This method is useful for obtaining the current height of the blockchain, which can be used for various purposes, such as monitoring the blockchain, determining the number of confirmations for a transaction, or assessing the progress of the blockchain's growth.

{% embed url="https://codepen.io/tatum-devrel/pen/xxQMMrQ" %}

### Parameters

This method does not have any parameters.

### Return Object

The returned object is an integer representing the number of blocks in the local best blockchain.

### JSON Examples

Request example:

{% code overflow="wrap" lineNumbers="true" %}
```json
{
  "id": 1,
  "jsonrpc": "2.0",
  "method": "getblockcount"
}
```
{% endcode %}

Response example:

{% code overflow="wrap" lineNumbers="true" %}
```json
{
    "result": 787067,
    "error": null,
    "id": 1
}
```
{% endcode %}

\
