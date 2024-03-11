# getClaimableBalances

### How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, Stellar, Network } from "@tatumio/tatum";

// Initialize the Tatum SDK for Stellar
const tatum = await TatumSDK.init<Stellar>({ network: Network.STELLAR });

// Define input parameters as an object (Replace placeholders with actual values and remove redundant)
const params = {
  sponsor: "YOUR_SPONSOR_ACCOUNT_ID",
  asset: "YOUR_ASSET",
  claimant: "YOUR_CLAIMANT_ACCOUNT_ID",
  cursor: "YOUR_CURSOR",
  order: "asc",
  limit: 10,
};

// Retrieve a list of all claimable balances
const claimableBalances = await tatum.rpc.getClaimableBalances(params);

// Log the list of claimable balances
console.log("Claimable Balances:", claimableBalances);

// Always destroy the Tatum SDK instance when done to stop any background processes
await tatum.destroy();
```

### Overview

The `getClaimableBalances` method allows you to retrieve a list of all available claimable balances on the Stellar blockchain. You can use various filtering options to narrow down the list based on the sponsor account, asset code, claimant account, cursor for pagination, sorting order, and limit for the number of records to be returned.

### Request Parameters

The `getClaimableBalances` method accepts the following request parameters:

- `sponsor` (string, optional):
  The account ID of the sponsor to filter claimable balances. Use this parameter to list claimable balances sponsored by a specific account.

- `asset` (string, optional):
  The asset code to filter claimable balances. Use this parameter to list claimable balances associated with a specific asset.

- `claimant` (string, optional):
  The account ID of the claimant to filter claimable balances. Use this parameter to list claimable balances claimable by a specific account.

- `cursor` (string, optional):
  A cursor value that determines the starting point for pagination. Use this parameter to retrieve claimable balances from a specific point in the list.

- `order` (string, optional):
  A designation of the order in which records should appear. Options include 'asc' (ascending) or 'desc' (descending). If this argument isn’t set, it defaults to 'asc'.

- `limit` (number, optional):
  The maximum number of records returned. It defines the number of claimable balances to fetch in a single request.

### Return Object

The `getClaimableBalances` method returns a JSON object containing the list of claimable balances that match the specified criteria. Each claimable balance is represented as an object with various properties describing its characteristics.

(Note: The exact fields in the return object might vary based on the Stellar blockchain's implementation and version.)

```json
{
  "_links": {
    "self": {
      "href": "https://01-vinthill-068-01.rpc.tatum.io/claimable_balances?cursor=&limit=10&order=asc"
    },
    "next": {
      "href": "https://01-vinthill-068-01.rpc.tatum.io/claimable_balances?cursor=33494305-000000006f6cd6031f3e4fcdfb795412cc0f1ffd45663098691f5eff88ff9b6cff1006a0&limit=10&order=asc"
    },
    "prev": {
      "href": "https://01-vinthill-068-01.rpc.tatum.io/claimable_balances?cursor=32747318-00000000178826fbfe339e1f5c53417c6fedfe2c05e8bec14303143ec46b38981b09c3f9&limit=10&order=desc"
    }
  },
  "_embedded": {
    "records": [
      {
        "_links": {
          "self": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/claimable_balances/00000000178826fbfe339e1f5c53417c6fedfe2c05e8bec14303143ec46b38981b09c3f9"
          },
          "transactions": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/claimable_balances/00000000178826fbfe339e1f5c53417c6fedfe2c05e8bec14303143ec46b38981b09c3f9/transactions{?cursor,limit,order}",
            "templated": true
          },
          "operations": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/claimable_balances/00000000178826fbfe339e1f5c53417c6fedfe2c05e8bec14303143ec46b38981b09c3f9/operations{?cursor,limit,order}",
            "templated": true
          }
        },
        "id": "00000000178826fbfe339e1f5c53417c6fedfe2c05e8bec14303143ec46b38981b09c3f9",
        "asset": "BODHI:GDCJIHD3623OCYNH65UUQC3NLG2D6YCNCDPZULRLCLOA76TBQRL6A3TF",
        "amount": "0.1000000",
        "sponsor": "GDCJIHD3623OCYNH65UUQC3NLG2D6YCNCDPZULRLCLOA76TBQRL6A3TF",
        "last_modified_ledger": 32747318,
        "last_modified_time": null,
        "claimants": [
          {
            "destination": "GBEUDKANIFPTFHPWJ5T3R6RIO36RQBFGHYPAQ6STH7KMNDHAT36LHOLD",
            "predicate": {
              "unconditional": true
            }
          }
        ],
        "flags": {
          "clawback_enabled": false
        },
        "paging_token": "32747318-00000000178826fbfe339e1f5c53417c6fedfe2c05e8bec14303143ec46b38981b09c3f9"
      }
    ]
  }
}
```
