# getOffers

## How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, Stellar, Network } from '@tatumio/tatum';

// Initialize the Tatum SDK for Stellar
const tatum = await TatumSDK.init<Stellar>({ network: Network.STELLAR });

// Define parameters (Replace placeholders with actual values and remove redundant)
const params = {
    sponsor: 'SPONSOR_ADDRESS',
    seller: 'SELLER_ADDRESS',
    sellingAssetType: 'ASSET_TYPE',
    sellingAssetIssuer: 'ASSET_ISSUER',
    sellingAssetCode: 'ASSET_CODE',
    buyingAssetType: 'ASSET_TYPE',
    buyingAssetIssuer: 'ASSET_ISSUER',
    buyingAssetCode: 'ASSET_CODE',
    cursor: 'YOUR_CURSOR',
    order: 'asc',
    limit: 10
};

// List all open offers
const allOffers = await tatum.rpc.getOffers(params);

// Always destroy the Tatum SDK instance when done to stop any background processes
await tatum.destroy();
```

## Overview

The `getOffers` method allows you to list all currently open offers on the Stellar blockchain.

## Example use cases:

1. **Offer Monitoring:**
   Developers and applications can use this method to monitor and retrieve information about all open offers on the Stellar network.

2. **Offer Filtering:**
   Platform administrators can filter and search for specific offers based on various criteria, such as asset type, issuer, code, seller, and more.

3. **Streaming Offers:**
   Users can use streaming mode to listen for new offers as they are added to the Stellar ledger.

## Request Parameters

The `getOffers` method accepts the following optional parameters:

- `sponsor` (string, optional):
  Filter by the sponsor of the offer.

- `seller` (string, optional):
  Filter by the seller of the offer.

- `sellingAssetType` (string, optional):
  Filter by the selling asset type.

- `sellingAssetIssuer` (string, optional):
  Filter by the selling asset issuer.

- `sellingAssetCode` (string, optional):
  Filter by the selling asset code.

- `buyingAssetType` (string, optional):
  Filter by the buying asset type.

- `buyingAssetIssuer` (string, optional):
  Filter by the buying asset issuer.

- `buyingAssetCode` (string, optional):
  Filter by the buying asset code.

- `cursor` (string, optional):
  An optional cursor to start listing offers from a specific point.

- `order` (string, optional):
  An optional parameter to specify the order of listing (asc or desc). If not provided, it defaults to 'asc'.

- `limit` (number, optional):
  An optional parameter to specify the maximum number of offers to return. The limit can range from 1 to 200.

## Return Object

The `getOffers` method returns an array of open offers on the Stellar blockchain. Each offer object contains information such as the offer ID, sponsor, seller, buying asset, selling asset, and more.

(Note: The exact fields in the return object might vary based on the Stellar blockchain's implementation and version.)
