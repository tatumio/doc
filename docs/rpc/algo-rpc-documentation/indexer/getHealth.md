# getHealth

### How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, AlgorandIndexer, Network } from '@tatumio/tatum';

// Initialize the Tatum SDK for Algorand
const tatum = await TatumSDK.init<AlgorandIndexer>({ network: Network.ALGORAND_INDEXER });

// Check the health status of the Algorand node
const healthStatus = await tatum.rpc.health();

// Log the health status
console.log('Algorand Node Health Status:', healthStatus);

// Always destroy the Tatum SDK instance when done to stop any background processes
await tatum.destroy();
```

### Overview

The `getHealth` method allows you to check the health status of the Algorand node connected to the Tatum SDK. It provides information about the node's availability and operational status.

### Example Use Cases:

1. **Node Monitoring:** Developers and operators can use this method to monitor the health of the Algorand node connected to their application and ensure it is operational.

2. **Application Resilience:** It can be used to build resilience into your application by checking the health status of the node before making requests to it.

### Return Object

The method returns an object representing the health status of the Algorand Indexer node.

Please note that the structure of the returned object may change in different Algorand RPC versions.