# getAsset

### How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, Algorand, Network } from '@tatumio/tatum';

// Initialize the Tatum SDK for Algorand
const tatum = await TatumSDK.init<Algorand>({ network: Network.ALGORAND });

// Define the input parameters in a single object
const params = {
    assetId: 123,  // Specify the asset ID for which you want to retrieve information.
};

// Retrieve the asset information for the specified asset ID
const assetInfo = await tatum.rpc.getAsset(params);

// Log the asset information
console.log('Asset Information:', assetInfo);

// Always destroy the Tatum SDK instance when done to stop any background processes
tatum.destroy();
```

### Overview

The `getAsset` method allows you to retrieve asset information, including creator, name, total supply, and special addresses, for a specific asset ID.

### Example Use Cases

1. **Asset Details**: Developers can use this method to retrieve detailed information about a specific asset, including the address of the asset's creator, the name of the asset, the total supply of the asset, and any special addresses associated with the asset.

### Request Parameters

The `getAsset` method requires the following parameter:

- `assetId` (integer, required): An asset identifier representing the asset for which you want to retrieve information.

### Return Object

The method returns an object representing the asset information for the specified asset ID. The returned object includes details such as the asset's creator, name, total supply, and special addresses.

Please note that the structure of the returned object may change in different Algorand RPC versions.