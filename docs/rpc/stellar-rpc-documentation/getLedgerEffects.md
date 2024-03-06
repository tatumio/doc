# getLedgersEffects

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
};

// Retrieve effects related to a specific ledger
const ledgerEffects = await tatum.rpc.getLedgersEffects(params);

// Always destroy the Tatum SDK instance when done to stop any background processes
await tatum.destroy();
```

### Overview

The `getLedgersEffects` method allows you to retrieve the effects of a specific Stellar ledger.

### Example use cases:

1. **Transaction Analysis:** Developers and applications can use this method to analyze the effects related to transactions and operations within a specific ledger.
2. **Transaction Tracking:** Tracking and monitoring the effects of operations within a specific ledger for auditing or analysis purposes.
3. **Historical Data Retrieval:** Researchers and analysts can retrieve effect-related data for historical analysis and record-keeping.

### Request Parameters

The `getLedgersEffects` method requires the following parameters:

- `sequence` (string, required): The sequence number of the ledger for which you want to retrieve effects.
- `cursor` (string, optional): An optional cursor to start listing effects from a specific point within the ledger.
- `order` (string, optional): An optional parameter to specify the order of listing (asc or desc). If not provided, it defaults to 'asc'.
- `limit` (number, optional): An optional parameter to specify the maximum number of effects to return. The limit can range from 1 to 200.

### Return Object

The `getLedgersEffects` method returns an array of effects related to the specified ledger. Each effect includes details such as the type, account, operation, and more.

(Note: The exact fields in the return object might vary based on the Stellar blockchain's implementation and version.)

```json
{
  "_links": {
    "self": {
      "href": "https://01-vinthill-068-01.rpc.tatum.io/ledgers/49896908/effects?cursor=&limit=10&order=asc"
    },
    "next": {
      "href": "https://01-vinthill-068-01.rpc.tatum.io/ledgers/49896908/effects?cursor=214305588031623169-6&limit=10&order=asc"
    },
    "prev": {
      "href": "https://01-vinthill-068-01.rpc.tatum.io/ledgers/49896908/effects?cursor=214305588031610881-1&limit=10&order=desc"
    }
  },
  "_embedded": {
    "records": [
      {
        "_links": {
          "operation": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/operations/214305588031610881"
          },
          "succeeds": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/effects?order=desc&cursor=214305588031610881-1"
          },
          "precedes": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/effects?order=asc&cursor=214305588031610881-1"
          }
        },
        "id": "0214305588031610881-0000000001",
        "paging_token": "214305588031610881-1",
        "account": "GC2ATEL4K2O5BJO7Z76MYSV6TKHCROKV5GXEOU7NO2TUEOOMFDDIPWID",
        "type": "trustline_flags_updated",
        "type_i": 26,
        "created_at": "2024-01-13T08:44:04Z",
        "asset_type": "credit_alphanum4",
        "asset_code": "USD",
        "asset_issuer": "GC2ATEL4K2O5BJO7Z76MYSV6TKHCROKV5GXEOU7NO2TUEOOMFDDIPWID",
        "trustor": "GDFQ5USFBAUR2XEKCC7Z6VBEN5TJJH7TZPFKNHR47RCW36NCO3RQ5U5T",
        "authorized_flag": true
      }
    ]
  }
}
```
