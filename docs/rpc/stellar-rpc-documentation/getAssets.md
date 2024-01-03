# getAssets

### How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, Stellar, Network } from '@tatumio/tatum';

// Initialize the Tatum SDK for Stellar
const tatum = await TatumSDK.init<Stellar>({ network: Network.STELLAR });

// Define input parameters as an object (Replace placeholders with actual values)
const inputParams = {
    assetCode: 'YOUR_ASSET_CODE', 
    assetIssuer: 'YOUR_ASSET_ISSUER', 
    cursor: 'YOUR_CURSOR', 
    order: 'asc', 
    limit: 10,
};

// Retrieve a list of all assets
const assets = await tatum.rpc.getAssets(inputParams);

// Log the list of assets
console.log('Assets:', assets);

// Always destroy the Tatum SDK instance when done to stop any background processes
await tatum.destroy();
```

### Overview

The `getAssets` method allows you to retrieve a list of all assets on the Stellar blockchain. You can use various filtering options to narrow down the asset list based on asset code, asset issuer, cursor for pagination, sorting order, and limit for the number of records to be returned.

### Request Parameters

The `getAssets` method accepts the following request parameters:

- `assetCode` (string, optional): 
  The asset code for filtering assets by code. Use this parameter to list assets with a specific code.

- `assetIssuer` (string, optional): 
  The asset issuer for filtering assets by issuer. Use this parameter to list assets issued by a specific account.

- `cursor` (string, optional): 
  A cursor value that determines the starting point for pagination. Use this parameter to retrieve assets from a specific point in the asset list.

- `order` (string, optional): 
  A designation of the order in which records should appear. Options include 'asc' (ascending) or 'desc' (descending). If this argument isn’t set, it defaults to 'asc'.

- `limit` (number, optional): 
  The maximum number of records returned. It defines the number of assets to fetch in a single request.

### Return Object

The `getAssets` method returns a JSON object containing the list of assets that match the specified criteria. Each asset is represented as an object with various properties describing its characteristics.

(Note: The exact fields in the return object might vary based on the Stellar blockchain's implementation and version.)
