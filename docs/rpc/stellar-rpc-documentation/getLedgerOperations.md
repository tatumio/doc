# getLedgersOperations

### How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, Stellar, Network } from "@tatumio/tatum";

// Initialize the Tatum SDK for Stellar
const tatum = await TatumSDK.init<Stellar>({ network: Network.STELLAR });

// Define the ledger sequence number and optional parameters (Replace placeholders with actual values and remove redundant)
const params = {
  sequence: "YOUR_LEDGER_SEQUENCE",
  cursor: "YOUR_CURSOR",
  order: "asc",
  limit: 10,
  includeFailed: true,
  join: "inner",
};

// Retrieve successful operations related to a specific ledger
const ledgerOperations = await tatum.rpc.getLedgersOperations(params);

// Always destroy the Tatum SDK instance when done to stop any background processes
await tatum.destroy();
```

### Overview

The `getLedgersOperations` method allows you to retrieve successful operations in a specific Stellar ledger.

### Example use cases:

1. **Transaction Analysis:**
   Developers and applications can use this method to analyze successful operations within a specific ledger, including operations like payments, account creation, and more.

2. **Transaction Tracking:**
   Tracking and monitoring successful operations made within a specific ledger for auditing or analysis purposes.

3. **Historical Data Retrieval:**
   Researchers and analysts can retrieve operation-related data for historical analysis and record-keeping.

### Request Parameters

The `getLedgersOperations` method requires the following parameters:

- `sequence` (string, required):
  The sequence number of the ledger for which you want to retrieve successful operations.

- `cursor` (string, optional):
  An optional cursor to start listing operations from a specific point within the ledger.

- `order` (string, optional):
  An optional parameter to specify the order of listing (asc or desc). If not provided, it defaults to 'asc'.

- `limit` (number, optional):
  An optional parameter to specify the maximum number of operations to return. The limit can range from 1 to 200.

- `includeFailed` (boolean, optional):
  An optional parameter to include failed operations in the results (true or false). If not provided, it defaults to 'false'.

- `join` (string, optional):
  An optional parameter to specify the join type (inner or left). If not provided, it defaults to 'inner'.

### Return Object

The `getLedgersOperations` method returns an array of successful operations within the specified ledger. Each operation includes details such as the source account, operation type, asset, amount, and more.

(Note: The exact fields in the return object might vary based on the Stellar blockchain's implementation and version.)

```json
{
  "_links": {
    "self": {
      "href": "https://01-vinthill-068-01.rpc.tatum.io/ledgers/49896908/operations?cursor=&limit=10&order=asc"
    },
    "next": {
      "href": "https://01-vinthill-068-01.rpc.tatum.io/ledgers/49896908/operations?cursor=214305588031541254&limit=10&order=asc"
    },
    "prev": {
      "href": "https://01-vinthill-068-01.rpc.tatum.io/ledgers/49896908/operations?cursor=214305588031524865&limit=10&order=desc"
    }
  },
  "_embedded": {
    "records": [
      {
        "_links": {
          "self": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/operations/214305588031524865"
          },
          "transaction": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/transactions/83e580608afbc0d269107dd92629ae5be4a039c2751896bdf8e357a9cd947ea4"
          },
          "effects": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/operations/214305588031524865/effects"
          },
          "succeeds": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/effects?order=desc&cursor=214305588031524865"
          },
          "precedes": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/effects?order=asc&cursor=214305588031524865"
          }
        },
        "id": "214305588031524865",
        "paging_token": "214305588031524865",
        "transaction_successful": true,
        "source_account": "GAZCCHIATB5Z6ATORF46EDXRUKVDNGHOFL3NKG7Y577NBTSOWMJX2DOS",
        "type": "manage_buy_offer",
        "type_i": 12,
        "created_at": "2024-01-13T08:44:04Z",
        "transaction_hash": "83e580608afbc0d269107dd92629ae5be4a039c2751896bdf8e357a9cd947ea4",
        "amount": "105606.5780934",
        "price": "0.0094863",
        "price_r": {
          "n": 94863,
          "d": 10000000
        },
        "buying_asset_type": "credit_alphanum4",
        "buying_asset_code": "SSLX",
        "buying_asset_issuer": "GBHFGY3ZNEJWLNO4LBUKLYOCEK4V7ENEBJGPRHHX7JU47GWHBREH37UR",
        "selling_asset_type": "native",
        "offer_id": "1449752262"
      }
    ]
  }
}
```
