# listAllPayments

### How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, Stellar, Network } from "@tatumio/tatum";

// Initialize the Tatum SDK for Stellar
const tatum = await TatumSDK.init<Stellar>({ network: Network.STELLAR });

// Define parameters (Replace placeholders with actual values and remove redundant)
const params = {
  cursor: "YOUR_CURSOR",
  order: "asc",
  limit: 10,
  includeFailed: true,
  join: true,
};

// List all successful payment-related operations
const allPayments = await tatum.rpc.listAllPayments(params);

// Always destroy the Tatum SDK instance when done to stop any background processes
await tatum.destroy();
```

### Overview

The `listAllPayments` method allows you to list all successful payment-related operations on the Stellar blockchain.

### Example use cases:

1. **Payment Monitoring:**
   Developers and applications can use this method to monitor and retrieve information about all successful payment-related operations on the Stellar network.

2. **Payment Filtering:**
   Platform administrators can filter and search for specific payments based on various criteria, such as cursor, order, and more.

3. **Streaming Payments:**
   Users can use streaming mode to listen for new payments as they are added to the Stellar ledger.

### Request Parameters

The `listAllPayments` method accepts a single `params` object with the following properties:

- `cursor` (string, optional):
  An optional cursor to start listing payments from a specific point.

- `order` (string, optional):
  An optional parameter to specify the order of listing (asc or desc). If not provided, it defaults to 'asc'.

- `limit` (number, optional):
  An optional parameter to specify the maximum number of payments to return. The limit can range from 1 to 200.

- `includeFailed` (boolean, optional):
  An optional parameter to include failed payments. If set to true, failed payments will be included in the results. Defaults to false.

- `join` (boolean, optional):
  An optional parameter to join results. If set to true, results will be joined. Defaults to false.

### Return Object

The `listAllPayments` method returns an array of successful payment-related operations on the Stellar blockchain. Each operation object corresponds to a payment operation, and it contains information such as the operation ID, source account, destination account, amount, asset, and more.

(Note: The exact fields in the return object might vary based on the Stellar blockchain's implementation and version.)

```json
{
  "_links": {
    "self": {
      "href": "https://01-vinthill-068-01.rpc.tatum.io/payments?cursor=&limit=10&order=asc"
    },
    "next": {
      "href": "https://01-vinthill-068-01.rpc.tatum.io/payments?cursor=215271955673706503&limit=10&order=asc"
    },
    "prev": {
      "href": "https://01-vinthill-068-01.rpc.tatum.io/payments?cursor=215271955673169921&limit=10&order=desc"
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
