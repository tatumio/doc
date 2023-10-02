# get_activated_protocol_features

### Overview

The `get_activated_protocol_features` method retrieves the activated protocol features for a producer node in the EOS blockchain. This method is crucial for developers and block producers to identify and understand the protocol features activated on a node, ensuring proper configuration and management of producer nodes.
{% tabs %}
{% tab title="TypeScript/JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}

```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Eos, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Eos>({ network: Network.EOS })

const response = await tatum.rpc.getActivatedProtocolFeatures({
params: {
"lower_bound": 0,
"upper_bound": 100,
"limit": 2,
"search_by_block_num": true,
"reverse": false
}
})

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}
{% endtab %}
{% endtabs %}
### Example use cases:

1. **Producer Node Management:**
   Developers and block producers can utilize this method to analyze and manage the activated protocol features, ensuring the optimal configuration of producer nodes.

2. **Protocol Feature Exploration:**
   This method allows users and developers to explore and understand the activated protocol features on the blockchain, enhancing their interaction and experience with the EOS blockchain.

3. **Enhanced Feature Retrieval:**
   The method provides extensive filtering options for retrieving activated protocol features, enabling users to efficiently manage and interact with the protocol features.

### Request Parameters

The `getActivatedProtocolFeatures` method requires the following parameters in the request body:

* `params` (object, required): Defines the filters to retrieve the protocol features by.
  * `lowerBound` (integer): Lower bound.
  * `upperBound` (integer): Upper bound.
  * `limit` (integer, default: 10): The limit.
  * `searchByBlockNum` (boolean, required): Flag to indicate whether it has to search by block number.
  * `reverse` (boolean, required): Flag to indicate whether it has to search in reverse.

### Return Object 

The `get_activated_protocol_features` method returns an object with the following properties:

* `activated_protocol_features` (Array of strings, required): Variant type, an array of strings representing the activated protocol features.
* `more` (integer): Represents whether there are more activated protocol features to be fetched. If there's `more` activated protocol features than the input parameter limit requested, it returns the ordinal of the next activated protocol feature which was not returned, otherwise, it returns zero.

### JSON-RPC Request Example

```json
{
  "params": {
    "lower_bound": 0,
    "upper_bound": 100,
    "limit": 10,
    "search_by_block_num": true,
    "reverse": false
  }
}
```

### JSON-RPC Response Example

```json
{
  "activated_protocol_features": ["0a1b2c3d4e5f6789abcdef10", "1a2b3c4d5e6f7890abcdef01"],
  "more": 1
}
```