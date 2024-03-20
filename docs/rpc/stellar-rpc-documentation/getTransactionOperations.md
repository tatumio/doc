# getTransactionsOperations

### How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, Stellar, Network } from '@tatumio/tatum';

// Initialize the Tatum SDK for Stellar
const tatum = await TatumSDK.init<Stellar>({ network: Network.STELLAR });

// Define parameters (Replace placeholders with actual values and remove redundant)
const params = {
    transactionHash: 'TRANSACTION_HASH'
    cursor: 'YOUR_CURSOR',
    order: 'asc',
    limit: 10,
    includeFailed: true,
    join: true
};

// Get operations for a specific transaction
const transactionOperations = await tatum.rpc.getTransactionsOperations(params);

// Always destroy the Tatum SDK instance when done to stop any background processes
await tatum.destroy();
```

### Overview

The `getTransactionsOperations` method allows you to retrieve Successful operations for a specific transaction on the Stellar blockchain. You can use this method to fetch the operations associated with a particular transaction.

### Example use cases:

1. **Transaction Analysis:**
   Users can retrieve the operations related to a specific transaction for analysis and auditing purposes.

2. **Transaction History:**
   Developers can use this method to obtain the operations performed within a specific transaction.

### Request Parameters

The `getTransactionsOperations` method accepts the following optional parameters:

- `transaction_hash` (string, required):
  The hash of the transaction for which you want to retrieve operations.

- `cursor` (string, optional):
  An optional cursor to start listing operations from a specific point.

- `order` (string, optional):
  An optional parameter to specify the order of listing (asc or desc). If not provided, it defaults to 'asc'.

- `limit` (number, optional):
  An optional parameter to specify the maximum number of operations to return. The limit can range from 1 to 200.

- `includeFailed` (boolean, optional):
  An optional parameter to include failed operations. If set to true, failed operations will be included in the results. Defaults to false.

- `join` (boolean, optional):
  Set to transactions to include the transactions which created each of the operations in the response.

### Response Object

The `getTransactionsOperations` method returns an array of Successful operations related to the specified transaction. Each operation object contains information such as the operation type, source account, destination account, amount, and more.

(Note: The exact fields in the return object might vary based on the Stellar blockchain's implementation and version.)

```json
{
  "value": {
    "_links": {
      "self": {
        "href": "https://horizon.stellar.org/transactions/6b983a4e0dc3c04f4bd6b9037c55f70a09c434dfd01492be1077cf7ea68c2e4a/operations?cursor=&limit=10&order=asc"
      },
      "next": {
        "href": "https://horizon.stellar.org/transactions/6b983a4e0dc3c04f4bd6b9037c55f70a09c434dfd01492be1077cf7ea68c2e4a/operations?cursor=120133379185221636&limit=10&order=asc"
      },
      "prev": {
        "href": "https://horizon.stellar.org/transactions/6b983a4e0dc3c04f4bd6b9037c55f70a09c434dfd01492be1077cf7ea68c2e4a/operations?cursor=120133379185221633&limit=10&order=desc"
      }
    },
    "_embedded": {
      "records": [
        {
          "_links": {
            "self": {
              "href": "https://horizon.stellar.org/operations/120133379185221633"
            },
            "transaction": {
              "href": "https://horizon.stellar.org/transactions/6b983a4e0dc3c04f4bd6b9037c55f70a09c434dfd01492be1077cf7ea68c2e4a"
            },
            "effects": {
              "href": "https://horizon.stellar.org/operations/120133379185221633/effects"
            },
            "succeeds": {
              "href": "https://horizon.stellar.org/effects?order=desc&cursor=120133379185221633"
            },
            "precedes": {
              "href": "https://horizon.stellar.org/effects?order=asc&cursor=120133379185221633"
            }
          },
          "id": "120133379185221633",
          "paging_token": "120133379185221633",
          "transaction_successful": true,
          "source_account": "GDJX67SFY2N73H72TWMKKBQP5UPBNKBNUMNE2IGFKNES43S4327X6DHG",
          "type": "manage_buy_offer",
          "type_i": 12,
          "created_at": "2020-01-28T21:14:59Z",
          "transaction_hash": "6b983a4e0dc3c04f4bd6b9037c55f70a09c434dfd01492be1077cf7ea68c2e4a",
          "amount": "0.0000000",
          "price": "0.0001000",
          "price_r": {
            "n": 1,
            "d": 10000
          },
          "buying_asset_type": "native",
          "selling_asset_type": "credit_alphanum4",
          "selling_asset_code": "ETH",
          "selling_asset_issuer": "GBDEVU63Y6NTHJQQZIKVTC23NWLQVP3WJ2RI2OTSJTNYOIGICST6DUXR",
          "offer_id": 149983118
        }
      ]
    }
  }
}
```
