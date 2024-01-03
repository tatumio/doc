# liquidityPoolEffects

### How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, Stellar, Network } from '@tatumio/tatum';

// Initialize the Tatum SDK for Stellar
const tatum = await TatumSDK.init<Stellar>({ network: Network.STELLAR });

// Replace 'YOUR_LIQUIDITY_POOL_ID' with the actual Liquidity Pool ID
const liquidityPoolId = 'YOUR_LIQUIDITY_POOL_ID';

// Retrieve effects related to a specific liquidity pool
const effects = await tatum.rpc.liquidityPoolEffects(liquidityPoolId);

// Always destroy the Tatum SDK instance when done to stop any background processes
await tatum.destroy();
```

### Overview

The `liquidityPoolEffects` method allows you to retrieve effects related to a specific liquidity pool on the Stellar blockchain. Effects represent various events or changes that occur within the Stellar network, such as trades, payments, and more.

### Example use cases:

1. **Monitoring Liquidity Pool Activity:**
   Developers and applications can use this method to monitor and track events related to a particular liquidity pool.

2. **Transaction Analysis:**
   Researchers and analysts can analyze the effects of liquidity pool transactions for reporting and insights.

3. **Real-time Updates:**
   Applications can subscribe to streaming updates to receive real-time notifications of new effects associated with the liquidity pool.

### Request Parameters

The `liquidityPoolEffects` method requires the following parameters:

- `liquidityPoolId` (string):
  The unique identifier of the liquidity pool for which you want to retrieve related effects.
