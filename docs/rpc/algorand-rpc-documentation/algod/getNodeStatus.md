# getNodeStatus

### How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, Algorand, Network } from '@tatumio/tatum';

// Initialize the Tatum SDK for Algorand
const tatum = await TatumSDK.init<Algorand>({ network: Network.ALGORAND });

// Retrieve the current node status
const nodeStatus = await tatum.rpc.getNodeStatus();

// Log the node status
console.log('Algorand Node Status:', nodeStatus);

// Always destroy the Tatum SDK instance when done to stop any background processes
tatum.destroy();
```

### Overview

The `getNodeStatus` method allows you to retrieve the current status of an Algorand node.

### Example Use Cases

1. **Check Node Status**: Developers can use this method to check the status of an Algorand node and get information about the node's catchup progress, last round seen, consensus version details, and more.

### Request Parameters

The `getNodeStatus` method does not require any parameters.

### Return Object

The method returns an object representing the current status of the Algorand node. The object contains information about the node's catchup progress, last round seen, consensus version details, and more. 

Please note that the structure of the returned object may change in different Algorand RPC versions.
```
