# getAssets

### How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, Stellar, Network } from "@tatumio/tatum";

// Initialize the Tatum SDK for Stellar
const tatum = await TatumSDK.init<Stellar>({ network: Network.STELLAR });

// Define input parameters as an object (Replace placeholders with actual values and remove redundant)
const inputParams = {
  assetCode: "YOUR_ASSET_CODE",
  assetIssuer: "YOUR_ASSET_ISSUER",
  cursor: "YOUR_CURSOR",
  order: "asc",
  limit: 10,
};

// Retrieve a list of all assets
const assets = await tatum.rpc.getAssets(inputParams);

// Log the list of assets
console.log("Assets:", assets);

// Always destroy the Tatum SDK instance when done to stop any background processes
await tatum.destroy();
```

### Overview

The `getAssets` method allows you to retrieve a list of all assets on the Stellar blockchain. You can use various filtering options to narrow down the asset list based on asset code, asset issuer, cursor for pagination, sorting order, and limit for the number of records to be returned.

### Request Parameters

The `getAssets` method accepts the following request parameters:

- `assetCode` (string, optional):
  The asset code for filtering assets by code. Use this parameter to list assets with a specific code.

- `assetIssuer` (string, optional):
  The asset issuer for filtering assets by issuer. Use this parameter to list assets issued by a specific account.

- `cursor` (string, optional):
  A cursor value that determines the starting point for pagination. Use this parameter to retrieve assets from a specific point in the asset list.

- `order` (string, optional):
  A designation of the order in which records should appear. Options include 'asc' (ascending) or 'desc' (descending). If this argument isn’t set, it defaults to 'asc'.

- `limit` (number, optional):
  The maximum number of records returned. It defines the number of assets to fetch in a single request.

### Return Object

The `getAssets` method returns a JSON object containing the list of assets that match the specified criteria. Each asset is represented as an object with various properties describing its characteristics.

(Note: The exact fields in the return object might vary based on the Stellar blockchain's implementation and version.)

```json
{
  "_links": {
    "self": {
      "href": "https://01-vinthill-068-01.rpc.tatum.io/assets?cursor=&limit=10&order=asc"
    },
    "next": {
      "href": "https://01-vinthill-068-01.rpc.tatum.io/assets?cursor=0001_GB7L7CB7F5R7GXXI2VY3AUHDIBGWHUB2SAYO7NPERUCQO4F35G62DBAR_credit_alphanum4&limit=10&order=asc"
    },
    "prev": {
      "href": "https://01-vinthill-068-01.rpc.tatum.io/assets?cursor=0_GBBJZOYEGLOCW32Q4ZGWRWQ7UKIGMMIQXIRBBBOVJVFJTZW7CR2VQKAT_credit_alphanum4&limit=10&order=desc"
    }
  },
  "_embedded": {
    "records": [
      {
        "_links": {
          "toml": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/.well-known/stellar.toml"
          }
        },
        "asset_type": "credit_alphanum4",
        "asset_code": "0",
        "asset_issuer": "GBBJZOYEGLOCW32Q4ZGWRWQ7UKIGMMIQXIRBBBOVJVFJTZW7CR2VQKAT",
        "paging_token": "0_GBBJZOYEGLOCW32Q4ZGWRWQ7UKIGMMIQXIRBBBOVJVFJTZW7CR2VQKAT_credit_alphanum4",
        "num_accounts": 24,
        "num_claimable_balances": 0,
        "num_liquidity_pools": 0,
        "num_contracts": 0,
        "num_archived_contracts": 0,
        "amount": "998.9481303",
        "accounts": {
          "authorized": 24,
          "authorized_to_maintain_liabilities": 0,
          "unauthorized": 0
        },
        "claimable_balances_amount": "0.0000000",
        "liquidity_pools_amount": "0.0000000",
        "contracts_amount": "0.0000000",
        "archived_contracts_amount": "0.0000000",
        "balances": {
          "authorized": "998.9481303",
          "authorized_to_maintain_liabilities": "0.0000000",
          "unauthorized": "0.0000000"
        },
        "flags": {
          "auth_required": false,
          "auth_revocable": false,
          "auth_immutable": false,
          "auth_clawback_enabled": false
        }
      }
    ]
  }
}
```
