# getTransactions

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
};

// Get a list of transactions
const transactions = await tatum.rpc.getTransactions(params);

// Always destroy the Tatum SDK instance when done to stop any background processes
await tatum.destroy();
```

### Overview

The `getTransactions` method allows you to retrieve a list of transactions on the Stellar blockchain. You can use this method in streaming mode to listen for new transactions as they are added to the Stellar ledger. When used in streaming mode, Horizon will start at the earliest known transaction unless a cursor is set, in which case it will start from that cursor. By setting the cursor value to now, you can stream transactions created since your request time.

### Example use cases:

1. **Transaction Monitoring:**
   Developers and applications can use this method to monitor and track all transactions on the Stellar network in real-time.

2. **Transaction Data Analysis:**
   Users can retrieve a list of transactions for analysis, reporting, and auditing purposes.

3. **Stream Transactions:**
   You can use streaming mode to receive real-time updates of new transactions on the Stellar ledger.

### Request Parameters

The `getTransactions` method accepts the following optional parameters:

- `cursor` (string, optional):
  An optional cursor to start listing transactions from a specific point.

- `order` (string, optional):
  An optional parameter to specify the order of listing (asc or desc). If not provided, it defaults to 'asc'.

- `limit` (number, optional):
  An optional parameter to specify the maximum number of transactions to return. The limit can range from 1 to 200.

- `includeFailed` (boolean, optional):
  An optional parameter to include failed transactions. If set to true, failed transactions will be included in the results. Defaults to false.

### Return Object

The `getTransactions` method returns an array of transactions on the Stellar blockchain. Each transaction object contains information such as the transaction ID, source account, destination account, amount, fee, and more.

(Note: The exact fields in the return object might vary based on the Stellar blockchain's implementation and version.)

```json
{
  "value": {
    "_links": {
      "self": {
        "href": "https://horizon.stellar.org/transactions?cursor=&limit=3&order=asc"
      },
      "next": {
        "href": "https://horizon.stellar.org/transactions?cursor=33736968114176&limit=3&order=asc"
      },
      "prev": {
        "href": "https://horizon.stellar.org/transactions?cursor=12884905984&limit=3&order=desc"
      }
    },
    "_embedded": {
      "records": [
        {
          "memo": "hello world",
          "_links": {
            "self": {
              "href": "https://horizon.stellar.org/transactions/3389e9f0f1a65f19736cacf544c2e825313e8447f569233bb8db39aa607c8889"
            },
            "account": {
              "href": "https://horizon.stellar.org/accounts/GAAZI4TCR3TY5OJHCTJC2A4QSY6CJWJH5IAJTGKIN2ER7LBNVKOCCWN7"
            },
            "ledger": {
              "href": "https://horizon.stellar.org/ledgers/3"
            },
            "operations": {
              "href": "https://horizon.stellar.org/transactions/3389e9f0f1a65f19736cacf544c2e825313e8447f569233bb8db39aa607c8889/operations{?cursor,limit,order}",
              "templated": true
            },
            "effects": {
              "href": "https://horizon.stellar.org/transactions/3389e9f0f1a65f19736cacf544c2e825313e8447f569233bb8db39aa607c8889/effects{?cursor,limit,order}",
              "templated": true
            },
            "precedes": {
              "href": "https://horizon.stellar.org/transactions?order=asc&cursor=12884905984"
            },
            "succeeds": {
              "href": "https://horizon.stellar.org/transactions?order=desc&cursor=12884905984"
            }
          },
          "id": "3389e9f0f1a65f19736cacf544c2e825313e8447f569233bb8db39aa607c8889",
          "paging_token": "12884905984",
          "successful": true,
          "hash": "3389e9f0f1a65f19736cacf544c2e825313e8447f569233bb8db39aa607c8889",
          "ledger": 3,
          "created_at": "2015-09-30T17:15:54Z",
          "source_account": "GAAZI4TCR3TY5OJHCTJC2A4QSY6CJWJH5IAJTGKIN2ER7LBNVKOCCWN7",
          "source_account_sequence": "1",
          "fee_charged": 300,
          "max_fee": 300,
          "operation_count": 3,
          "envelope_xdr": "AAAAAAAGUcmKO5465JxTSLQOQljwk2SfqAJmZSG6JH6wtqpwhAAABLAAAAAAAAAABAAAAAAAAAAEAAAALaGVsbG8gd29ybGQAAAAAAwAAAAAAAAAAAAAAABbxCy3mLg3hiTqX4VUEEp60pFOrJNxYM1JtxXTwXhY2AAAAAAvrwgAAAAAAAAAAAQAAAAAW8Qst5i4N4Yk6l+FVBBKetKRTqyTcWDNSbcV08F4WNgAAAAAN4Lazj4x61AAAAAAAAAAFAAAAAAAAAAAAAAAAAAAAAQAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAABLaqcIQAAAEBKwqWy3TaOxoGnfm9eUjfTRBvPf34dvDA0Nf+B8z4zBob90UXtuCqmQqwMCyH+okOI3c05br3khkH0yP4kCwcE",
          "result_xdr": "AAAAAAAAASwAAAAAAAAAAwAAAAAAAAAAAAAAAAAAAAAAAAABAAAAAAAAAAAAAAAFAAAAAAAAAAA=",
          "result_meta_xdr": "AAAAAAAAAAMAAAACAAAAAAAAAAMAAAAAAAAAABbxCy3mLg3hiTqX4VUEEp60pFOrJNxYM1JtxXTwXhY2AAAAAAvrwgAAAAADAAAAAAAAAAAAAAAAAAAAAAAAAAABAAAAAAAAAAAAAAAAAAAAAAAAAQAAAAMAAAAAAAAAAAGUcmKO5465JxTSLQOQljwk2SfqAJmZSG6JH6wtqpwhDeC2s5t4PNQAAAAAAAAAAQAAAAAAAAAAAAAAAAAAAAABAAAAAAAAAAAAAAAAAAAAAAAAAwAAAAEAAAADAAAAAAAAAAABlHJijueOuScU0i0DkJY8JNkn6gCZmUhuiR+sLaqcIQAAAAAL68IAAAAAAAAAAAEAAAAAAAAAAAAAAAAAAAAAAQAAAAAAAAAAAAAAAAAAAAAAAAMAAAADAAAAAAAAAAAW8Qst5i4N4Yk6l+FVBBKetKRTqyTcWDNSbcV08F4WNgAAAAAL68IAAAAAAwAAAAAAAAAAAAAAAAAAAAAAAAAAAQAAAAAAAAAAAAAAAAAAAAAAAAEAAAADAAAAAAAAAAAW8Qst5i4N4Yk6l+FVBBKetKRTqyTcWDNSbcV08F4WNg3gtrObeDzUAAAAAwAAAAAAAAAAAAAAAAAAAAAAAAAAAQAAAAAAAAAAAAAAAAAAAAAAAAEAAAABAAAAAwAAAAAAAAAAAZRyYo7njrknFNItA5CWPCTZJ+oAmZlIbokfrC2qnCEAAAAAC+vCAAAAAAAAAAABAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA=",
          "fee_meta_xdr": "AAAAAgAAAAMAAAABAAAAAAAAAAABlHJijueOuScU0i0DkJY8JNkn6gCZmUhuiR+sLaqcIQ3gtrOnZAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAQAAAAAAAAAAAAAAAAAAAAAAAAEAAAADAAAAAAAAAAABlHJijueOuScU0i0DkJY8JNkn6gCZmUhuiR+sLaqcIQ3gtrOnY/7UAAAAAAAAAAEAAAAAAAAAAAAAAAAAAAAAAQAAAAAAAAAAAAAAAAAAAA==",
          "memo_type": "text",
          "signatures": [
            "SsKlst02jsaBp35vXlI300Qbz39+HbwwNDX/gfM+MwaG/dFF7bgqpkKsDAsh/qJDiN3NOW695IZB9Mj+JAsHBA=="
          ]
        }
      ]
    }
  }
}
```
