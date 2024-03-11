# getLedgersTransactions

### How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, Stellar, Network } from "@tatumio/tatum";

// Initialize the Tatum SDK for Stellar
const tatum = await TatumSDK.init<Stellar>({ network: Network.STELLAR });

// Define the ledger sequence number and optional parameters (Replace placeholders with actual values and remove redundant)
const params = {
  sequence: "YOUR_LEDGER_SEQUENCE",
  cursor: "YOUR_CURSOR",
  order: "asc",
  limit: 10,
  includeFailed: true,
};

// Retrieve transactions for a specific ledger
const ledgerTransactions = await tatum.rpc.getLedgersTransactions(params);

// Log the list of ledger transactions
console.log("Ledger Transactions:", ledgerTransactions);

// Always destroy the Tatum SDK instance when done to stop any background processes
await tatum.destroy();
```

### Overview

The `getLedgersTransactions` method allows you to retrieve a list of successful transactions associated with a specific ledger on the Stellar blockchain. You can specify the ledger's sequence number and use optional parameters to customize the result.

### Request Parameters

The `getLedgersTransactions` method requires the following parameters:

- `sequence` (string, required): Specify the sequence number of the ledger for which you want to retrieve transactions.
- `cursor` (string, optional): Set the cursor to start listing transactions from a specific transaction within the ledger. If not specified, it starts from the beginning.
- `order` (string, optional): Set the order of listing, which can be either 'asc' (ascending) or 'desc' (descending). If not specified, it defaults to 'asc'.
- `limit` (integer, optional): Set the maximum number of transactions to return in a single request. The limit can range from 1 to an upper limit hardcoded in Horizon for performance reasons. If not specified, it defaults to 10.
- `includeFailed` (boolean, optional): Specify whether to include failed transactions in the results. Set to `true` to include failed transactions, or `false` to exclude them. If not specified, it defaults to `false`.

### Return Object

The `getLedgersTransactions` method returns a JSON object representing a list of successful transactions associated with the specified ledger. Each transaction entry includes various properties describing the transaction, such as its transaction hash, source account, operation details, and more.

(Note: The exact fields in the return object might vary based on the Stellar blockchain's implementation and version.)

```json
{
  "_links": {
    "self": {
      "href": "https://01-vinthill-068-01.rpc.tatum.io/ledgers/49896908/transactions?cursor=&limit=10&order=asc"
    },
    "next": {
      "href": "https://01-vinthill-068-01.rpc.tatum.io/ledgers/49896908/transactions?cursor=214305588031565824&limit=10&order=asc"
    },
    "prev": {
      "href": "https://01-vinthill-068-01.rpc.tatum.io/ledgers/49896908/transactions?cursor=214305588031524864&limit=10&order=desc"
    }
  },
  "_embedded": {
    "records": [
      {
        "_links": {
          "self": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/transactions/83e580608afbc0d269107dd92629ae5be4a039c2751896bdf8e357a9cd947ea4"
          },
          "account": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/accounts/GAZCCHIATB5Z6ATORF46EDXRUKVDNGHOFL3NKG7Y577NBTSOWMJX2DOS"
          },
          "ledger": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/ledgers/49896908"
          },
          "operations": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/transactions/83e580608afbc0d269107dd92629ae5be4a039c2751896bdf8e357a9cd947ea4/operations{?cursor,limit,order}",
            "templated": true
          },
          "effects": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/transactions/83e580608afbc0d269107dd92629ae5be4a039c2751896bdf8e357a9cd947ea4/effects{?cursor,limit,order}",
            "templated": true
          },
          "precedes": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/transactions?order=asc&cursor=214305588031524864"
          },
          "succeeds": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/transactions?order=desc&cursor=214305588031524864"
          },
          "transaction": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/transactions/83e580608afbc0d269107dd92629ae5be4a039c2751896bdf8e357a9cd947ea4"
          }
        },
        "id": "83e580608afbc0d269107dd92629ae5be4a039c2751896bdf8e357a9cd947ea4",
        "paging_token": "214305588031524864",
        "successful": true,
        "hash": "83e580608afbc0d269107dd92629ae5be4a039c2751896bdf8e357a9cd947ea4",
        "ledger": 49896908,
        "created_at": "2024-01-13T08:44:04Z",
        "source_account": "GAZCCHIATB5Z6ATORF46EDXRUKVDNGHOFL3NKG7Y577NBTSOWMJX2DOS",
        "source_account_sequence": "157780425393618577",
        "fee_account": "GAZCCHIATB5Z6ATORF46EDXRUKVDNGHOFL3NKG7Y577NBTSOWMJX2DOS",
        "fee_charged": "100",
        "max_fee": "100",
        "operation_count": 1,
        "envelope_xdr": "AAAAAgAAAAAyIR0AmHufAm6JeeIO8aKqNpjuKvbVG/jv/tDOTrMTfQAAAGQCMIx2ABi+kQAAAAEAAAAAAAAAAAAAAABlok1uAAAAAAAAAAEAAAAAAAAADAAAAAAAAAABU1NMWAAAAABOU2N5aRNltdxYaKXhwiK5X5GkCkz4nPf6ac+axwxIfQAAAPXibPzGAAFyjwCYloAAAAAAVml2xgAAAAAAAAABTrMTfQAAAEDf1H9htFjhgBsmeu+wg7k0wWJzTsX0bPmUuulWF2cW6A83T0Dc/iea50iARBqCjlF0u7ANpEmOWdhK2CW3/UAF",
        "result_xdr": "AAAAAAAAAGQAAAAAAAAAAQAAAAAAAAAMAAAAAAAAAAAAAAABAAAAADIhHQCYe58Cbol54g7xoqo2mO4q9tUb+O/+0M5OsxN9AAAAAFZpdsYAAAAAAAAAAVNTTFgAAAAATlNjeWkTZbXcWGil4cIiuV+RpApM+Jz3+mnPmscMSH0AAAACVSDxEQCYloAAAXKPAAAAAAAAAAAAAAAA",
        "result_meta_xdr": "AAAAAgAAAAIAAAADAvldzAAAAAAAAAAAMiEdAJh7nwJuiXniDvGiqjaY7ir21Rv47/7Qzk6zE30AAAAW0Mp5WAIwjHYAGL6QAAAAJgAAAAAAAAAAAAAAAAEAAAAAAAAAAAAAAQAAACJBvvGgAAAAFba2mA4AAAACAAAAAAAAAAAAAAAAAAAAAwAAAAAC+V3LAAAAAGWiTU4AAAAAAAAAAQL5XcwAAAAAAAAAADIhHQCYe58Cbol54g7xoqo2mO4q9tUb+O/+0M5OsxN9AAAAFtDKeVgCMIx2ABi+kQAAACYAAAAAAAAAAAAAAAABAAAAAAAAAAAAAAEAAAAiQb7xoAAAABW2tpgOAAAAAgAAAAAAAAAAAAAAAAAAAAMAAAAAAvldzAAAAABlok1UAAAAAAAAAAEAAAAGAAAAAwL5XOYAAAACAAAAADIhHQCYe58Cbol54g7xoqo2mO4q9tUb+O/+0M5OsxN9AAAAAFZpdsYAAAAAAAAAAVNTTFgAAAAATlNjeWkTZbXcWGil4cIiuV+RpApM+Jz3+mnPmscMSH0AAAACVSF7XwCYloAAAXKPAAAAAAAAAAAAAAAAAAAAAQL5XcwAAAACAAAAADIhHQCYe58Cbol54g7xoqo2mO4q9tUb+O/+0M5OsxN9AAAAAFZpdsYAAAAAAAAAAVNTTFgAAAAATlNjeWkTZbXcWGil4cIiuV+RpApM+Jz3+mnPmscMSH0AAAACVSDxEQCYloAAAXKPAAAAAAAAAAAAAAAAAAAAAwL5XcsAAAABAAAAADIhHQCYe58Cbol54g7xoqo2mO4q9tUb+O/+0M5OsxN9AAAAAVNTTFgAAAAATlNjeWkTZbXcWGil4cIiuV+RpApM+Jz3+mnPmscMSH0AAAEkapBph3zmbFDihAAAAAAAAQAAAAEAAAOQdGO06wAAAPIDPIERAAAAAAAAAAAAAAABAvldzAAAAAEAAAAAMiEdAJh7nwJuiXniDvGiqjaY7ir21Rv47/7Qzk6zE30AAAABU1NMWAAAAABOU2N5aRNltdxYaKXhwiK5X5GkCkz4nPf6ac+axwxIfQAAASRqkGmHfOZsUOKEAAAAAAABAAAAAQAAA5B0KsGBAAAA8gM8gREAAAAAAAAAAAAAAAMC+V3MAAAAAAAAAAAyIR0AmHufAm6JeeIO8aKqNpjuKvbVG/jv/tDOTrMTfQAAABbQynlYAjCMdgAYvpEAAAAmAAAAAAAAAAAAAAAAAQAAAAAAAAAAAAABAAAAIkG+8aAAAAAVtraYDgAAAAIAAAAAAAAAAAAAAAAAAAADAAAAAAL5XcwAAAAAZaJNVAAAAAAAAAABAvldzAAAAAAAAAAAMiEdAJh7nwJuiXniDvGiqjaY7ir21Rv47/7Qzk6zE30AAAAW0Mp5WAIwjHYAGL6RAAAAJgAAAAAAAAAAAAAAAAEAAAAAAAAAAAAAAQAAACJBvvGgAAAAFba2DcAAAAACAAAAAAAAAAAAAAAAAAAAAwAAAAAC+V3MAAAAAGWiTVQAAAAAAAAAAA==",
        "fee_meta_xdr": "AAAAAgAAAAMC+V3LAAAAAAAAAAAyIR0AmHufAm6JeeIO8aKqNpjuKvbVG/jv/tDOTrMTfQAAABbQynm8AjCMdgAYvpAAAAAmAAAAAAAAAAAAAAAAAQAAAAAAAAAAAAABAAAAIkG+8aAAAAAVtraYDgAAAAIAAAAAAAAAAAAAAAAAAAADAAAAAAL5XcsAAAAAZaJNTgAAAAAAAAABAvldzAAAAAAAAAAAMiEdAJh7nwJuiXniDvGiqjaY7ir21Rv47/7Qzk6zE30AAAAW0Mp5WAIwjHYAGL6QAAAAJgAAAAAAAAAAAAAAAAEAAAAAAAAAAAAAAQAAACJBvvGgAAAAFba2mA4AAAACAAAAAAAAAAAAAAAAAAAAAwAAAAAC+V3LAAAAAGWiTU4AAAAA",
        "memo_type": "none",
        "signatures": [
          "39R/YbRY4YAbJnrvsIO5NMFic07F9Gz5lLrpVhdnFugPN09A3P4nmudIgEQago5RdLuwDaRJjlnYStglt/1ABQ=="
        ],
        "valid_after": "1970-01-01T00:00:00Z",
        "valid_before": "2024-01-13T08:44:30Z",
        "preconditions": {
          "timebounds": {
            "min_time": "0",
            "max_time": "1705135470"
          }
        }
      }
    ]
  }
}
```
