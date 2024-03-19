# getLiquidityPoolOperations

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
  includeFailed: true,
  join: true,
};

// Retrieve operations related to a liquidity pool
const liquidityPoolOperations = await tatum.rpc.getLiquidityPoolOperations(
  params
);

// Always destroy the Tatum SDK instance when done to stop any background processes
await tatum.destroy();
```

### Overview

The `getLiquidityPoolOperations` method allows you to retrieve a list of operations related to a specific liquidity pool on the Stellar blockchain.

### Example use cases:

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

- `join` (boolean, optional):
  An optional parameter to join results. If set to true, results will be joined. Defaults to false.

### Return Object

The `getLiquidityPoolOperations` method returns an array of operations related to the specified liquidity pool on the Stellar blockchain. Each operation object contains information such as the operation ID, source account, type of operation, and more.

(Note: The exact fields in the return object might vary based on the Stellar blockchain's implementation and version.)

```json
{
  "_links": {
    "self": {
      "href": "https://01-vinthill-068-01.rpc.tatum.io/liquidity_pools/0000a8198b5e25994c1ca5b0556faeb27325ac746296944144e0a7406d501e8a/operations?cursor=&limit=10&order=asc"
    },
    "next": {
      "href": "https://01-vinthill-068-01.rpc.tatum.io/liquidity_pools/0000a8198b5e25994c1ca5b0556faeb27325ac746296944144e0a7406d501e8a/operations?cursor=215379467295031297&limit=10&order=asc"
    },
    "prev": {
      "href": "https://01-vinthill-068-01.rpc.tatum.io/liquidity_pools/0000a8198b5e25994c1ca5b0556faeb27325ac746296944144e0a7406d501e8a/operations?cursor=215280038803128321&limit=10&order=desc"
    }
  },
  "_embedded": {
    "records": [
      {
        "_links": {
          "self": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/operations/215280038803128321"
          },
          "transaction": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/transactions/91a59ae616f077b905d29841d7b053282862d3fade107163ea9256847588ef56"
          },
          "effects": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/operations/215280038803128321/effects"
          },
          "succeeds": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/effects?order=desc&cursor=215280038803128321"
          },
          "precedes": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/effects?order=asc&cursor=215280038803128321"
          }
        },
        "id": "215280038803128321",
        "paging_token": "215280038803128321",
        "transaction_successful": true,
        "source_account": "GA5Q3UHRKBBZFUQBFF3CEEPY322UIEALGUA7KS7LKGMAK7WJ4NF3W742",
        "type": "path_payment_strict_receive",
        "type_i": 2,
        "created_at": "2024-01-28T17:10:34Z",
        "transaction_hash": "91a59ae616f077b905d29841d7b053282862d3fade107163ea9256847588ef56",
        "asset_type": "native",
        "from": "GA5Q3UHRKBBZFUQBFF3CEEPY322UIEALGUA7KS7LKGMAK7WJ4NF3W742",
        "to": "GA5Q3UHRKBBZFUQBFF3CEEPY322UIEALGUA7KS7LKGMAK7WJ4NF3W742",
        "amount": "0.0149988",
        "path": [
          {
            "asset_type": "credit_alphanum12",
            "asset_code": "XRPBANK003",
            "asset_issuer": "GAUCPLSPBJKOSN7WZK6SDD2BYPQMC3YSWMLX4XXY7S4JPQFLJXEINDUS"
          },
          {
            "asset_type": "credit_alphanum12",
            "asset_code": "XRPGOLD",
            "asset_issuer": "GAUCPLSPBJKOSN7WZK6SDD2BYPQMC3YSWMLX4XXY7S4JPQFLJXEINDUS"
          },
          {
            "asset_type": "credit_alphanum12",
            "asset_code": "BRICSGOLD",
            "asset_issuer": "GAUCPLSPBJKOSN7WZK6SDD2BYPQMC3YSWMLX4XXY7S4JPQFLJXEINDUS"
          },
          {
            "asset_type": "credit_alphanum12",
            "asset_code": "RUGOLDBRIDGE",
            "asset_issuer": "GAUCPLSPBJKOSN7WZK6SDD2BYPQMC3YSWMLX4XXY7S4JPQFLJXEINDUS"
          },
          {
            "asset_type": "credit_alphanum12",
            "asset_code": "GOLDBANK001",
            "asset_issuer": "GDEUQ2MX3YXMITFOTC3CO3GW5V3XE3IVG7JKLZZAOZ7WFYIN256INDUS"
          }
        ],
        "source_amount": "0.0145987",
        "source_max": "0.0149988",
        "source_asset_type": "native"
      }
    ]
  }
}
```
