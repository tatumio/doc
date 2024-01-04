# getLedgers

### How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, Stellar, Network } from '@tatumio/tatum';

// Initialize the Tatum SDK for Stellar
const tatum = await TatumSDK.init<Stellar>({ network: Network.STELLAR });

// Define optional parameters for listing ledgers (Replace placeholders with actual values and remove redundant)
const params = {
    cursor: 'YOUR_CURSOR',
    order: 'asc',
    limit: 10
};

// List all ledgers or stream new ledgers as they close
const ledgers = await tatum.rpc.getLedgers(params);

// Log the list of ledgers
console.log('Ledgers:', ledgers);

// Always destroy the Tatum SDK instance when done to stop any background processes
await tatum.destroy();
```

### Overview

The `getLedgers` method allows you to retrieve a list of all ledgers on the Stellar blockchain. You can use this endpoint to either list all existing ledgers or stream new ledgers as they are created.

### Request Parameters

The `getLedgers` method supports the following optional request parameters:

- `cursor` (string, optional): 
  Set the cursor to start listing ledgers from a specific ledger. If not specified, it starts from the earliest known ledger.

- `order` (string, optional): 
  Set the order of listing, which can be either 'asc' (ascending) or 'desc' (descending). If not specified, it defaults to 'asc'.

- `limit` (integer, optional): 
  Set the maximum number of ledgers to return in a single request. The limit can range from 1 to an upper limit hardcoded in Horizon for performance reasons. If not specified, it defaults to 10.

### Return Object

The `getLedgers` method returns a JSON object representing a list of ledgers on the Stellar blockchain. Each ledger entry includes various properties describing the ledger's characteristics, such as its sequence number, transaction count, and more.

(Note: The exact fields in the return object might vary based on the Stellar blockchain's implementation and version.)