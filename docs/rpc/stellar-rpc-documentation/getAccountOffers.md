# getAccountOffers

### How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, Stellar, Network } from '@tatumio/tatum';

// Initialize the Tatum SDK for Stellar
const tatum = await TatumSDK.init<Stellar>({ network: Network.STELLAR });

// Define input parameters as an object (Replace placeholders with actual values)
const params = {
    accountId: 'YOUR_ACCOUNT_ID', 
    cursor: 'now', 
    order: 'asc', 
    limit: 10, 
};

// Retrieve all offers currently open for a given account
const offers = await tatum.rpc.getAccountOffers(params);

// Log the list of offers
console.log('Account Offers:', offers);

// Always destroy the Tatum SDK instance when done to stop any background processes
await tatum.destroy();
```

### Overview

The `getAccountOffers` method allows you to retrieve all offers that a specific account has currently open on the Stellar blockchain. You can use this endpoint in streaming mode to listen for new offers for the specified account as they are added to the Stellar ledger. When called in streaming mode, Horizon will start at the earliest known offer unless a cursor is set, in which case it will start from that cursor. Setting the cursor value to 'now' allows you to stream offers created since your request time.

### Request Parameters

The `getAccountOffers` method accepts the following request parameters:

- `accountId` (string, required): 
  The unique identifier (account ID) of the account for which you want to retrieve offers.

- `cursor` (string, optional): 
  A cursor value that determines the starting point for retrieving offers. Set it to 'now' to stream offers created since your request time.

- `order` (string, optional): 
  A designation of the order in which records should appear. Options include 'asc' (ascending) or 'desc' (descending). If this argument isn’t set, it defaults to 'asc'.

- `limit` (number, optional): 
  The maximum number of records returned. It defines the number of offers to fetch in a single request.

### Return Object

The `getAccountOffers` method returns a JSON object containing the list of offers associated with the specified account. Each offer represents an open order on the Stellar network, such as a trade offer to exchange one asset for another.

(Note: The exact fields in the return object might vary based on the Stellar blockchain's implementation and version.)
