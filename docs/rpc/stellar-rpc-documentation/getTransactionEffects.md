# getTransactionsEffects

### How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, Stellar, Network } from "@tatumio/tatum";

// Initialize the Tatum SDK for Stellar
const tatum = await TatumSDK.init<Stellar>({ network: Network.STELLAR });

// Define parameters (Replace placeholders with actual values and remove redundant)
const params = {
  hash: "YOUR_TRANSACTION_HASH", // Replace with the actual transaction hash
  cursor: "YOUR_CURSOR",
  order: "asc",
  limit: 10,
};

// Get effects for a specific transaction
const transactionEffects = await tatum.rpc.getTransactionsEffects(params);

// Always destroy the Tatum SDK instance when done to stop any background processes
await tatum.destroy();
```

### Overview

The `Retrieve a Transaction's Effects` method allows you to retrieve the effects of a specific transaction on the Stellar blockchain. You can use this method to view the various effects produced by the transaction, such as offers created, payments made, and more.

### Example use cases:

1. **Transaction Analysis:**
   Developers and applications can use this method to analyze the effects of a particular transaction, including its impact on the Stellar network.

2. **Auditing and Reporting:**
   Users can retrieve the effects of a transaction for auditing and reporting purposes.

### Request Parameters

The `Retrieve a Transaction's Effects` method accepts the following parameters:

- `hash` (string, required):
  The hash of the transaction for which you want to retrieve effects.

- `cursor` (string, optional):
  An optional cursor to start listing effects from a specific point.

- `order` (string, optional):
  An optional parameter to specify the order of listing (asc or desc). If not provided, it defaults to 'asc'.

- `limit` (number, optional):
  An optional parameter to specify the maximum number of effects to return. The limit can range from 1 to 200.

### Return Object

The `Retrieve a Transaction's Effects` method returns an array of effects associated with the specified transaction on the Stellar blockchain. Each effect object contains information such as the effect type, asset details, and other relevant data.

(Note: The exact fields in the return object might vary based on the Stellar blockchain's implementation and version.)

Feel free to replace `'YOUR_TRANSACTION_HASH'` with the actual hash of the transaction you want to retrieve effects for.

```json
{
  "value": {
    "_links": {
      "self": {
        "href": "https://horizon.stellar.org/transactions/512a9946bc7ff4a363299f14f79e0beb9b9cdbd0103e3a69a44446a0aa6471a8/effects?cursor=&limit=10&order=asc"
      },
      "next": {
        "href": "https://horizon.stellar.org/transactions/512a9946bc7ff4a363299f14f79e0beb9b9cdbd0103e3a69a44446a0aa6471a8/effects?cursor=121628667754319873-2&limit=10&order=asc"
      },
      "prev": {
        "href": "https://horizon.stellar.org/transactions/512a9946bc7ff4a363299f14f79e0beb9b9cdbd0103e3a69a44446a0aa6471a8/effects?cursor=121628667754319873-1&limit=10&order=desc"
      }
    },
    "_embedded": {
      "records": [
        {
          "_links": {
            "operation": {
              "href": "https://horizon.stellar.org/operations/121628667754319873"
            },
            "succeeds": {
              "href": "https://horizon.stellar.org/effects?order=desc&cursor=121628667754319873-1"
            },
            "precedes": {
              "href": "https://horizon.stellar.org/effects?order=asc&cursor=121628667754319873-1"
            }
          },
          "id": "0121628667754319873-0000000001",
          "paging_token": "121628667754319873-1",
          "account": "GAHK7EEG2WWHVKDNT4CEQFZGKF2LGDSW2IVM4S5DP42RBW3K6BTODB4A",
          "type": "account_credited",
          "type_i": 2,
          "created_at": "2020-02-20T21:18:33Z",
          "asset_type": "native",
          "amount": "1573.5112616"
        },
        {
          "_links": {
            "operation": {
              "href": "https://horizon.stellar.org/operations/121628667754319873"
            },
            "succeeds": {
              "href": "https://horizon.stellar.org/effects?order=desc&cursor=121628667754319873-2"
            },
            "precedes": {
              "href": "https://horizon.stellar.org/effects?order=asc&cursor=121628667754319873-2"
            }
          },
          "id": "0121628667754319873-0000000002",
          "paging_token": "121628667754319873-2",
          "account": "GA2XP4KMY4KWNPW4KUCUKYUF2J7Y6HO5HLPUEA3VPVSMYCM3TGNEZP5S",
          "type": "account_debited",
          "type_i": 3,
          "created_at": "2020-02-20T21:18:33Z",
          "asset_type": "native",
          "amount": "1573.5112616"
        }
      ]
    }
  }
}
```
