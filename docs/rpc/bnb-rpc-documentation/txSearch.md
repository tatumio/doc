# txSearch

### How to use it

```typescript
// Importing Tatum SDK for Binance Beacon Chain
import { TatumSDK, Network, Bnb } from '@tatumio/tatum';

// Initializing SDK for Binance Beacon Chain network
const tatum = await TatumSDK.init<Bnb>({ network: Network.BNB });

// Defining the search parameters
const searchParams = {
  query: 'QUERY_STRING',      // Replace with your query string (Required)
  prove: true,               // Include proofs of transaction inclusion in the block (true/false) (Required)
  page: '1',                   // Page number (1-based) (Optional)
  per_page: '10'               // Number of entries per page (max: 100) (Optional)
};

// Searching for transactions
const searchResults = await tatum.rpc.txSearch(searchParams);
console.log(searchResults);

// Destroy Tatum SDK - needed for stopping background jobs
tatum.destroy();
```

### Overview

The `txSearch` method is used to search for transactions on the BNB beacon chain that match specific search criteria.

### Parameters

- `query` (string, Required): The query string used to search for transactions.
- `prove` (boolean, Required): Include proofs of the transaction's inclusion in the block (true/false).
- `page` (string number, Optional): Page number for paginating results (1-based).
- `per_page` (string number, Optional): Number of entries per page (max: 100).

### Return Object

The method returns a JSON-RPC response containing information about the matching transactions. The response includes the following fields:

- `total_count` (string, Required): The total count of matching transactions.
  - Example: `2`
  
- `txs` (array, Required): An array of transaction objects.
  - Example: `[ ]`

(Note: The exact structure of the transaction objects and response may vary based on the BNB beacon chain's implementation and version.)