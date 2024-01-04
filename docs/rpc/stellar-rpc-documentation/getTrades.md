# listTrades

### How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, Stellar, Network } from '@tatumio/tatum';

// Initialize the Tatum SDK for Stellar
const tatum = await TatumSDK.init<Stellar>({ network: Network.STELLAR });

// Define input parameters as an object (Replace placeholders with actual values and remove redundant)
const params = {
    offerId: 'YOUR_OFFER_ID',
    baseAssetType: 'YOUR_BASE_ASSET_TYPE',
    baseAssetIssuer: 'YOUR_BASE_ASSET_ISSUER',
    baseAssetCode: 'YOUR_BASE_ASSET_CODE',
    counterAssetType: 'YOUR_COUNTER_ASSET_TYPE',
    counterAssetIssuer: 'YOUR_COUNTER_ASSET_ISSUER',
    counterAssetCode: 'YOUR_COUNTER_ASSET_CODE',
    tradeType: 'YOUR_TRADE_TYPE',
    cursor: 'YOUR_CURSOR',
    order: 'YOUR_ORDER',
    limit: 10
};

// List all trades or use streaming mode to listen for new trades
const trades = await tatum.rpc.listTrades(params);

// Log the list of trades
console.log('Trades:', trades);

// Always destroy the Tatum SDK instance when done to stop any background processes
await tatum.destroy();
```

### Overview

The `listTrades` method allows you to list all trades on the Stellar blockchain. You can also use streaming mode to listen for new trades as they are added to the Stellar ledger. When called in streaming mode, Horizon will start at the earliest known trade unless a cursor is set, in which case it will start from that cursor.

### Request Parameters

The `listTrades` method accepts the following request parameters:

- `offerId` (string, optional):
  The identifier of the offer to filter trades. Use this parameter to list trades for a specific offer.

- `baseAssetType` (string, optional):
  The asset type of the base asset to filter trades. Use this parameter to filter trades by the base asset type.

- `baseAssetIssuer` (string, optional):
  The issuer account of the base asset to filter trades. Use this parameter to filter trades by the base asset issuer.

- `baseAssetCode` (string, optional):
  The asset code of the base asset to filter trades. Use this parameter to filter trades by the base asset code.

- `counterAssetType` (string, optional):
  The asset type of the counter asset to filter trades. Use this parameter to filter trades by the counter asset type.

- `counterAssetIssuer` (string, optional):
  The issuer account of the counter asset to filter trades. Use this parameter to filter trades by the counter asset issuer.

- `counterAssetCode` (string, optional):
  The asset code of the counter asset to filter trades. Use this parameter to filter trades by the counter asset code.

- `tradeType` (string, optional):
  The type of trade to filter. Use this parameter to filter trades by trade type.

- `cursor` (string, optional):
  A cursor value that determines the starting point for pagination. Use this parameter to retrieve trades from a specific point in the list.

- `order` (string, optional):
  A designation of the order in which records should appear. Options include 'asc' (ascending) or 'desc' (descending). If this argument isn’t set, it defaults to 'asc'.

- `limit` (number, optional):
  The maximum number of records returned. It defines the number of trades to fetch in a single request.

### Response

The `listTrades` method returns a JSON object containing the list of trades that match the specified criteria. Each trade is represented as an object with various properties describing its characteristics.

(Note: The exact fields in the return object might vary based on the Stellar blockchain's implementation and version.)
