# getOperation

### How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, Stellar, Network } from "@tatumio/tatum";

// Initialize the Tatum SDK for Stellar
const tatum = await TatumSDK.init<Stellar>({ network: Network.STELLAR });

// Define parameters (Replace placeholders with actual values and remove redundant)
const params = {
  operationId: "OPERATION_ID",
  join: true,
};

// Retrieve information about a specific operation
const operationInfo = await tatum.rpc.getOperation(params);

// Always destroy the Tatum SDK instance when done to stop any background processes
await tatum.destroy();
```

### Overview

The `getOperation` method allows you to retrieve detailed information about a specific operation on the Stellar blockchain by providing the operation's unique identifier.

### Example use cases:

1. **Operation Information Retrieval:**
   Developers and applications can use this method to retrieve detailed information about a specific operation on the Stellar network.

2. **Operation Verification:**
   Users can verify the details of an operation, including its type, source account, destination account, and other relevant information.

### Request Parameters

The `getOperation` method accepts the following parameters:

- `operationId` (string, required):
  The unique identifier of the operation for which you want to retrieve information.

- `join` (boolean, optional):
  An optional parameter to join results. If set to true, results will be joined. Defaults to false.

### Return Object

The `getOperation` method returns detailed information about the specified operation on the Stellar blockchain. The response includes data such as the operation ID, source account, destination account, type of operation, and more.

(Note: The exact fields in the return object might vary based on the Stellar blockchain's implementation and version.)

```json
{
  "_links": {
    "self": {
      "href": "https://01-vinthill-068-01.rpc.tatum.io/operations?cursor=&limit=10&order=asc"
    },
    "next": {
      "href": "https://01-vinthill-068-01.rpc.tatum.io/operations?cursor=215271955673231361&limit=10&order=asc"
    },
    "prev": {
      "href": "https://01-vinthill-068-01.rpc.tatum.io/operations?cursor=215271955673128961&limit=10&order=desc"
    }
  },
  "_embedded": {
    "records": [
      {
        "_links": {
          "self": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/operations/215271955673128961"
          },
          "transaction": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/transactions/bf3e8c575c463bff1c23c1a7113b38d1cb79c983be62bf696dc96632ef00af47"
          },
          "effects": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/operations/215271955673128961/effects"
          },
          "succeeds": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/effects?order=desc&cursor=215271955673128961"
          },
          "precedes": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/effects?order=asc&cursor=215271955673128961"
          }
        },
        "id": "215271955673128961",
        "paging_token": "215271955673128961",
        "transaction_successful": true,
        "source_account": "GBARZTOSSCH3XDC7NMRIHQVOWEYX7VOBQ4TZTR4HZRBZS3UO7QID242H",
        "type": "manage_sell_offer",
        "type_i": 3,
        "created_at": "2024-01-28T14:07:11Z",
        "transaction_hash": "bf3e8c575c463bff1c23c1a7113b38d1cb79c983be62bf696dc96632ef00af47",
        "amount": "0.1833209",
        "price": "5.4578916",
        "price_r": {
          "n": 545789163,
          "d": 100000000
        },
        "buying_asset_type": "native",
        "selling_asset_type": "credit_alphanum4",
        "selling_asset_code": "RIO",
        "selling_asset_issuer": "GBNLJIYH34UWO5YZFA3A3HD3N76R6DOI33N4JONUOHEEYZYCAYTEJ5AK",
        "offer_id": "1461815697"
      }
    ]
  }
}
```
