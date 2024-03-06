# txpool\_status

### How to use it

{% tabs %}
{% tab title="TypeScript/JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Cronos, Network } from '@tatumio/tatum'
  
const tatum = await TatumSDK.init<Cronos>({network: Network.CRONOS})

const status = await tatum.rpc.txPoolStatus()

await tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Overview

The `txpool_status` method returns statistics about the current state of the transaction pool. The transaction pool is a queue of pending transactions waiting to be included in the next block by miners.

This method can be useful for monitoring the health of the network and analyzing the behavior of the miners. It can also be used to estimate the time it will take for a transaction to be processed, as well as to determine the gas price necessary to ensure prompt inclusion of a transaction in the next block.

### Parameters

This method does not take any parameters.

### Return Object

The `txpool_status` method returns an object with the following fields:

* **`pending`**: Number of pending transactions in the pool
* **`queued`**: Number of queued transactions in the pool