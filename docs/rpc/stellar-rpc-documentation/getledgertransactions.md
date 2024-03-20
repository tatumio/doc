# getLedgerTransactions

### How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, Stellar, Network } from "@tatumio/tatum";

// Initialize the Tatum SDK for Stellar
const tatum = await TatumSDK.init<Stellar>({ network: Network.STELLAR });

// Define the ledger sequence number and optional parameters (Replace placeholders with actual values)
const params = {
  sequence: "YOUR_LEDGER_SEQUENCE",
  cursor: "YOUR_CURSOR",
  order: "asc",
  limit: 10,
  includeFailed: true,
};

// Retrieve transactions for a specific ledger
const ledgerTransactions = await tatum.rpc.getLedgerTransactions(params);

// Log the list of ledger transactions
console.log("Ledger Transactions:", ledgerTransactions);

// Always destroy the Tatum SDK instance when done to stop any background processes
await tatum.destroy();
```

### Overview

The `getLedgerTransactions` method allows you to retrieve a list of successful transactions associated with a specific ledger on the Stellar blockchain. You can specify the ledger's sequence number and use optional parameters to customize the result.

### Request Parameters

The `getLedgerTransactions` method requires the following parameters:

- `sequence` (string, required):
  Specify the sequence number of the ledger for which you want to retrieve transactions.

- `cursor` (string, optional):
  Set the cursor to start listing transactions from a specific transaction within the ledger. If not specified, it starts from the beginning.

- `order` (string, optional):
  Set the order of listing, which can be either 'asc' (ascending) or 'desc' (descending). If not specified, it defaults to 'asc'.

- `limit` (integer, optional):
  Set the maximum number of transactions to return in a single request. The limit can range from 1 to an upper limit hardcoded in Horizon for performance reasons. If not specified, it defaults to 10.

- `includeFailed` (boolean, optional):
  Specify whether to include failed transactions in the results. Set to `true` to include failed transactions, or `false` to exclude them. If not specified, it defaults to `false`.

### Return Object

The `getLedgerTransactions` method returns a JSON object representing a list of successful transactions associated with the specified ledger. Each transaction entry includes various properties describing the transaction, such as its transaction hash, source account, operation details, and more.

(Note: The exact fields in the return object might vary based on the Stellar blockchain's implementation and version.)

```json
{
  "_links": {
    "self": {
      "href": "https://01-vinthill-068-01.rpc.tatum.io/ledgers/50121908/transactions?cursor=&limit=10&order=asc"
    },
    "next": {
      "href": "https://01-vinthill-068-01.rpc.tatum.io/ledgers/50121908/transactions?cursor=215271955673288704&limit=10&order=asc"
    },
    "prev": {
      "href": "https://01-vinthill-068-01.rpc.tatum.io/ledgers/50121908/transactions?cursor=215271955673128960&limit=10&order=desc"
    }
  },
  "_embedded": {
    "records": [
      {
        "_links": {
          "self": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/transactions/bf3e8c575c463bff1c23c1a7113b38d1cb79c983be62bf696dc96632ef00af47"
          },
          "account": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/accounts/GDZN22HI7CVATKDEVTBTMBIHJ7BXPRETNCGAG67E5DTSDG55MYMYEVCF"
          },
          "ledger": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/ledgers/50121908"
          },
          "operations": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/transactions/bf3e8c575c463bff1c23c1a7113b38d1cb79c983be62bf696dc96632ef00af47/operations{?cursor,limit,order}",
            "templated": true
          },
          "effects": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/transactions/bf3e8c575c463bff1c23c1a7113b38d1cb79c983be62bf696dc96632ef00af47/effects{?cursor,limit,order}",
            "templated": true
          },
          "precedes": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/transactions?order=asc&cursor=215271955673128960"
          },
          "succeeds": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/transactions?order=desc&cursor=215271955673128960"
          },
          "transaction": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/transactions/bf3e8c575c463bff1c23c1a7113b38d1cb79c983be62bf696dc96632ef00af47"
          }
        },
        "id": "bf3e8c575c463bff1c23c1a7113b38d1cb79c983be62bf696dc96632ef00af47",
        "paging_token": "215271955673128960",
        "successful": true,
        "hash": "bf3e8c575c463bff1c23c1a7113b38d1cb79c983be62bf696dc96632ef00af47",
        "ledger": 50121908,
        "created_at": "2024-01-28T14:07:11Z",
        "source_account": "GDZN22HI7CVATKDEVTBTMBIHJ7BXPRETNCGAG67E5DTSDG55MYMYEVCF",
        "source_account_sequence": "194986649040516756",
        "fee_account": "GDZN22HI7CVATKDEVTBTMBIHJ7BXPRETNCGAG67E5DTSDG55MYMYEVCF",
        "fee_charged": "509",
        "max_fee": "20000",
        "operation_count": 1,
        "envelope_xdr": "AAAAAgAAAADy3Wjo+KoJqGSswzYFB0/Dd8STaIwDe+To5yGbvWYZggAATiACtLtTAAD2lAAAAAIAAAAAAAAAAQAAAAAC/My1AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAQAAAAEAAAAAQRzN0pCPu4xfayKDwq6xMX/VwYcnmceHzEOZbo78ED0AAAADAAAAAVJJTwAAAAAAWrSjB98pZ3cZKDYNnHtv/R8NyN7bxLm0cchMZwIGJkQAAAAAAAAAAAAb+PkgiBTrBfXhAAAAAABXIYmRAAAAAAAAAAK9ZhmCAAAAQD/25UHfzLm0uL936wIoQY47ZDs+iJ+kIdgMqwOOvMJ2T11YH0ibtwhGoYrL7mVT0gSsYHV1d6H8DEgy03V/WQiO/BA9AAAAQHZps3K+2wdY6YN6uc4wk9UNdfDS6cxgyT2el/eGvVbyjrGw8vhv7vYckJwGrPzfpkrMeHHDIaK4mCu5oTO5VAw=",
        "result_xdr": "AAAAAAAAAf0AAAAAAAAAAQAAAAAAAAADAAAAAAAAAAAAAAABAAAAAEEczdKQj7uMX2sig8KusTF/1cGHJ5nHh8xDmW6O/BA9AAAAAFchiZEAAAABUklPAAAAAABatKMH3ylndxkoNg2ce2/9Hw3I3tvEubRxyExnAgYmRAAAAAAAAAAAABv4+SCIFOsF9eEAAAAAAAAAAAAAAAAA",
        "result_meta_xdr": "AAAAAgAAAAIAAAADAvzMtAAAAAAAAAAA8t1o6PiqCahkrMM2BQdPw3fEk2iMA3vk6Ochm71mGYIAAAAACdBVeQK0u1MAAPaTAAAAAAAAAAAAAAAAAAAAAAEAAAAAAAAAAAAAAQAAAAAAAAAAAAAAAAAAAAAAAAACAAAAAAAAAAAAAAAAAAAAAwAAAAAC/MygAAAAAGW2XxYAAAAAAAAAAQL8zLQAAAAAAAAAAPLdaOj4qgmoZKzDNgUHT8N3xJNojAN75OjnIZu9ZhmCAAAAAAnQVXkCtLtTAAD2lAAAAAAAAAAAAAAAAAAAAAABAAAAAAAAAAAAAAEAAAAAAAAAAAAAAAAAAAAAAAAAAgAAAAAAAAAAAAAAAAAAAAMAAAAAAvzMtAAAAABltl+PAAAAAAAAAAEAAAAGAAAAAwL8zK0AAAACAAAAAEEczdKQj7uMX2sig8KusTF/1cGHJ5nHh8xDmW6O/BA9AAAAAFchiZEAAAABUklPAAAAAABatKMH3ylndxkoNg2ce2/9Hw3I3tvEubRxyExnAgYmRAAAAAAAAAAAAADqnyCHuP8F9eEAAAAAAAAAAAAAAAAAAAAAAQL8zLQAAAACAAAAAEEczdKQj7uMX2sig8KusTF/1cGHJ5nHh8xDmW6O/BA9AAAAAFchiZEAAAABUklPAAAAAABatKMH3ylndxkoNg2ce2/9Hw3I3tvEubRxyExnAgYmRAAAAAAAAAAAABv4+SCIFOsF9eEAAAAAAAAAAAAAAAAAAAAAAwL8zK0AAAAAAAAAAEEczdKQj7uMX2sig8KusTF/1cGHJ5nHh8xDmW6O/BA9AAAAAAoWcL8Bo7K6AFnEggAAAAkAAAAAAAAAAAAAAAABAAAAAAAAAAAAAAEAAAABAAUAeQAAAAAAAAACAAAAAgAAAAAAAAAAAAAAAAAAAAMAAAAAApdErwAAAABjaWf8AAAAAAAAAAEC/My0AAAAAAAAAABBHM3SkI+7jF9rIoPCrrExf9XBhyeZx4fMQ5lujvwQPQAAAAAKFnC/AaOyugBZxIIAAAAJAAAAAAAAAAAAAAAAAQAAAAAAAAAAAAABAAAAAQCYq84AAAAAAAAAAgAAAAIAAAAAAAAAAAAAAAAAAAADAAAAAAKXRK8AAAAAY2ln/AAAAAAAAAADAvzMrQAAAAEAAAAAQRzN0pCPu4xfayKDwq6xMX/VwYcnmceHzEOZbo78ED0AAAABUklPAAAAAABatKMH3ylndxkoNg2ce2/9Hw3I3tvEubRxyExnAgYmRAAAAAAgStfkf////////NgAAAABAAAAAQAAAAD////+AAAAAAAA6qEAAAAAAAAAAAAAAAEC/My0AAAAAQAAAABBHM3SkI+7jF9rIoPCrrExf9XBhyeZx4fMQ5lujvwQPQAAAAFSSU8AAAAAAFq0owffKWd3GSg2DZx7b/0fDcje28S5tHHITGcCBiZEAAAAACBK1+R////////82AAAAAEAAAABAAAAAP////4AAAAAABv4+wAAAAAAAAAAAAAAAA==",
        "fee_meta_xdr": "AAAAAgAAAAMC/MygAAAAAAAAAADy3Wjo+KoJqGSswzYFB0/Dd8STaIwDe+To5yGbvWYZggAAAAAJ0Fd2ArS7UwAA9pMAAAAAAAAAAAAAAAAAAAAAAQAAAAAAAAAAAAABAAAAAAAAAAAAAAAAAAAAAAAAAAIAAAAAAAAAAAAAAAAAAAADAAAAAAL8zKAAAAAAZbZfFgAAAAAAAAABAvzMtAAAAAAAAAAA8t1o6PiqCahkrMM2BQdPw3fEk2iMA3vk6Ochm71mGYIAAAAACdBVeQK0u1MAAPaTAAAAAAAAAAAAAAAAAAAAAAEAAAAAAAAAAAAAAQAAAAAAAAAAAAAAAAAAAAAAAAACAAAAAAAAAAAAAAAAAAAAAwAAAAAC/MygAAAAAGW2XxYAAAAA",
        "memo_type": "none",
        "signatures": [
          "P/blQd/MubS4v3frAihBjjtkOz6In6Qh2AyrA468wnZPXVgfSJu3CEahisvuZVPSBKxgdXV3ofwMSDLTdX9ZCA==",
          "dmmzcr7bB1jpg3q5zjCT1Q118NLpzGDJPZ6X94a9VvKOsbDy+G/u9hyQnAas/N+mSsx4ccMhoriYK7mhM7lUDA=="
        ],
        "preconditions": {
          "ledgerbounds": {
            "min_ledger": 0,
            "max_ledger": 50121909
          }
        }
      }
    ]
  }
}
```
