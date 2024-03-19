# getLedgerPayments

### How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, Stellar, Network } from '@tatumio/tatum';

// Initialize the Tatum SDK for Stellar
const tatum = await TatumSDK.init<Stellar>({ network: Network.STELLAR });

// Define the ledger sequence number and optional parameters (Replace placeholders with actual values)
const params = {
    sequence: 'YOUR_LEDGER_SEQUENCE',
    cursor: 'YOUR_CURSOR',
    order: 'asc',
    limit: 10,
    includeFailed: true
    join: 'inner',
};

// Retrieve payments related to a specific ledger
const ledgerPayments = await tatum.rpc.getLedgerPayments(params);

// Always destroy the Tatum SDK instance when done to stop any background processes
await tatum.destroy();
```

### Overview

The `getLedgerPayments` method allows you to retrieve all payment-related operations in a specific Stellar ledger. This includes operations such as `create_account`, `payment`, `path_payment`, and `account_merge`.

### Example use cases:

1. **Payment Analysis:**
   Developers and applications can use this method to analyze payment-related operations within a specific ledger.

2. **Transaction Tracking:**
   Tracking and monitoring payments made within a specific ledger for auditing or analysis purposes.

3. **Historical Data Retrieval:**
   Researchers and analysts can retrieve payment-related data for historical analysis and record-keeping.

### Request Parameters

The `getLedgerPayments` method requires the following parameters:

- `sequence` (string, required):
  The sequence number of the ledger for which you want to retrieve payment-related operations.

- `cursor` (string, optional):
  An optional cursor to start listing payments from a specific point within the ledger.

- `order` (string, optional):
  An optional parameter to specify the order of listing (asc or desc). If not provided, it defaults to 'asc'.

- `limit` (number, optional):
  An optional parameter to specify the maximum number of payments to return. The limit can range from 1 to 200.

- `includeFailed` (boolean, optional):
  An optional parameter to include failed payments in the results (true or false). If not provided, it defaults to 'false'.

- `join` (string, optional):
  An optional parameter to specify the join type (inner or left). If not provided, it defaults to 'inner'.

### Return Object

The `getLedgerPayments` method returns an array of payment-related operations within the specified ledger. Each operation includes details such as the sender, receiver, asset, amount, and more.

(Note: The exact fields in the return object might vary based on the Stellar blockchain's implementation and version.)

```json
{
  "_links": {
    "self": {
      "href": "https://01-vinthill-068-01.rpc.tatum.io/ledgers/50121908/payments?cursor=&limit=10&order=asc"
    },
    "next": {
      "href": "https://01-vinthill-068-01.rpc.tatum.io/ledgers/50121908/payments?cursor=215271955673706503&limit=10&order=asc"
    },
    "prev": {
      "href": "https://01-vinthill-068-01.rpc.tatum.io/ledgers/50121908/payments?cursor=215271955673169921&limit=10&order=desc"
    }
  },
  "_embedded": {
    "records": [
      {
        "_links": {
          "self": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/operations/215271955673169921"
          },
          "transaction": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/transactions/c2b52adc99766007cf1cb1f218b2c40b9771123450282e0d6e3c0be69159880d"
          },
          "effects": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/operations/215271955673169921/effects"
          },
          "succeeds": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/effects?order=desc&cursor=215271955673169921"
          },
          "precedes": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/effects?order=asc&cursor=215271955673169921"
          }
        },
        "id": "215271955673169921",
        "paging_token": "215271955673169921",
        "transaction_successful": true,
        "source_account": "GCEETSI6ZGG3CS37YUFAUKCCJSCOILXL43JOJVZ435KBJ5NICDYY4EMP",
        "type": "path_payment_strict_send",
        "type_i": 13,
        "created_at": "2024-01-28T14:07:11Z",
        "transaction_hash": "c2b52adc99766007cf1cb1f218b2c40b9771123450282e0d6e3c0be69159880d",
        "asset_type": "credit_alphanum4",
        "asset_code": "yXLM",
        "asset_issuer": "GARDNV3Q7YGT4AKSDF25LT32YSCCW4EV22Y2TV3I2PU2MMXJTEDL5T55",
        "from": "GCEETSI6ZGG3CS37YUFAUKCCJSCOILXL43JOJVZ435KBJ5NICDYY4EMP",
        "to": "GCEETSI6ZGG3CS37YUFAUKCCJSCOILXL43JOJVZ435KBJ5NICDYY4EMP",
        "amount": "1.0291984",
        "path": [
          {
            "asset_type": "credit_alphanum4",
            "asset_code": "PL",
            "asset_issuer": "GBV34DLSYPWQYJTWGC6AYDRNSU7YM244SD4NLPBLDR7D74PZMFEL5OMG"
          },
          {
            "asset_type": "credit_alphanum4",
            "asset_code": "XRP",
            "asset_issuer": "GCNSGHUCG5VMGLT5RIYYZSO7VQULQKAJ62QA33DBC5PPBSO57LFWVV6P"
          },
          {
            "asset_type": "credit_alphanum4",
            "asset_code": "XRP",
            "asset_issuer": "GBXRPL45NPHCVMFFAYZVUVFFVKSIZ362ZXFP7I2ETNQ3QKZMFLPRDTD5"
          },
          {
            "asset_type": "credit_alphanum4",
            "asset_code": "SHX",
            "asset_issuer": "GDSTRSHXHGJ7ZIVRBXEYE5Q74XUVCUSEKEBR7UCHEUUEK72N7I7KJ6JH"
          }
        ],
        "source_amount": "1.0000000",
        "destination_min": "1.0000000",
        "source_asset_type": "native"
      }
    ]
  }
}
```
