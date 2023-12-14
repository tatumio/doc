# getLiquidityPoolsTransactions

## How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, Stellar, Network } from '@tatumio/tatum';

// Initialize the Tatum SDK for Stellar
const tatum = await TatumSDK.init<Stellar>({ network: Network.STELLAR });

// Define parameters (Replace placeholders with actual values)
const params = {
    liquidityPoolId: 'YOUR_LIQUIDITY_POOL_ID',
    cursor: 'YOUR_CURSOR',
    order: 'asc',
    limit: 10,
    includeFailed: true
};

// Retrieve transactions related to a liquidity pool
const liquidityPoolTransactions = await tatum.rpc.getLiquidityPoolsTransactions(params);

// Always destroy the Tatum SDK instance when done to stop any background processes
await tatum.destroy();
```

## Overview

The `getLiquidityPoolsTransactions` method allows you to retrieve a list of transactions related to a specific liquidity pool on the Stellar blockchain.

## Example use cases:

1. **Liquidity Pool Transaction Analysis:**
   Developers and applications can use this method to analyze and retrieve information about transactions associated with a liquidity pool.
   
2. **Liquidity Pool Transaction Monitoring:**
   Platform administrators can monitor and track transactions related to liquidity pools for auditing and management purposes.

3. **Liquidity Pool Transaction Exploration:**
   Researchers and analysts can explore and analyze the characteristics of transactions involving liquidity pools on the Stellar network.

## Request Parameters

The `getLiquidityPoolsTransactions` method accepts the following optional parameters:

- `liquidityPoolId` (string, required):
  The unique identifier of the liquidity pool for which you want to retrieve transactions.

- `cursor` (string, optional):
  An optional cursor to start listing transactions from a specific point.

- `order` (string, optional):
  An optional parameter to specify the order of listing (asc or desc). If not provided, it defaults to 'asc'.

- `limit` (number, optional):
  An optional parameter to specify the maximum number of transactions to return. The limit can range from 1 to 200.

- `includeFailed` (boolean, optional):
  An optional parameter to include failed transactions. If set to true, failed transactions will be included in the results. Defaults to false.

## Return Object

The `getLiquidityPoolsTransactions` method returns an array of transactions related to the specified liquidity pool on the Stellar blockchain. Each transaction object contains information such as the transaction ID, source account, destination account, and more.

(Note: The exact fields in the return object might vary based on the Stellar blockchain's implementation and version.)
