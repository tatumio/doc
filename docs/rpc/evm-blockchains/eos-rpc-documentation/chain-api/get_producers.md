# get_producers

### Overview

The `get_producers` method is designed to retrieve a list of producers from the EOS blockchain. Producers are essential entities in the EOS network responsible for producing blocks, and this method provides valuable insights into their details and statuses, including active, pending, and proposed producers. 

{% tabs %}
{% tab title="TypeScript/JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}

```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Eos, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Eos>({ network: Network.EOS })

const response = await tatum.rpc.getProducers({
  limit: '10',
  lower_bound: '0',
  json: true
})

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Example use cases:

1. **Monitoring Network Health:**
   Developers and network monitors can use the `get_producers` method to observe the active, pending, and proposed producers, assessing the overall health and consensus of the network.

2. **Network Statistics:**
   This method aids in gathering statistical data about the network, including the number and statuses of producers, facilitating enhanced network analysis and management.

3. **Voting and Governance:**
   `get_producers` can be instrumental for users involved in EOS governance, helping them to make informed decisions by providing a current list of producers along with their statuses.

### Request Parameters

The `get_producers` method requires the following parameters in the request body:

- `limit` (string, required): The total number of producers to retrieve.
- `lowerBound` (string, required): In conjunction with limit, it can be used to paginate through the results. For example, limit=10 and lower_bound=10 would represent page 2.
- `json` (boolean, required): Indicates whether the result should be returned in JSON format.

### Return Object

The `getProducers` method typically returns an object containing lists of active, pending, and proposed producers:

- `active` (Array of objects, nullable): A list of currently active producers.
- `pending` (Array of objects, nullable): A list of producers that are pending.
- `proposed` (Array of objects, nullable): A list of producers that are proposed.

### JSON-RPC Request Example

```json
{
  "limit": "10",
  "lower_bound": "0",
  "json": true
}
```

### JSON-RPC Response Example

```json
{
  "active": [...],
  "pending": [...],
  "proposed": [...]
}
```