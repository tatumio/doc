# getAssetBalances

### How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, AlgorandIndexer, Network } from '@tatumio/tatum';

// Initialize the Tatum SDK
const tatum = await TatumSDK.init<AlgorandIndexer>({ network: Network.ALGORAND_INDEXER });

// Define the input parameters as a dictionary object
const params = {
    assetId: 123,               // Specify the asset ID (number) for which you want to lookup balances.
    currencyGreaterThan: 100,  // Optional: Results should have an amount greater than this value (number).
    currencyLessThan: 500,     // Optional: Results should have an amount less than this value (number).
    includeAll: true,          // Optional: Include all items, including closed accounts, deleted applications, destroyed assets, opted-out asset holdings, and closed-out application localstates (boolean).
    limit: 100,                // Optional: Maximum number of results to return (number).
    next: 'NEXT_PAGE_TOKEN'     // Optional: The next page of results. Use the next token provided by the previous results (string).
};

// Lookup the list of accounts holding the specified asset
const assetBalances = await tatum.rpc.getAssetBalances(params);

// Log the list of accounts and their asset balances
console.log('Asset Balances:', assetBalances);

// Always destroy the Tatum SDK instance when done to stop any background processes
await tatum.destroy();
```

### Overview

The `getAssetBalances` method allows you to lookup the list of accounts that hold a specific asset.

### Example Use Cases

1. **Asset Balances**: Developers can use this method to retrieve a list of accounts holding a particular asset, with optional filters for currency amounts.

### Request Parameters

The `getAssetBalances` method requires the following parameters:

- `assetId` (number, required): Specify the asset ID for which you want to lookup balances.
- `currencyGreaterThan` (number, optional): Results should have an amount greater than this value (number).
- `currencyLessThan` (number, optional): Results should have an amount less than this value (number).
- `includeAll` (boolean, optional): Include all items, including closed accounts, deleted applications, destroyed assets, opted-out asset holdings, and closed-out application localstates (boolean).
- `limit` (number, optional): Maximum number of results to return (number).
- `next` (string, optional): The next page of results. Use the next token provided by the previous results (string).

### Return Object

The method returns a list of accounts holding the specified asset, along with their asset balances. 

Please note that the structure of the returned object may change in different RPC versions.