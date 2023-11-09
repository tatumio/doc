# getGenesis

### How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, Algorand, Network } from '@tatumio/tatum';

// Initialize the Tatum SDK for Algorand
const tatum = await TatumSDK.init<Algorand>({ network: Network.ALGORAND });

// Retrieve the genesis information
const genesisInfo = await tatum.rpc.getGenesis();

// Log the genesis information
console.log('Algorand Genesis:', genesisInfo);

// Always destroy the Tatum SDK instance when done to stop any background processes
tatum.destroy();
```

### Overview

The `getGenesis` method allows you to retrieve the entire genesis file in JSON format.

### Example Use Cases

1. **Genesis Information**: Developers can use this method to retrieve the genesis information of the Algorand network, including details about the network configuration.

### Request Parameters

The `getGenesis` method does not require any parameters.

### Return Object

The method returns a string representing the entire genesis file in JSON format.

Please note that the structure of the returned object may change in different Algorand RPC versions.