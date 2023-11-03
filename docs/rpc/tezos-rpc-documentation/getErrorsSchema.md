# getErrorsSchema

### How to use it 

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, Tezos, Network } from '@tatumio/tatum';

// Initialize the Tatum SDK for Tezos
const tatum = await TatumSDK.init<Tezos>({ network: Network.TEZOS });

// Fetch a list of errors
const errors = await tatum.rpc.getErrorsSchema();

// Log the list of errors
console.log('Errors:', errors);

// Always destroy the Tatum SDK instance when done to stop any background processes
tatum.destroy();
```

### Overview

The `getErrorsSchema` method allows you to retrieve a list of errors with a status code of 200 from the Tezos network. These errors can provide insights into various aspects of the network, including smart contract execution, transaction failures, or other operational issues.

### Example use cases:

1. **Error Monitoring:**
   Developers and node operators can use this method to fetch error information to monitor the health and performance of the Tezos network. This information can help diagnose and address issues promptly.

2. **Troubleshooting:**
   When encountering issues with transactions or smart contract interactions, developers can use this method to obtain detailed error messages, aiding in troubleshooting and debugging.

3. **Network Analysis:**
   Blockchain analysts and researchers can analyze error data to gain insights into network activity, identify patterns, and assess the overall health of the Tezos blockchain.

### Request Parameters

The `getErrorsSchema` method does not require any specific parameters.

### Return Object

The endpoint returns an array of errors from the Tezos blockchain. Each error is an object containing details about the error.

(Note: The exact fields in the return object might vary based on the Tezos blockchain's implementation and version.)