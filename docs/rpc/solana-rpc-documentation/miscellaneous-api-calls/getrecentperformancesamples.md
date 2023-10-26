# getRecentPerformanceSamples

### How to Use It

{% code overflow="wrap" lineNumbers="true" %}
```javascript
// yarn add @tatumio/tatum

import { TatumSDK, Solana, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Solana>({ network: Network.SOLANA })

const res = await tatum.rpc.getRecentPerformanceSamples(limit)

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}

### Overview

The `getRecentPerformanceSamples` method returns a list of recent performance samples, in reverse slot order. Performance samples are taken every 60 seconds and include the number of transactions and slots that occur in a given time window. This data can be used to monitor network performance and understand the activity within the Solana network.

{% embed url="https://codepen.io/Night-Shift-Dev/pen/poQbeqp" %}

### Parameters

* `limit` (usize, optional): The number of samples to return (maximum 720).

### Return Object

The result will be an array of objects with the following fields:

* `slot`: Slot in which sample was taken at.
* `numTransactions`: Number of transactions in sample.
* `numSlots`: Number of slots in sample.
* `samplePeriodSecs`: Number of seconds in a sample window.
* `numNonVoteTransaction`: Number of non-vote transactions in sample.

Note: `numNonVoteTransaction` is present starting with v1.15. To get the number of voting transactions, compute: numTransactions - numNonVoteTransaction.

### JSON-RPC Request Example

```json
{
  "jsonrpc":"2.0",
  "id":1,
  "method":"getRecentPerformanceSamples",
  "params": [4]
}
```

### JSON-RPC Response Example

```json
{
  "jsonrpc": "2.0",
  "result": [
    {
      "numSlots": 126,
      "numTransactions": 126,
      "numNonVoteTransaction": 1,
      "samplePeriodSecs": 60,
      "slot": 348125
    },
    {
      "numSlots": 126,
      "numTransactions": 126,
      "numNonVoteTransaction": 1,
      "samplePeriodSecs": 60,
      "slot": 347999
    },
    {
      "numSlots": 125,
      "numTransactions": 125,
      "numNonVoteTransaction": 0,
      "samplePeriodSecs": 60,
      "slot": 347873
    },
    {
      "numSlots": 125,
      "numTransactions": 125,
      "numNonVoteTransaction": 0,
      "samplePeriodSecs": 60,
      "slot": 347748
    }
  ],
  "id": 1
}
```
