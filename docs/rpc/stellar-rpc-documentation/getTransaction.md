# getTransaction

## How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, Stellar, Network } from '@tatumio/tatum';

// Initialize the Tatum SDK for Stellar
const tatum = await TatumSDK.init<Stellar>({ network: Network.STELLAR });

// Define parameters (Replace placeholders with actual values and remove redundant)
const transactionHash = 'YOUR_TRANSACTION_HASH';

// Retrieve a specific transaction by its hash
const transaction = await tatum.rpc.getTransaction(transactionHash);

// Always destroy the Tatum SDK instance when done to stop any background processes
await tatum.destroy();
```

## Overview

The `getTransaction` method allows you to retrieve information about a specific transaction on the Stellar blockchain. You can specify the transaction you want to retrieve by providing its unique transaction hash.

## Example use cases:

1. **Transaction Details:**
   Developers and applications can use this method to fetch detailed information about a specific transaction, including its source, destination, amount, and other transaction-specific data.

2. **Transaction Verification:**
   Users can use this method to verify and validate specific transactions on the Stellar network.

3. **Auditing and Reporting:**
   Platform administrators can access transaction data for auditing and reporting purposes.

## Request Parameters

The `getTransaction` method accepts a `transactionHash` parameter, which is a string representing the unique hash of the transaction you want to retrieve.

- `transactionHash` (string, required):
  The unique hash of the transaction you want to retrieve.

## Return Object

The `getTransaction` method returns detailed information about the specified transaction on the Stellar blockchain. The response includes data such as the transaction ID, source account, destination account, amount, fee, and other transaction-specific details.

(Note: The exact fields in the return object might vary based on the Stellar blockchain's implementation and version.)
