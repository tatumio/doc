# getAccount

### How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, AlgorandIndexer, Network } from '@tatumio/tatum';

// Initialize the Tatum SDK for Algorand
const tatum = await TatumSDK.init<AlgorandIndexer>({ network: Network.ALGORAND_INDEXER });

// Define the input parameters as an object
const accountAddress = { address: 'ALGORAND_ACCOUNT_ADDRESS' }; // Replace with the Algorand account address you want to retrieve information for.

// Retrieve account information using the Algorand Indexer
const accountInfo = await tatum.rpc.getAccount(accountAddress);

// Log the account information
console.log('Algorand Account Information:', accountInfo);

// Always destroy the Tatum SDK instance when done to stop any background processes
tatum.destroy();
```

### Overview

The `getAccount` method allows you to retrieve detailed information about a specific Algorand account based on its account address.

### Example Use Cases

1. **Account Balance**: Developers can use this method to check the balance of a specific Algorand account by providing its address.

2. **Account Details**: Retrieve various details of an Algorand account, including its transactions, assets, and more, for further analysis.

### Request Parameters

The `getAccount` method requires the following parameter:

- `account-address` (string, required): The Algorand account address for which you want to retrieve account information.

### Return Object

The method returns an object representing the detailed information of the specified Algorand account, including various parameters. 

Please note that the structure of the returned object may change in different Algorand RPC versions.