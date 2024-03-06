# getLedgers

### How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, Stellar, Network } from "@tatumio/tatum";

// Initialize the Tatum SDK for Stellar
const tatum = await TatumSDK.init<Stellar>({ network: Network.STELLAR });

// Define optional parameters for listing ledgers (Replace placeholders with actual values and remove redundant)
const params = {
  cursor: "YOUR_CURSOR",
  order: "asc",
  limit: 10,
};

// List all ledgers or stream new ledgers as they close
const ledgers = await tatum.rpc.getLedgers(params);

// Log the list of ledgers
console.log("Ledgers:", ledgers);

// Always destroy the Tatum SDK instance when done to stop any background processes
await tatum.destroy();
```

### Overview

The `getLedgers` method allows you to retrieve a list of all ledgers on the Stellar blockchain. You can use this endpoint to either list all existing ledgers or stream new ledgers as they are created.

### Request Parameters

The `getLedgers` method supports the following optional request parameters:

- `cursor` (string, optional):
  Set the cursor to start listing ledgers from a specific ledger. If not specified, it starts from the earliest known ledger.

- `order` (string, optional):
  Set the order of listing, which can be either 'asc' (ascending) or 'desc' (descending). If not specified, it defaults to 'asc'.

- `limit` (integer, optional):
  Set the maximum number of ledgers to return in a single request. The limit can range from 1 to an upper limit hardcoded in Horizon for performance reasons. If not specified, it defaults to 10.

### Return Object

The `getLedgers` method returns a JSON object representing a list of ledgers on the Stellar blockchain. Each ledger entry includes various properties describing the ledger's characteristics, such as its sequence number, transaction count, and more.

(Note: The exact fields in the return object might vary based on the Stellar blockchain's implementation and version.)

```json
{
  "_links": {
    "self": {
      "href": "https://01-vinthill-068-01.rpc.tatum.io/ledgers?cursor=209252254065098752&limit=10&order=asc"
    },
    "next": {
      "href": "https://01-vinthill-068-01.rpc.tatum.io/ledgers?cursor=214305626686226432&limit=10&order=asc"
    },
    "prev": {
      "href": "https://01-vinthill-068-01.rpc.tatum.io/ledgers?cursor=214305588031520768&limit=10&order=desc"
    }
  },
  "_embedded": {
    "records": [
      {
        "_links": {
          "self": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/ledgers/49896908"
          },
          "transactions": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/ledgers/49896908/transactions{?cursor,limit,order}",
            "templated": true
          },
          "operations": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/ledgers/49896908/operations{?cursor,limit,order}",
            "templated": true
          },
          "payments": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/ledgers/49896908/payments{?cursor,limit,order}",
            "templated": true
          },
          "effects": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/ledgers/49896908/effects{?cursor,limit,order}",
            "templated": true
          }
        },
        "id": "377342fc7d2d3e8e8aebcc2bd069cebce97ef59142afcf3834187e27670b69e5",
        "paging_token": "214305588031520768",
        "hash": "377342fc7d2d3e8e8aebcc2bd069cebce97ef59142afcf3834187e27670b69e5",
        "prev_hash": "64b283aa8f123102b27334c9b0b4d0ba7baca635bc0fdee2471762755185fc8d",
        "sequence": 49896908,
        "successful_transaction_count": 122,
        "failed_transaction_count": 16,
        "operation_count": 422,
        "tx_set_operation_count": 444,
        "closed_at": "2024-01-13T08:44:04Z",
        "total_coins": "105443902087.3472865",
        "fee_pool": "4352705.3880757",
        "base_fee_in_stroops": 100,
        "base_reserve_in_stroops": 5000000,
        "max_tx_set_size": 1000,
        "protocol_version": 19,
        "header_xdr": "AAAAE2Syg6qPEjECsnM0ybC00Lp7rKY1vA/e4kcXYnVRhfyNp1FbP/TkMcsgPzxpkwmSanCPlHIkEEdIUluDz3RuOMAAAAAAZaJNVAAAAAAAAAABAAAAAJnoMfsa4vmDNtUy8T76WXcr2up7H7MouQjkXcMmro3YAAAAQOWiXUUgvk9prIYO2MowcNsSmp7gJ2pDeKstCpOS1JDvEGry7E0EIA2uNNuQicQkF0LPkzibuNqFIrRAlS3qwQt2V4R3dnRsy/hBIt5wz7oIBqVZNDN+w21lovTVBGxHHh5McTecKdm6+JSPeLr+qWjW8QFh7Z8+TOcgCjAtJkI1AvldzA6iHrPseVthAAAnlm6VrbUAAAEWAAAAAFZtQfcAAABkAExLQAAAA+jlo5p0S2VRLG/2qoS2AHIAqWpkozbDmPnGixgTrfRM4EhakDMvJGA2NlrXaNdrDghS8gBVmir/lvjB5aIM8CqaNZ3+bNIMjENN35Wl0SqvmRPHm1ba+rIkuDOUxRhPT5cTHtTJQ8xzm+/8UT+eTL84VX2S5mxKeyMkTW+VYnrVPwAAAAA="
      }
    ]
  }
}
```
