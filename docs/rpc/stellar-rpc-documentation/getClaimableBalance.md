# getClaimableBalance

### How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, Stellar, Network } from '@tatumio/tatum';

// Initialize the Tatum SDK for Stellar
const tatum = await TatumSDK.init<Stellar>({ network: Network.STELLAR });

// Define the claimable balance ID (Replace 'YOUR_CLAIMABLE_BALANCE_ID' with the actual claimable balance ID)
const claimableBalanceId = 'YOUR_CLAIMABLE_BALANCE_ID';

// Retrieve information about a specific claimable balance
const claimableBalance = await tatum.rpc.getClaimableBalance(claimableBalanceId);

// Log the claimable balance details
console.log('Claimable Balance:', claimableBalance);

// Always destroy the Tatum SDK instance when done to stop any background processes
await tatum.destroy();
```

### Overview

The `getClaimableBalance` method allows you to retrieve information about a specific claimable balance on the Stellar blockchain. You need to provide the claimable balance ID to identify the balance you want to retrieve.

### Request Parameters

The `getClaimableBalance` method accepts the following request parameters:

- `claimableBalanceId` (string, required): 
  The unique identifier of the claimable balance you want to retrieve.

### Return Object

The `getClaimableBalance` method returns a JSON object containing the details of the requested claimable balance. The object includes various properties describing the characteristics of the claimable balance.

(Note: The exact fields in the return object might vary based on the Stellar blockchain's implementation and version.)