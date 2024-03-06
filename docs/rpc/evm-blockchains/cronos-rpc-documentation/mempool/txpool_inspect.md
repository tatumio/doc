# txpool\_inspect

### How to use it

{% tabs %}
{% tab title="TypeScript/JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Cronos, Network } from '@tatumio/tatum'
  
const tatum = await TatumSDK.init<Cronos>({network: Network.CRONOS})

const inspect = await tatum.rpc.txPoolInspect()

await tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Overview

The `txpool_inspect` method is a JSON-RPC method used to inspect the current transaction pool of a running node. The method allows you to view all pending transactions and their details, including transaction hashes, gas prices, and transaction data. This method is useful for developers who want to monitor the status of pending transactions or debug transaction-related issues.

### Parameters

The `txpool_inspect` method takes one optional parameter:

* **`include`**: A string specifying the type of transactions to include in the response. Possible values are **`pending`** (default) and **`queued`**.

### Return Object

The `txpool_inspect` method returns an object with the following fields:

* **`pending`**: An array of transaction objects, with textual data
* **`queued`**: An array of transaction objects, with textual data