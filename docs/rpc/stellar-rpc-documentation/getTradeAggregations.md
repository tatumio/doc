# getTradeAggregations

### How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, Stellar, Network } from '@tatumio/tatum';

// Initialize the Tatum SDK for Stellar
const tatum = await TatumSDK.init<Stellar>({ network: Network.STELLAR });

// Define parameters (Replace placeholders with actual values and remove redundant)
const params = {
    startTime: 'START_TIME',
    endTime: 'END_TIME',
    resolution: 'RESOLUTION',
    offset: 'OFFSET',
    baseAssetType: 'BASE_ASSET_TYPE',
    baseAssetIssuer: 'BASE_ASSET_ISSUER',
    baseAssetCode: 'BASE_ASSET_CODE',
    counterAssetType: 'COUNTER_ASSET_TYPE',
    counterAssetIssuer: 'COUNTER_ASSET_ISSUER',
    counterAssetCode: 'COUNTER_ASSET_CODE',
    order: 'asc',
    limit: 10
};

// List trade aggregations
const tradeAggregations = await tatum.rpc.getTradeAggregations(params);

// Always destroy the Tatum SDK instance when done to stop any background processes
await tatum.destroy();
```

### Overview

The `getTradeAggregations` method allows you to list trade data based on filters set in the arguments. It divides a given time range into segments and aggregates statistics for a given asset pair (base, counter) over each of these segments. The duration of the segments is specified with the `resolution` parameter. The `startTime` and `endTime` parameters define the start and end of the time range, which are both rounded to the nearest multiple of `resolution` since epoch. The individual segments are also aligned with multiples of `resolution` since epoch. If you want to change this alignment, the segments can be offset by specifying the `offset` parameter.

## Example use cases:

1. **Trade Data Analysis:**
   Developers and applications can use this method to analyze and retrieve aggregated trade data for specific asset pairs over a specified time range.

2. **Historical Trade Statistics:**
   Users can request historical trade statistics for asset pairs to gain insights into trading activity.

3. **Trade Data Visualization:**
   Data visualization tools can use this method to generate charts and graphs of trade data over time.

### Request Parameters

The `getTradeAggregations` method accepts a `params` object with the following properties:

- `startTime` (string, optional):
  The start time of the time range for trade aggregations.

- `endTime` (string, optional):
  The end time of the time range for trade aggregations.

- `resolution` (string, optional):
  The duration of each aggregation segment (e.g., '1d' for one day, '1h' for one hour).

- `offset` (string, optional):
  An optional parameter to offset the segments from multiples of `resolution` since epoch.

- `baseAssetType` (string, required):
  The asset type of the base asset (e.g., 'native' or 'credit_alphanum4' or 'credit_alphanum12').

- `baseAssetIssuer` (string, optional):
  The issuer account of the base asset (required if the base asset type is not 'native').

- `baseAssetCode` (string, optional):
  The asset code of the base asset (required if the base asset type is not 'native').

- `counterAssetType` (string, required):
  The asset type of the counter asset (e.g., 'native' or 'credit_alphanum4' or 'credit_alphanum12').

- `counterAssetIssuer` (string, optional):
  The issuer account of the counter asset (required if the counter asset type is not 'native').

- `counterAssetCode` (string, optional):
  The asset code of the counter asset (required if the counter asset type is not 'native').

- `order` (string, optional):
  An optional parameter to specify the order of listing (asc or desc). If not provided, it defaults to 'asc'.

- `limit` (number, optional):
  An optional parameter to specify the maximum number of trade aggregations to return. The limit can range from 1 to 200.

### Return Object

The `getTradeAggregations` method returns an array of trade aggregations based on the specified parameters. Each trade aggregation object contains statistics and data for a specific time segment and asset pair.

(Note: The exact fields in the return object might vary based on the Stellar blockchain's implementation and version.)
