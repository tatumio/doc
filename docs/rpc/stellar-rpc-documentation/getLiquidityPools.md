# getLiquidityPools

### How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, Stellar, Network } from "@tatumio/tatum";

// Initialize the Tatum SDK for Stellar
const tatum = await TatumSDK.init<Stellar>({ network: Network.STELLAR });

// Define optional parameters (Replace placeholders with actual values and remove redundant)
const params = {
  reserve: "YOUR_RESERVE",
  account: "YOUR_ACCOUNT",
  cursor: "YOUR_CURSOR",
  order: "asc",
  limit: 10,
};

// List all available liquidity pools
const liquidityPools = await tatum.rpc.getLiquidityPools(params);

// Always destroy the Tatum SDK instance when done to stop any background processes
await tatum.destroy();
```

### Overview

The `getLiquidityPools` method allows you to retrieve a list of all available liquidity pools on the Stellar blockchain.

### Example use cases:

1. **Liquidity Pool Analysis:**
   Developers and applications can use this method to analyze and retrieve information about existing liquidity pools.

2. **Liquidity Pool Management:**
   Platform administrators can manage liquidity pools by listing and tracking their status.

3. **Liquidity Pool Exploration:**
   Researchers and analysts can explore and analyze the characteristics of liquidity pools on the Stellar network.

### Request Parameters

The `getLiquidityPools` method accepts the following optional parameters:

- `reserve` (string, optional):
  Filter liquidity pools by the reserve asset. Provide the asset code of the reserve asset.

- `account` (string, optional):
  Filter liquidity pools by account ID. Provide the account ID associated with the liquidity pool.

- `cursor` (string, optional):
  An optional cursor to start listing liquidity pools from a specific point.

- `order` (string, optional):
  An optional parameter to specify the order of listing (asc or desc). If not provided, it defaults to 'asc'.

- `limit` (number, optional):
  An optional parameter to specify the maximum number of liquidity pools to return. The limit can range from 1 to 200.

### Return Object

The `getLiquidityPools` method returns an array of liquidity pools on the Stellar blockchain. Each liquidity pool object contains information such as the liquidity pool ID, reserve asset, total value, and more.

(Note: The exact fields in the return object might vary based on the Stellar blockchain's implementation and version.)

```json
{
  "_links": {
    "self": {
      "href": "https://01-vinthill-068-01.rpc.tatum.io/liquidity_pools?cursor=&limit=10&order=asc"
    },
    "next": {
      "href": "https://01-vinthill-068-01.rpc.tatum.io/liquidity_pools?cursor=00293f3a22c8ef5561de7cefc98f9286ac688cb8abf6b1c29a1dabbb63f265ce&limit=10&order=asc"
    },
    "prev": {
      "href": "https://01-vinthill-068-01.rpc.tatum.io/liquidity_pools?cursor=0000a8198b5e25994c1ca5b0556faeb27325ac746296944144e0a7406d501e8a&limit=10&order=desc"
    }
  },
  "_embedded": {
    "records": [
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
    ]
  }
}
```
