# getOfferTrades

## How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, Stellar, Network } from '@tatumio/tatum';

// Initialize the Tatum SDK for Stellar
const tatum = await TatumSDK.init<Stellar>({ network: Network.STELLAR });

// Define parameters (Replace placeholders with actual values)
const params = {
    offerId = 'OFFER_ID';
    cursor = 'YOUR_CURSOR';
    order = 'asc';
    limit = 10;
}
 
// Retrieve trades for a specific offer
const offerTrades = await tatum.rpc.getOfferTrades(params);

// Always destroy the Tatum SDK instance when done to stop any background processes
await tatum.destroy();
```

## Overview

The `getOfferTrades` method allows you to retrieve all trades associated with a specific offer by providing the offer's unique identifier.

## Example use cases:

1. **Trade Analysis:**
   Developers and applications can use this method to analyze and retrieve information about trades related to a specific offer on the Stellar network.

2. **Trade Monitoring:**
   Platform administrators can monitor and track trades associated with offers for auditing and management purposes.

3. **Streaming Trades:**
   Users can use streaming mode to listen for new trades related to the offer as they are added to the Stellar ledger.

## Request Parameters

The `getOfferTrades` method accepts the following optional parameters:

- `offerId` (string, required):
  The unique identifier of the offer for which you want to retrieve trades.

- `cursor` (string, optional):
  An optional cursor to start listing trades from a specific point.

- `order` (string, optional):
  An optional parameter to specify the order of listing (asc or desc). If not provided, it defaults to 'asc'.

- `limit` (number, optional):
  An optional parameter to specify the maximum number of trades to return. The limit can range from 1 to 200.

## Return Object

The `getOfferTrades` method returns an array of trades related to the specified offer on the Stellar blockchain. Each trade object contains information such as the trade ID, seller, buyer, price, and more.

(Note: The exact fields in the return object might vary based on the Stellar blockchain's implementation and version.)
