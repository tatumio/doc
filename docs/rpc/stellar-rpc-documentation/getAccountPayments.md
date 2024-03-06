# getAccountPayments

### How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, Stellar, Network } from "@tatumio/tatum";

// Initialize the Tatum SDK for Stellar
const tatum = await TatumSDK.init<Stellar>({ network: Network.STELLAR });

// Define input parameters as an object (Replace placeholders with actual values and remove redundant)
const params = {
  accountId: "YOUR_ACCOUNT_ID",
  cursor: "now",
  order: "asc",
  limit: 10,
  includeFailed: true,
  join: true,
};

// Retrieve successful payments for a given account
const payments = await tatum.rpc.getAccountPayments(params);

// Log the list of payments
console.log("Account Payments:", payments);

// Always destroy the Tatum SDK instance when done to stop any background processes
await tatum.destroy();
```

### Overview

The `getAccountPayments` method allows you to retrieve successful payments for a given account on the Stellar blockchain. You can use this endpoint in streaming mode to listen for new payments for the specified account as they are added to the Stellar ledger. When called in streaming mode, Horizon will start at the earliest known payment unless a cursor is set, in which case it will start from that cursor. Setting the cursor value to 'now' allows you to stream payments created since your request time.

### Request Parameters

The `getAccountPayments` method accepts the following request parameters:

- `accountId` (string, required):
  The unique identifier (account ID) of the account for which you want to retrieve payments.

- `cursor` (string, optional):
  A cursor value that determines the starting point for retrieving payments. Set it to 'now' to stream payments created since your request time.

- `order` (string, optional):
  A designation of the order in which records should appear. Options include 'asc' (ascending) or 'desc' (descending). If this argument isn’t set, it defaults to 'asc'.

- `limit` (number, optional):
  The maximum number of records returned. It defines the number of payments to fetch in a single request.

- `includeFailed` (boolean, optional):
  A flag to indicate whether to include failed payments in the results. Set to `true` to include failed payments.

- `join` (boolean, optional):
  A flag to indicate whether to join payment data with relevant accounts. Set to `true` to join payment data with accounts.

### Return Object

The `getAccountPayments` method returns a JSON object containing the list of payments associated with the specified account. Each payment includes details such as its source, destination, amount, and other relevant information.

(Note: The exact fields in the return object might vary based on the Stellar blockchain's implementation and version.)

```json
{
    "_links": {
        "self": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/accounts/GA2224DCGO3WHC4EALA2PR2BZEMAYZPBPTHS243ZYYWQMBWRPJSZH5A6/payments?cursor=&limit=10&order=asc"
        },
        "next": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/accounts/GA2224DCGO3WHC4EALA2PR2BZEMAYZPBPTHS243ZYYWQMBWRPJSZH5A6/payments?cursor=216532408316960769&limit=10&order=asc"
        },
        "prev": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/accounts/GA2224DCGO3WHC4EALA2PR2BZEMAYZPBPTHS243ZYYWQMBWRPJSZH5A6/payments?cursor=216518179090239489&limit=10&order=desc"
        }
    },
    "_embedded": {
        "records": [
            {
                "_links": {
                    "self": {
                        "href": "https://01-vinthill-068-01.rpc.tatum.io/operations/216518179090239489"
                    },
                    "transaction": {
                        "href": "https://01-vinthill-068-01.rpc.tatum.io/transactions/57d2fccfb885169155913177f74d390a6675fcc28ccab529b8848cfcb1882435"
                    },
                    "effects": {
                        "href": "https://01-vinthill-068-01.rpc.tatum.io/operations/216518179090239489/effects"
                    },
                    "succeeds": {
                        "href": "https://01-vinthill-068-01.rpc.tatum.io/effects?order=desc&cursor=216518179090239489"
                    },
                    "precedes": {
                        "href": "https://01-vinthill-068-01.rpc.tatum.io/effects?order=asc&cursor=216518179090239489"
                    }
                },
                "id": "216518179090239489",
                "paging_token": "216518179090239489",
                "transaction_successful": true,
                "source_account": "GBOXZWWNZL3MQ7EP3KNL66WBVE4NH2UOLCMFKEKZFYQT5MOP2JDKENIZ",
                "type": "payment",
                "type_i": 1,
                "created_at": "2024-02-17T14:16:35Z",
                "transaction_hash": "57d2fccfb885169155913177f74d390a6675fcc28ccab529b8848cfcb1882435",
                "asset_type": "native",
                "from": "GBOXZWWNZL3MQ7EP3KNL66WBVE4NH2UOLCMFKEKZFYQT5MOP2JDKENIZ",
                "to": "GA2224DCGO3WHC4EALA2PR2BZEMAYZPBPTHS243ZYYWQMBWRPJSZH5A6",
                "amount": "0.0000100"
            },
    }
}
```
