# getAsset

### How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, Algorand, Network } from '@tatumio/tatum';

// Initialize the Tatum SDK
const tatum = await TatumSDK.init<AlgorandIndexer>({ network: Network.ALGORAND_INDEXER });

// Define the input parameters as a dictionary object
const params = {
    assetId: 123,               // Specify the asset ID (number) for which you want to lookup asset information.
    includeAll: true            // Optional: Include all items, including closed accounts, deleted applications, destroyed assets, opted-out asset holdings, and closed-out application localstates (boolean).
};

// Lookup asset information
const assetInfo = await tatum.rpc.getAsset(params);

// Log the asset information
console.log('Asset Information:', assetInfo);

// Always destroy the Tatum SDK instance when done to stop any background processes
tatum.destroy();
```

### Overview

The `getAsset` method allows you to lookup information for a specific asset.

### Example Use Cases

1. **Asset Lookup**: Developers can use this method to retrieve detailed information about a specific asset.

### Request Parameters

The `getAsset` method requires the following parameters, all included in the `params` dictionary object:

- `assetId` (number, required): Specify the asset ID for which you want to lookup asset information.
- `includeAll` (boolean, optional): Include all items, including closed accounts, deleted applications, destroyed assets, opted-out asset holdings, and closed-out application localstates (boolean).

### Return Object

The method returns an object representing the detailed information of the specified asset, including its properties. 

Please note that the structure of the returned object may change in different RPC versions.