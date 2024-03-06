# getLiquidityPool

### How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, Stellar, Network } from "@tatumio/tatum";

// Initialize the Tatum SDK for Stellar
const tatum = await TatumSDK.init<Stellar>({ network: Network.STELLAR });

// Replace 'YOUR_LIQUIDITY_POOL_ID' with the actual Liquidity Pool ID
const liquidityPoolId = "YOUR_LIQUIDITY_POOL_ID";

// Retrieve information about a specific liquidity pool
const liquidityPool = await tatum.rpc.getLiquidityPool(liquidityPoolId);

// Always destroy the Tatum SDK instance when done to stop any background processes
await tatum.destroy();
```

### Overview

The `getLiquidityPool` method allows you to retrieve information about a specific liquidity pool on the Stellar blockchain.

### Example use cases:

1. **Liquidity Pool Analysis:**
   Developers and applications can use this method to analyze and retrieve detailed information about a specific liquidity pool.

2. **Liquidity Pool Management:**
   Platform administrators can access information about a liquidity pool for management purposes.

3. **Liquidity Pool Exploration:**
   Researchers and analysts can explore and study the characteristics of individual liquidity pools.

### Request Parameters

The `getLiquidityPool` method requires the following parameter:

- `liquidityPoolId` (string):
  The unique identifier of the liquidity pool you want to retrieve information about.

### Return Object

The `getLiquidityPool` method returns an object containing detailed information about the specified liquidity pool. This information may include the liquidity pool ID, reserve assets, total value, and more.

(Note: The exact fields in the return object might vary based on the Stellar blockchain's implementation and version.)

```json
{
  "_links": {
    "self": {
      "href": "https://01-vinthill-068-01.rpc.tatum.io/liquidity_pools/0000a8198b5e25994c1ca5b0556faeb27325ac746296944144e0a7406d501e8a"
    },
    "transactions": {
      "href": "https://01-vinthill-068-01.rpc.tatum.io/liquidity_pools/0000a8198b5e25994c1ca5b0556faeb27325ac746296944144e0a7406d501e8a/transactions{?cursor,limit,order}",
      "templated": true
    },
    "operations": {
      "href": "https://01-vinthill-068-01.rpc.tatum.io/liquidity_pools/0000a8198b5e25994c1ca5b0556faeb27325ac746296944144e0a7406d501e8a/operations{?cursor,limit,order}",
      "templated": true
    }
  },
  "id": "0000a8198b5e25994c1ca5b0556faeb27325ac746296944144e0a7406d501e8a",
  "paging_token": "0000a8198b5e25994c1ca5b0556faeb27325ac746296944144e0a7406d501e8a",
  "fee_bp": 30,
  "type": "constant_product",
  "total_trustlines": "1",
  "total_shares": "5494.2144063",
  "reserves": [
    {
      "asset": "native",
      "amount": "3.5287238"
    },
    {
      "asset": "GOLDBANK001:GDEUQ2MX3YXMITFOTC3CO3GW5V3XE3IVG7JKLZZAOZ7WFYIN256INDUS",
      "amount": "11669718.3952703"
    }
  ],
  "last_modified_ledger": 50744249,
  "last_modified_time": "2024-03-11T13:02:15Z"
}
```
