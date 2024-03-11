# liquidityPoolEffects

### How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, Stellar, Network } from "@tatumio/tatum";

// Initialize the Tatum SDK for Stellar
const tatum = await TatumSDK.init<Stellar>({ network: Network.STELLAR });

// Replace 'YOUR_LIQUIDITY_POOL_ID' with the actual Liquidity Pool ID
const liquidityPoolId = "YOUR_LIQUIDITY_POOL_ID";

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

  ```json
  {
    "_links": {
      "self": {
        "href": "https://01-vinthill-068-01.rpc.tatum.io/liquidity_pools/0000a8198b5e25994c1ca5b0556faeb27325ac746296944144e0a7406d501e8a/effects?cursor=&limit=10&order=asc"
      },
      "next": {
        "href": "https://01-vinthill-068-01.rpc.tatum.io/liquidity_pools/0000a8198b5e25994c1ca5b0556faeb27325ac746296944144e0a7406d501e8a/effects?cursor=214312580239376385-2&limit=10&order=asc"
      },
      "prev": {
        "href": "https://01-vinthill-068-01.rpc.tatum.io/liquidity_pools/0000a8198b5e25994c1ca5b0556faeb27325ac746296944144e0a7406d501e8a/effects?cursor=214312571649462273-1&limit=10&order=desc"
      }
    },
    "_embedded": {
      "records": [
        {
          "_links": {
            "operation": {
              "href": "https://01-vinthill-068-01.rpc.tatum.io/operations/214312571649462273"
            },
            "succeeds": {
              "href": "https://01-vinthill-068-01.rpc.tatum.io/effects?order=desc&cursor=214312571649462273-1"
            },
            "precedes": {
              "href": "https://01-vinthill-068-01.rpc.tatum.io/effects?order=asc&cursor=214312571649462273-1"
            }
          },
          "id": "0214312571649462273-0000000001",
          "paging_token": "214312571649462273-1",
          "account": "GA5Q3UHRKBBZFUQBFF3CEEPY322UIEALGUA7KS7LKGMAK7WJ4NF3W742",
          "type": "account_credited",
          "type_i": 2,
          "created_at": "2024-01-13T11:19:52Z",
          "asset_type": "native",
          "amount": "0.0252872"
        }
      ]
    }
  }
  ```
