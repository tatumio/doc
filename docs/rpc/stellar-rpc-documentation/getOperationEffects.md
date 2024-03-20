# getOperationEffects

### How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, Stellar, Network } from "@tatumio/tatum";

// Initialize the Tatum SDK for Stellar
const tatum = await TatumSDK.init<Stellar>({ network: Network.STELLAR });

// Define parameters (Replace placeholders with actual values and remove redundant)
const params = {
  operationId: "OPERATION_ID",
  cursor: "YOUR_CURSOR",
  order: "asc",
  limit: 10,
};

// Retrieve effects of a specific operation
const operationEffects = await tatum.rpc.getOperationEffects(params);

// Always destroy the Tatum SDK instance when done to stop any background processes
await tatum.destroy();
```

### Overview

The `getOperationEffects` method allows you to retrieve the effects of a specific operation on the Stellar blockchain by providing the operation's unique identifier.

### Example use cases:

1. **Effect Information Retrieval:**
   Developers and applications can use this method to retrieve detailed information about the effects of a specific operation on the Stellar network.

2. **Effect Analysis:**
   Users can analyze the effects of an operation, which may include details about changes to account balances, trustlines, data entries, and more.

### Request Parameters

The `getOperationEffects` method accepts a single `params` object with the following properties:

- `operationId` (string, required):
  The unique identifier of the operation for which you want to retrieve effects.

- `cursor` (string, optional):
  An optional cursor to start listing effects from a specific point.

- `order` (string, optional):
  An optional parameter to specify the order of listing (asc or desc). If not provided, it defaults to 'asc'.

- `limit` (number, optional):
  An optional parameter to specify the maximum number of effects to return. The limit can range from 1 to 200.

### Return Object

The `getOperationEffects` method returns an array of effects related to the specified operation on the Stellar blockchain. Each effect object contains information about the changes that occurred as a result of the operation.

(Note: The exact fields in the return object might vary based on the Stellar blockchain's implementation and version.)

```json
{
  "_links": {
    "self": {
      "href": "https://01-vinthill-068-01.rpc.tatum.io/operations//effects?cursor=&limit=10&order=asc"
    },
    "next": {
      "href": "https://01-vinthill-068-01.rpc.tatum.io/operations//effects?cursor=215271955673288705-1&limit=10&order=asc"
    },
    "prev": {
      "href": "https://01-vinthill-068-01.rpc.tatum.io/operations//effects?cursor=215271955673169921-1&limit=10&order=desc"
    }
  },
  "_embedded": {
    "records": [
      {
        "_links": {
          "operation": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/operations/215271955673169921"
          },
          "succeeds": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/effects?order=desc&cursor=215271955673169921-1"
          },
          "precedes": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/effects?order=asc&cursor=215271955673169921-1"
          }
        },
        "id": "0215271955673169921-0000000001",
        "paging_token": "215271955673169921-1",
        "account": "GCEETSI6ZGG3CS37YUFAUKCCJSCOILXL43JOJVZ435KBJ5NICDYY4EMP",
        "type": "account_credited",
        "type_i": 2,
        "created_at": "2024-01-28T14:07:11Z",
        "asset_type": "credit_alphanum4",
        "asset_code": "yXLM",
        "asset_issuer": "GARDNV3Q7YGT4AKSDF25LT32YSCCW4EV22Y2TV3I2PU2MMXJTEDL5T55",
        "amount": "1.0291984"
      }
    ]
  }
}
```
