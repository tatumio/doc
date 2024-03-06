# getLiquidityPoolTrades

### How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, Stellar, Network } from "@tatumio/tatum";

// Initialize the Tatum SDK for Stellar
const tatum = await TatumSDK.init<Stellar>({ network: Network.STELLAR });

// Define parameters (Replace placeholders with actual values and remove redundant)
const params = {
  liquidityPoolId: "YOUR_LIQUIDITY_POOL_ID",
  cursor: "YOUR_CURSOR",
  order: "asc",
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

```json
{
  "_links": {
    "self": {
      "href": "https://01-vinthill-068-01.rpc.tatum.io/liquidity_pools/0000a8198b5e25994c1ca5b0556faeb27325ac746296944144e0a7406d501e8a/trades?cursor=&limit=10&order=asc"
    },
    "next": {
      "href": "https://01-vinthill-068-01.rpc.tatum.io/liquidity_pools/0000a8198b5e25994c1ca5b0556faeb27325ac746296944144e0a7406d501e8a/trades?cursor=214318047732097026-0&limit=10&order=asc"
    },
    "prev": {
      "href": "https://01-vinthill-068-01.rpc.tatum.io/liquidity_pools/0000a8198b5e25994c1ca5b0556faeb27325ac746296944144e0a7406d501e8a/trades?cursor=214312571649462273-0&limit=10&order=desc"
    }
  },
  "_embedded": {
    "records": [
      {
        "_links": {
          "self": {
            "href": ""
          },
          "base": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/accounts/GA5Q3UHRKBBZFUQBFF3CEEPY322UIEALGUA7KS7LKGMAK7WJ4NF3W742"
          },
          "counter": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/liquidity_pools/0000a8198b5e25994c1ca5b0556faeb27325ac746296944144e0a7406d501e8a"
          },
          "operation": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/operations/214312571649462273"
          }
        },
        "id": "214312571649462273-0",
        "paging_token": "214312571649462273-0",
        "ledger_close_time": "2024-01-13T11:19:52Z",
        "trade_type": "liquidity_pool",
        "liquidity_pool_fee_bp": 30,
        "base_offer_id": "4825998590076850177",
        "base_account": "GA5Q3UHRKBBZFUQBFF3CEEPY322UIEALGUA7KS7LKGMAK7WJ4NF3W742",
        "base_amount": "0.0242091",
        "base_asset_type": "native",
        "counter_liquidity_pool_id": "0000a8198b5e25994c1ca5b0556faeb27325ac746296944144e0a7406d501e8a",
        "counter_amount": "23250.7124160",
        "counter_asset_type": "credit_alphanum12",
        "counter_asset_code": "GOLDBANK001",
        "counter_asset_issuer": "GDEUQ2MX3YXMITFOTC3CO3GW5V3XE3IVG7JKLZZAOZ7WFYIN256INDUS",
        "base_is_seller": false,
        "price": {
          "n": "232507124160",
          "d": "242091"
        }
      }
    ]
  }
}
```
