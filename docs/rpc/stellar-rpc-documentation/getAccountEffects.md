# getAccountEffects

### How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, Stellar, Network } from "@tatumio/tatum";

// Initialize the Tatum SDK for Stellar
const tatum = await TatumSDK.init<Stellar>({ network: Network.STELLAR });

// Define input parameters as an object (Replace placeholders with actual values and remove redundant)
const inputParams = {
  accountId: "YOUR_ACCOUNT_ID",
  cursor: "now",
  order: "asc",
  limit: 10,
};

// Retrieve effects of a specific account
const effects = await tatum.rpc.getAccountEffects(inputParams);

// Log the list of effects
console.log("Account Effects:", effects);

// Always destroy the Tatum SDK instance when done to stop any background processes
await tatum.destroy();
```

### Overview

The `getAccountEffects` method allows you to retrieve the effects of a specific account on the Stellar blockchain. You can use this endpoint in streaming mode to listen for new effects for the specified account as they are added to the Stellar ledger. When called in streaming mode, Horizon will start at the earliest known effect unless a cursor is set, in which case it will start from that cursor. Setting the cursor value to 'now' allows you to stream effects created since your request time.

### Request Parameters

The `getAccountEffects` method accepts the following request parameters:

- `accountId` (string, required):
  The unique identifier (account ID) of the account for which you want to retrieve effects.

- `cursor` (string, optional):
  A cursor value that determines the starting point for retrieving effects. Set it to 'now' to stream effects created since your request time.

- `order` (string, optional):
  A designation of the order in which records should appear. Options include 'asc' (ascending) or 'desc' (descending). If this argument isn’t set, it defaults to 'asc'.

- `limit` (number, optional):
  The maximum number of records returned. It defines the number of effects to fetch in a single request.

### Return Object

The `getAccountEffects` method returns a JSON object containing the list of effects associated with the specified account. Each effect represents an event that has occurred on the Stellar blockchain, such as the creation of an account, a payment, or other actions.

(Note: The exact fields in the return object might vary based on the Stellar blockchain's implementation and version.)

```json
{
  "_links": {
    "self": {
      "href": "https://.."
    },
    "next": {
      "href": "https://.."
    },
    "prev": {
      "href": "https://.."
    }
  },
  "_embedded": {
    "records": [
      {
        "_links": {
          "operation": {
            "href": "https://..."
          },
          "succeeds": {
            "href": "https://..."
          },
          "precedes": {
            "href": "https://..."
          }
        },
        "id": "0216517620744060929-0000000002",
        "paging_token": "216517620744060929-2",
        "account": "GA2224DCGO3WHC4EALA2PR2BZEMAYZPBPTHS243ZYYWQMBWRPJSZH5A6",
        "type": "claimable_balance_claimant_created",
        "type_i": 51,
        "created_at": "2024-02-17T14:03:50Z",
        "asset": "ENIZ:GDLMUA4ZQSU3LMKEW7LETSIYLYMATTGVPXCHFRRTGQTF6K55XOQIENIZ",
        "balance_id": "000000004c56a7b5e98e7d5225f37d27fbd93c4fe2f03b00d2c80d23771ae97e66f599c7",
        "amount": "5000.0000000",
        "predicate": {
          "unconditional": true
        }
      }
    ]
  }
}
```
