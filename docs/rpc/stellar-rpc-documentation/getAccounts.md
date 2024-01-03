# getAccounts

## How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, Stellar, Network } from '@tatumio/tatum';

// Initialize the Tatum SDK for Stellar
const tatum = await TatumSDK.init<Stellar>({ network: Network.STELLAR });

// Define the account filters (Replace placeholders with actual values)
const filters: AccountFilters = {
    sponsor: 'YOUR_SPONSOR_ACCOUNT_ID',
    asset: 'YOUR_ASSET_CODE:ISSUER_ACCOUNT_ID',
    signer: 'YOUR_SIGNER_ACCOUNT_ID',
    liquidityPool: 'YOUR_LIQUIDITY_POOL_ID',
    cursor: 6606617478959105,
    order: 'asc',
    limit: 10,
};

// List accounts based on the specified filters
const accounts = await tatum.rpc.getAccounts(filters);

// Log the list of accounts
console.log('List of Accounts:', accounts);

// Always destroy the Tatum SDK instance when done to stop any background processes
await tatum.destroy();
```

## Overview

The `getAccounts` method allows you to retrieve a list of accounts based on various filters, including signer, asset, liquidity pool, or sponsor. 

**Please ensure that you are including a signer, sponsor, asset, or liquidity pool filter**.

## Example use cases:

1. **Account Filtering:**
   Developers and applications can use this method to filter and retrieve accounts based on specific criteria, such as signer, asset, or sponsor.

2. **Data Analysis:**
   Researchers and analysts can utilize this endpoint to gather account data for analysis and reporting.

3. **Pagination Support:**
   The method supports pagination using the `cursor`, `order`, and `limit` parameters for efficient data retrieval.

## Request Parameters

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

## Return Object

The `getAccounts` method returns a list of accounts based on the provided filters.

(Note: The exact fields in the return object might vary based on the Stellar blockchain's implementation and version.)
