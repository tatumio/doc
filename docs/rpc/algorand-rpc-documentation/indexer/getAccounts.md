# getAccounts

### How to use it

```typescript
// Import required libraries and modules
import { TatumSDK, Algorand, Network } from '@tatumio/tatum';

// Initialize the Tatum SDK
const tatum = await TatumSDK.init<Algorand>({ network: Network.ALGORAND_INDEXER });

// Define the input parameters
const address = { address: 'ALGORAND_ADDRESS' }; // Replace with the Algorand address you want to retrieve account information for.

// Retrieve account information using the Algorand Indexer
const accountInfo = await tatum.rpc.getAccounts(address);

// Log the account information
console.log('Algorand Account Information:', accountInfo);

// Always destroy the Tatum SDK instance when done to stop any background processes
tatum.destroy();
```

### Overview

The `getAccounts` method from the Algorand Indexer API allows you to retrieve detailed information about an Algorand account based on its address.

### Example Use Cases

1. **Account Balance**: Developers can use this method to check the balance of an Algorand account by providing its address.

2. **Account Details**: You can retrieve various details of an Algorand account, including its transactions, assets, and more, for further analysis.

### Request Parameters

The `getAccounts` method requires the following parameter:

- `address` (string, required): The Algorand address for which you want to retrieve account information.

### Return Object

The method returns an object representing the detailed information of the specified Algorand account, including various parameters. 

Please note that the structure of the returned object may change in different Algorand RPC versions.