# getLiquidityPoolTrades

### How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, Stellar, Network } from '@tatumio/tatum';

// Initialize the Tatum SDK for Stellar
const tatum = await TatumSDK.init<Stellar>({ network: Network.STELLAR });

// Define parameters (Replace placeholders with actual values and remove redundant)
const params = {
    liquidityPoolId: 'YOUR_LIQUIDITY_POOL_ID',
    cursor: 'YOUR_CURSOR',
    order: 'asc',
    limit: 10,
};

// Retrieve trades related to a liquidity pool
const liquidityPoolTrades = await tatum.rpc.getLiquidityPoolTrades(params);

// Always destroy the Tatum SDK instance when done to stop any background processes
await tatum.destroy();
```

### Overview

The `getLiquidityPoolTrades` method allows you to retrieve successful trades fulfilled by a specific liquidity pool on the Stellar blockchain.

### Example use cases:

1. **Liquidity Pool Monitoring:**
   Developers and applications can use this method to monitor and retrieve successful trades related to liquidity pools.

2. **Liquidity Pool Analysis:**
   Researchers and analysts can analyze the trade history of liquidity pools to gain insights into their performance.

### Request Parameters

The `getLiquidityPoolTrades` method accepts the following parameters:

- `liquidityPoolId` (string):
  The ID of the liquidity pool for which you want to retrieve related trades.

- `cursor` (string, optional):
  An optional cursor to start listing liquidity pool trades from a specific point.

- `order` (string, optional):
  An optional parameter to specify the order of listing (asc or desc). If not provided, it defaults to 'asc'.

- `limit` (number, optional):
  An optional parameter to specify the maximum number of trades to return. The limit can range from 1 to 200.

### Return Object

The `getLiquidityPoolTrades` method returns an array of trades related to the specified liquidity pool on the Stellar blockchain. Each trade object contains information such as the trade ID, asset details, timestamp, and more.

(Note: The exact fields in the return object might vary based on the Stellar blockchain's implementation and version.)
