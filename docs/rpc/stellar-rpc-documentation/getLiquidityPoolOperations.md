# getLiquidityPoolOperations

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
    includeFailed: true,
    join: ''
};

// Retrieve operations related to a liquidity pool
const liquidityPoolOperations = await tatum.rpc.getLiquidityPoolOperations(params);

// Always destroy the Tatum SDK instance when done to stop any background processes
await tatum.destroy();
```

### Overview

The `getLiquidityPoolOperations` method allows you to retrieve a list of operations related to a specific liquidity pool on the Stellar blockchain.

## Example use cases:

1. **Liquidity Pool Operation Analysis:**
   Developers and applications can use this method to analyze and retrieve information about operations associated with a liquidity pool.

2. **Liquidity Pool Operation Monitoring:**
   Platform administrators can monitor and track operations related to liquidity pools for auditing and management purposes.

3. **Liquidity Pool Operation Exploration:**
   Researchers and analysts can explore and analyze the characteristics of operations involving liquidity pools on the Stellar network.

### Request Parameters

The `getLiquidityPoolOperations` method accepts the following optional parameters:

- `liquidityPoolId` (string, required):
  The unique identifier of the liquidity pool for which you want to retrieve operations.

- `cursor` (string, optional):
  An optional cursor to start listing operations from a specific point.

- `order` (string, optional):
  An optional parameter to specify the order of listing (asc or desc). If not provided, it defaults to 'asc'.

- `limit` (number, optional):
  An optional parameter to specify the maximum number of operations to return. The limit can range from 1 to 200.

- `includeFailed` (boolean, optional):
  An optional parameter to include failed operations. If set to true, failed operations will be included in the results. Defaults to false.

- `join` (string, optional): 
  Set this parameter to "transactions" in the query to include the transactions which created each of the operations in the response. It is not required and is used to enrich the response with transaction details pertinent to the operations.

### Return Object

The `getLiquidityPoolOperations` method returns an array of operations related to the specified liquidity pool on the Stellar blockchain. Each operation object contains information such as the operation ID, source account, type of operation, and more.

(Note: The exact fields in the return object might vary based on the Stellar blockchain's implementation and version.)