# getFeeStats

### How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, Stellar, Network } from '@tatumio/tatum';

// Initialize the Tatum SDK for Stellar
const tatum = await TatumSDK.init<Stellar>({ network: Network.STELLAR });

// Retrieve fee statistics
const feeStats = await tatum.rpc.getFeeStats();

// Log the fee statistics
console.log('Fee Statistics:', feeStats);

// Always destroy the Tatum SDK instance when done to stop any background processes
await tatum.destroy();
```

### Overview

The `getFeeStats` method allows you to retrieve information about per-operation fee statistics over the last 5 ledgers on the Stellar blockchain.

### Return Object

The `getFeeStats` method returns a JSON object containing fee statistics for various operations. The structure of the returned object is defined by the `FeeStats` schema.

(Note: The exact fields in the return object may vary based on the Stellar blockchain's implementation and version.)