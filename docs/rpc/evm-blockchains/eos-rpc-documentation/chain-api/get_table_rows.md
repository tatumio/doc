# get_table_rows

### Overview

The `get_table_rows` method retrieves rows from a specified table in a given smart contract on the EOS blockchain. This method is essential for developers and users who need to interact with and analyze the data stored in smart contract tables. It provides multiple filtering options, ensuring extensive flexibility in querying specific data.
{% tabs %}
{% tab title="TypeScript/JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}

```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Eos, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Eos>({ network: Network.EOS })

const response = await tatum.rpc.getTableRows({
  code: 'eosio.token',
  table: 'accounts',
  scope: 'eosio',
  limit: 10
})

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Example use cases:

1. **Smart Contract Data Interaction:**
   Developers may find this method critical for interacting with the data within the tables of a smart contract, allowing for effective management and analysis of stored data.

2. **Detailed Data Analysis:**
   Users can employ this method to conduct detailed data analysis, which is pivotal for optimizing data use in smart contracts and enhancing functionalities.

3. **Enhanced Query Flexibility:**
   The diverse filtering options of this method enable the querying of specific data according to user needs, ensuring efficient and effective data retrieval and interaction.

### Request Parameters

The `get_table_rows` method requires the following parameters in the request body:

- `code` (string, required): The name of the smart contract that controls the provided table.
- `table` (string, required): The name of the table to query.
- `scope` (string, required): The account to which this data belongs.
- `indexPosition` (string): Position of the index used; accepted parameters are primary, secondary, tertiary, fourth, fifth, sixth, seventh, eighth, ninth, tenth.
- `keyType` (string): The type of key specified by indexPosition (e.g., uint64_t or name).
- `encodeType` (string): The encoding type used.
- `lowerBound` (string): Filters results to return the first element that is not less than the provided value in set.
- `upperBound` (string): Filters results to return the first element that is greater than the provided value in set.
- `limit` (integer <int32>, default: 10): Limits the number of results returned.
- `reverse` (boolean, default: false): Reverses the order of returned results.
- `showPayer` (boolean, default: false): Shows RAM payer.

### Return Object

The `get_table_rows` method typically returns an object containing the requested rows from the specified table associated with the provided smart contract.

### JSON-RPC Request Example

```json
{
  "code": "eosio.token",
  "table": "accounts",
  "scope": "eosio",
  "limit": 10
}
```

### JSON-RPC Response Example

```json
{
  "rows": [
    {"30010000000000000000000000000000011030555d4db7b23b01000000000000000000000000003041000000000000000000000000000000000000000000000000000000000000000000"},
    {"c00e000000000000000000000000000000c0270900000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000"},
    {"002400000000000000000000000000000064000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000"},
    {"50330000000000000000000000000000004c040000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000"}
  ],
  "more": true,
  "next_key": "595056260442244752"
}
```