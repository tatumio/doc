# getAccount

### How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, Stellar, Network } from '@tatumio/tatum';

// Initialize the Tatum SDK for Stellar
const tatum = await TatumSDK.init<Stellar>({ network: Network.STELLAR });

// Define the account ID (Replace placeholder with the actual account ID)
const accountId = 'YOUR_ACCOUNT_ID';

// Retrieve details of a specific account
const accountDetails = await tatum.rpc.getAccount(accountId);

// Log the account details
console.log('Account Details:', accountDetails);

// Always destroy the Tatum SDK instance when done to stop any background processes
await tatum.destroy();
```

### Overview

The `getAccount` method allows you to retrieve detailed information about a specific account. This includes information about balances and trustlines, including those that haven't been authorized yet.

## Example use cases:

1. **Account Information:**
   Developers and applications can use this method to access detailed information about a specific account, including its balances and trustlines.

2. **Trustline Analysis:**
   You can use the response to analyze the trustlines established by the account, including those that haven't been authorized yet.

### Request Parameters

The `getAccount` method requires the following parameter:

- `accountId` (string, required): 
  The unique identifier (account ID) of the account for which you want to retrieve details.

### Return Object

The `getAccount` method returns a JSON object containing details about the specified account, including balances, sponsorships, and other relevant information.

(Note: The exact fields in the return object might vary based on the Stellar blockchain's implementation and version.)