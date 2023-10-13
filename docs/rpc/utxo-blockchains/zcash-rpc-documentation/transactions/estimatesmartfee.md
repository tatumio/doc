# estimatesmartfee

### How to use it

{% tabs %}
{% tab title="TypeScript/JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, ZCash, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<ZCash>({network: Network.ZCASH})

const result = await tatum.rpc.estimateSmartFee(20)

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Overview

The `estimatesmartfee` method provides an estimated fee rate for a transaction to be confirmed within a certain number of blocks. The estimation is based on recent transactions in the network.

This method can be useful for users or applications trying to decide on an appropriate fee for their transactions, based on the desired confirmation speed.

### Parameters

The `estimatesmartfee` method accepts the following parameters:

* `conf_target`: An integer representing the number of blocks within which the transaction should be confirmed.
* `estimate_mode` _(optional)_: A string that determines the estimation mode. Possible values are "UNSET", "ECONOMICAL", and "CONSERVATIVE". Default is "CONSERVATIVE".

### Return Object

The `estimatesmartfee` method returns an object containing the following fields:

* `feerate`: A decimal number representing the estimated fee rate/kB.
* `blocks`: An integer representing the number of blocks within which the transaction is expected to be confirmed.

### JSON Examples

Request example:

{% code overflow="wrap" lineNumbers="true" %}
```json
{
  "jsonrpc": "2.0",
  "method": "estimatesmartfee",
  "params": [20],
  "id": 1
}
```
{% endcode %}

Response example:

{% code overflow="wrap" lineNumbers="true" %}
```json
{
    "result": {
        "feerate": 0.00017258,
        "blocks": 20
    },
    "error": null,
    "id": 1
}
```
{% endcode %}

\
