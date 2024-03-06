# getClaimableBalance

### How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, Stellar, Network } from "@tatumio/tatum";

// Initialize the Tatum SDK for Stellar
const tatum = await TatumSDK.init<Stellar>({ network: Network.STELLAR });

// Define the claimable balance ID (Replace 'YOUR_CLAIMABLE_BALANCE_ID' with the actual claimable balance ID)
const claimableBalanceId = "YOUR_CLAIMABLE_BALANCE_ID";

// Retrieve information about a specific claimable balance
const claimableBalance = await tatum.rpc.getClaimableBalance(
  claimableBalanceId
);

// Log the claimable balance details
console.log("Claimable Balance:", claimableBalance);

// Always destroy the Tatum SDK instance when done to stop any background processes
await tatum.destroy();
```

### Overview

The `getClaimableBalance` method allows you to retrieve information about a specific claimable balance on the Stellar blockchain. You need to provide the claimable balance ID to identify the balance you want to retrieve.

### Request Parameters

The `getClaimableBalance` method accepts the following request parameters:

- `claimableBalanceId` (string, required):
  The unique identifier of the claimable balance you want to retrieve.

### Return Object

The `getClaimableBalance` method returns a JSON object containing the details of the requested claimable balance. The object includes various properties describing the characteristics of the claimable balance.

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
