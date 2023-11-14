# get_table_by_scope

### Overview

The `get_table_by_scope` method retrieves the table scope for a given contract in the EOS blockchain. It is essential for developers and users who interact with smart contracts and need to query table data associated with a specific contract. This method provides flexibility by allowing filtered and limited results, making it highly adaptable to various use cases.
{% tabs %}
{% tab title="TypeScript/JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}

```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Eos, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Eos>({ network: Network.EOS })

const response = await tatum.rpc.getTableByScope({
  code: 'eosio.token',
  table: 'accounts',
  lowerBound: '0',
  upperBound: '100',
  limit: 10,
  reverse: false,
  show_payer: false
})

await tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Example use cases:

1. **Smart Contract Interaction:**
   Developers can use this method to interact with and retrieve table data for a specific contract, which is crucial for accurate and efficient contract interaction and validation.

2. **Data Analysis and Management:**
   By retrieving table scope, users and developers can perform detailed data analysis and management, which aids in optimizing and improving smart contract functionalities.

3. **Enhanced Querying:**
   The flexible filtering options provided by this method facilitate enhanced querying capabilities, allowing users to retrieve precise and relevant data according to their requirements.

### Request Parameters

The `getTableByScope` method requires the following parameters in the request body:

- `code` (string, required): The name of the contract to return table data for.
- `table` (string): To filter the results by table.
- `lowerBound` (string): Filters results to return the first element that is not less than the provided value in set.
- `upperBound` (string): Filters results to return the first element that is greater than the provided value in set.
- `limit` (integer <int32>, default: 10): Limit the number of results returned.
- `reverse` (boolean, default: false): Reverse the order of returned results.
- `showPayer` (boolean, default: false): Show RAM payer.

### Return Object

The `get_table_by_scope` method typically returns an array containing the requested table scope details related to the specified contract.

### JSON-RPC Request Example

```json
{
  "code": "eosio.token",
  "table": "accounts",
  "lower_bound": "0",
  "upper_bound": "100",
  "limit": 10,
  "reverse": false,
  "show_payer": false
}
```

### JSON-RPC Response Example

```json
{
    "rows": [
        {
            "code": "eosio.token",
            "scope": "........ehbo5",
            "table": "stat",
            "payer": "eosio.token",
            "count": 1
        }
    ],
    "more": "111222333445"
}
```