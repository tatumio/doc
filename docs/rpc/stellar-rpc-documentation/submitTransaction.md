# submitTransaction

### How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, Stellar, Network } from "@tatumio/tatum";

// Initialize the Tatum SDK for Stellar
const tatum = await TatumSDK.init<Stellar>({ network: Network.STELLAR });

// Define parameters (Replace placeholders with actual values and remove redundant)
const tx = "BASE64_ENCODED_TRANSACTION_XDR";

// Submit a transaction
const result = await tatum.rpc.submitTransaction(tx);

// Always destroy the Tatum SDK instance when done to stop any background processes
await tatum.destroy();
```

### Overview

The `submitTransaction` method allows you to submit a transaction to the Stellar network. It takes a single, required parameter, which is the base64-encoded XDR of the transaction. If you submit a transaction that has already been included in a ledger, this endpoint will return the same response as would have been returned for the original transaction submission. This allows for safe resubmission of transactions in error scenarios, as highlighted in the error-handling guide.

### Example use cases:

1. **Transaction Submission:**
   Developers and applications can use this method to submit transactions to the Stellar network.

### Request Parameters

The `submitTransaction` method accepts the following parameters:

- `tx` (string, required):
  The base64-encoded XDR of the transaction to be submitted.

### Response Object

The `submitTransaction` method returns the result of the transaction submission. The exact response object may vary based on the Stellar blockchain's implementation and version.

```json
{
  "value": {
    "memo": "Test Transaction",
    "memo_bytes": "VGVzdCBUcmFuc2FjdGlvbg==",
    "_links": {
      "self": {
        "href": "https://horizon-testnet.stellar.org/transactions/8ef0c6d60357bf91b0b0d7800b747ff02bf73117d3e017690cbff641ca67f124"
      },
      "account": {
        "href": "https://horizon-testnet.stellar.org/accounts/GCIHAQVWZH2AB5BB5NP63FBSIREG77LQZZNUVKD2LN2IOCLOT6N72MJN"
      },
      "ledger": {
        "href": "https://horizon-testnet.stellar.org/ledgers/139575"
      },
      "operations": {
        "href": "https://horizon-testnet.stellar.org/transactions/8ef0c6d60357bf91b0b0d7800b747ff02bf73117d3e017690cbff641ca67f124/operations{?cursor,limit,order}",
        "templated": true
      },
      "effects": {
        "href": "https://horizon-testnet.stellar.org/transactions/8ef0c6d60357bf91b0b0d7800b747ff02bf73117d3e017690cbff641ca67f124/effects{?cursor,limit,order}",
        "templated": true
      },
      "precedes": {
        "href": "https://horizon-testnet.stellar.org/transactions?order=asc&cursor=599470060347392"
      },
      "succeeds": {
        "href": "https://horizon-testnet.stellar.org/transactions?order=desc&cursor=599470060347392"
      },
      "transaction": {
        "href": "https://horizon-testnet.stellar.org/transactions/8ef0c6d60357bf91b0b0d7800b747ff02bf73117d3e017690cbff641ca67f124"
      }
    },
    "id": "8ef0c6d60357bf91b0b0d7800b747ff02bf73117d3e017690cbff641ca67f124",
    "paging_token": "599470060347392",
    "successful": true,
    "hash": "8ef0c6d60357bf91b0b0d7800b747ff02bf73117d3e017690cbff641ca67f124",
    "ledger": 139575,
    "created_at": "2021-03-25T21:14:11Z",
    "source_account": "GCIHAQVWZH2AB5BB5NP63FBSIREG77LQZZNUVKD2LN2IOCLOT6N72MJN",
    "source_account_sequence": "599336916353025",
    "fee_account": "GCIHAQVWZH2AB5BB5NP63FBSIREG77LQZZNUVKD2LN2IOCLOT6N72MJN",
    "fee_charged": "100",
    "max_fee": "100",
    "operation_count": 1,
    "envelope_xdr": "AAAAAgAAAACQcEK2yfQA9CHrX+2UMkRIb/1wzltKqHpbdIcJbp+b/QAAAGQAAiEYAAAAAQAAAAEAAAAAAAAAAAAAAABgXP3QAAAAAQAAABBUZXN0IFRyYW5zYWN0aW9uAAAAAQAAAAAAAAABAAAAAJBwQrbJ9AD0Ietf7ZQyREhv/XDOW0qoelt0hwlun5v9AAAAAAAAAAAF9eEAAAAAAAAAAAFun5v9AAAAQKdJnG8QRiv9xGp1Oq7ACv/xR2BnNqjfUHrGNua7m4tWbrun3+GmAj6ca3xz+4ZppWRTbvTUcCxvpbHERZ85QgY=",
    "result_xdr": "AAAAAAAAAGQAAAAAAAAAAQAAAAAAAAABAAAAAAAAAAA=",
    "result_meta_xdr": "AAAAAgAAAAIAAAADAAIhNwAAAAAAAAAAkHBCtsn0APQh61/tlDJESG/9cM5bSqh6W3SHCW6fm/0AAAAXSHbnnAACIRgAAAAAAAAAAAAAAAAAAAAAAAAAAAEAAAAAAAAAAAAAAAAAAAAAAAABAAIhNwAAAAAAAAAAkHBCtsn0APQh61/tlDJESG/9cM5bSqh6W3SHCW6fm/0AAAAXSHbnnAACIRgAAAABAAAAAAAAAAAAAAAAAAAAAAEAAAAAAAAAAAAAAAAAAAAAAAABAAAAAAAAAAA=",
    "fee_meta_xdr": "AAAAAgAAAAMAAiEYAAAAAAAAAACQcEK2yfQA9CHrX+2UMkRIb/1wzltKqHpbdIcJbp+b/QAAABdIdugAAAIhGAAAAAAAAAAAAAAAAAAAAAAAAAAAAQAAAAAAAAAAAAAAAAAAAAAAAAEAAiE3AAAAAAAAAACQcEK2yfQA9CHrX+2UMkRIb/1wzltKqHpbdIcJbp+b/QAAABdIduecAAIhGAAAAAAAAAAAAAAAAAAAAAAAAAAAAQAAAAAAAAAAAAAAAAAAAA==",
    "memo_type": "text",
    "max_fee": "100",
    "operation_count": 1,
    "envelope_xdr": "AAAAAgAAAACQcEK2yfQA9CHrX+2UMkRIb/1wzltKqHpbdIcJbp+b/QAAAGQAAiEYAAAAAQAAAAEAAAAAAAAAAAAAAABgXP3QAAAAAQAAABBUZXN0IFRyYW5zYWN0aW9uAAAAAQAAAAAAAAABAAAAAJBwQrbJ9AD0Ietf7ZQyREhv/XDOW0qoelt0hwlun5v9AAAAAAAAAAAF9eEAAAAAAAAAAAFun5v9AAAAQKdJnG8QRiv9xGp1Oq7ACv/xR2BnNqjfUHrGNua7m4tWbrun3+GmAj6ca3xz+4ZppWRTbvTUcCxvpbHERZ85QgY=",
    "result_xdr": "AAAAAAAAAGQAAAAAAAAAAQAAAAAAAAABAAAAAAAAAAA=",
    "result_meta_xdr": "AAAAAgAAAAIAAAADAAIhNwAAAAAAAAAAkHBCtsn0APQh61/tlDJESG/9cM5bSqh6W3SHCW6fm/0AAAAXSHbnnAACIRgAAAAAAAAAAAAAAAAAAAAAAAAAAAEAAAAAAAAAAAAAAAAAAAAAAAABAAIhNwAAAAAAAAAAkHBCtsn0APQh61/tlDJESG/9cM5bSqh6W3SHCW6fm/0AAAAXSHbnnAACIRgAAAABAAAAAAAAAAAAAAAAAAAAAAEAAAAAAAAAAAAAAAAAAAAAAAABAAAAAAAAAAA=",
    "fee_meta_xdr": "AAAAAgAAAAMAAiEYAAAAAAAAAACQcEK2yfQA9CHrX+2UMkRIb/1wzltKqHpbdIcJbp+b/QAAABdIdugAAAIhGAAAAAAAAAAAAAAAAAAAAAAAAAAAAQAAAAAAAAAAAAAAAAAAAAAAAAEAAiE3AAAAAAAAAACQcEK2yfQA9CHrX+2UMkRIb/1wzltKqHpbdIcJbp+b/QAAABdIduecAAIhGAAAAAAAAAAAAAAAAAAAAAAAAAAAAQAAAAAAAAAAAAAAAAAAAA==",
    "memo_type": "text",
    "signatures": [
      "p0mcbxBGK/3EanU6rsAK//FHYGc2qN9QesY25rubi1Zuu6ff4aYCPpxrfHP7hmmlZFNu9NRwLG+lscRFnzlCBg=="
    ],
    "valid_after": "1970-01-01T00:00:00Z",
    "valid_before": "2021-03-25T21:17:04Z"
  }
}
```
