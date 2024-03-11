# getAccounts

### How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, Stellar, Network } from "@tatumio/tatum";

// Initialize the Tatum SDK for Stellar
const tatum = await TatumSDK.init<Stellar>({ network: Network.STELLAR });

// Define the account filters (Replace placeholders with actual values and remove redundant)
const filters: AccountFilters = {
  sponsor: "YOUR_SPONSOR_ACCOUNT_ID",
  asset: "YOUR_ASSET_CODE:ISSUER_ACCOUNT_ID",
  signer: "YOUR_SIGNER_ACCOUNT_ID",
  liquidityPool: "YOUR_LIQUIDITY_POOL_ID",
  cursor: 6606617478959105,
  order: "asc",
  limit: 10,
};

// List accounts based on the specified filters
const accounts = await tatum.rpc.getAccounts(filters);

// Log the list of accounts
console.log("List of Accounts:", accounts);

// Always destroy the Tatum SDK instance when done to stop any background processes
await tatum.destroy();
```

### Overview

The `getAccounts` method allows you to retrieve a list of accounts based on various filters, including signer, asset, liquidity pool, or sponsor.

**Please ensure that you are including a signer, sponsor, asset, or liquidity pool filter**.

### Example use cases:

1. **Account Filtering:**
   Developers and applications can use this method to filter and retrieve accounts based on specific criteria, such as signer, asset, or sponsor.

2. **Data Analysis:**
   Researchers and analysts can utilize this endpoint to gather account data for analysis and reporting.

3. **Pagination Support:**
   The method supports pagination using the `cursor`, `order`, and `limit` parameters for efficient data retrieval.

### Request Parameters

The `getAccounts` method requires the following parameters in camelCase:

- `sponsor` (string, optional):
  Account ID of the sponsor. Every account in the response will either be sponsored by the given account ID or have a subentry (trustline, offer, or data entry) which is sponsored by the given account ID.

- `asset` (string, optional):
  An issued asset represented as "code:issuerAccountID". Every account in the response will have a trustline for the given asset.

- `signer` (string, optional):
  Account ID of the signer. Every account in the response will have the given account ID as a signer.

- `liquidityPool` (string, optional):
  With this parameter, the results will include only accounts which have trustlines to the specified liquidity pool.

- `cursor` (number, optional):
  A number that points to a specific location in a collection of responses and is pulled from the `pagingToken` value of a record.

- `order` (string, optional):
  A designation of the order in which records should appear. Options include "asc" (ascending) or "desc" (descending). If this argument isn’t set, it defaults to "asc".

- `limit` (number, optional):
  The maximum number of records returned. The limit can range from 1 to 200 - an upper limit that is hardcoded in Horizon for performance reasons. If this argument isn’t designated, it defaults to 10.

### Return Object

The `getAccounts` method returns a list of accounts based on the provided filters.

(Note: The exact fields in the return object might vary based on the Stellar blockchain's implementation and version.)

```json
{
  "_links": {
    "self": {
      "href": "https://horizon.stellar.org/accounts?asset=USDC%3AGA5ZSEJYB37JRC5AVCIA5MOP4RHTM335X2KGX3IHOJAPP5RE34K4KZVN&cursor=&limit=10&order=asc"
    },
    "next": {
      "href": "https://horizon.stellar.org/accounts?asset=USDC%3AGA5ZSEJYB37JRC5AVCIA5MOP4RHTM335X2KGX3IHOJAPP5RE34K4KZVN&cursor=GA223H7O26KC7NWDEH6R4D5ITI35I4R7BH5VDLPFTSKMWH2RUZD474TJ&limit=10&order=asc"
    },
    "prev": {
      "href": "https://horizon.stellar.org/accounts?asset=USDC%3AGA5ZSEJYB37JRC5AVCIA5MOP4RHTM335X2KGX3IHOJAPP5RE34K4KZVN&cursor=GA2224DCGO3WHC4EALA2PR2BZEMAYZPBPTHS243ZYYWQMBWRPJSZH5A6&limit=10&order=desc"
    }
  },
  "_embedded": {
    "records": [
      {
        "_links": {
          "self": {
            "href": "https://horizon.stellar.org/accounts/GA2224DCGO3WHC4EALA2PR2BZEMAYZPBPTHS243ZYYWQMBWRPJSZH5A6"
          },
          "transactions": {
            "href": "https://horizon.stellar.org/accounts/GA2224DCGO3WHC4EALA2PR2BZEMAYZPBPTHS243ZYYWQMBWRPJSZH5A6/transactions{?cursor,limit,order}",
            "templated": true
          },
          "operations": {
            "href": "https://horizon.stellar.org/accounts/GA2224DCGO3WHC4EALA2PR2BZEMAYZPBPTHS243ZYYWQMBWRPJSZH5A6/operations{?cursor,limit,order}",
            "templated": true
          },
          "payments": {
            "href": "https://horizon.stellar.org/accounts/GA2224DCGO3WHC4EALA2PR2BZEMAYZPBPTHS243ZYYWQMBWRPJSZH5A6/payments{?cursor,limit,order}",
            "templated": true
          },
          "effects": {
            "href": "https://horizon.stellar.org/accounts/GA2224DCGO3WHC4EALA2PR2BZEMAYZPBPTHS243ZYYWQMBWRPJSZH5A6/effects{?cursor,limit,order}",
            "templated": true
          },
          "offers": {
            "href": "https://horizon.stellar.org/accounts/GA2224DCGO3WHC4EALA2PR2BZEMAYZPBPTHS243ZYYWQMBWRPJSZH5A6/offers{?cursor,limit,order}",
            "templated": true
          },
          "trades": {
            "href": "https://horizon.stellar.org/accounts/GA2224DCGO3WHC4EALA2PR2BZEMAYZPBPTHS243ZYYWQMBWRPJSZH5A6/trades{?cursor,limit,order}",
            "templated": true
          },
          "data": {
            "href": "https://horizon.stellar.org/accounts/GA2224DCGO3WHC4EALA2PR2BZEMAYZPBPTHS243ZYYWQMBWRPJSZH5A6/data/{key}",
            "templated": true
          }
        },
        "id": "GA2224DCGO3WHC4EALA2PR2BZEMAYZPBPTHS243ZYYWQMBWRPJSZH5A6",
        "account_id": "GA2224DCGO3WHC4EALA2PR2BZEMAYZPBPTHS243ZYYWQMBWRPJSZH5A6",
        "sequence": "194013564070002690",
        "sequence_ledger": 45173210,
        "sequence_time": "1677700612",
        "subentry_count": 1,
        "last_modified_ledger": 50415380,
        "last_modified_time": "2024-02-17T19:44:28Z",
        "thresholds": {
          "low_threshold": 0,
          "med_threshold": 0,
          "high_threshold": 0
        },
        "flags": {
          "auth_required": false,
          "auth_revocable": false,
          "auth_immutable": false,
          "auth_clawback_enabled": false
        },
        "balances": [
          {
            "balance": "0.0000000",
            "limit": "922337203685.4775807",
            "buying_liabilities": "0.0000000",
            "selling_liabilities": "0.0000000",
            "last_modified_ledger": 45173210,
            "is_authorized": true,
            "is_authorized_to_maintain_liabilities": true,
            "asset_type": "credit_alphanum4",
            "asset_code": "USDC",
            "asset_issuer": "GA5ZSEJYB37JRC5AVCIA5MOP4RHTM335X2KGX3IHOJAPP5RE34K4KZVN"
          },
          {
            "balance": "2.9975391",
            "buying_liabilities": "0.0000000",
            "selling_liabilities": "0.0000000",
            "asset_type": "native"
          }
        ],
        "signers": [
          {
            "weight": 1,
            "key": "GA2224DCGO3WHC4EALA2PR2BZEMAYZPBPTHS243ZYYWQMBWRPJSZH5A6",
            "type": "ed25519_public_key"
          }
        ],
        "data": {},
        "num_sponsoring": 0,
        "num_sponsored": 0,
        "paging_token": "GA2224DCGO3WHC4EALA2PR2BZEMAYZPBPTHS243ZYYWQMBWRPJSZH5A6"
      }
```
