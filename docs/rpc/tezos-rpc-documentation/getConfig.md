# config

### How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, Tezos, Network } from '@tatumio/tatum';

// Initialize the Tatum SDK for Tezos
const tatum = await TatumSDK.init<Tezos>({ network: Network.TEZOS });

// Fetch Tezos configuration information
const configInfo = await tatum.rpc.config();

// Log the Tezos configuration information
console.log(`Tezos Configuration:`, configInfo);

// Always destroy the Tatum SDK instance when done to stop any background processes
await tatum.destroy();
```

### Overview

The `config` method is used to retrieve configuration information about the Tezos blockchain.

### Request Parameters

The `config` method doesn't require specific parameters in the request body.

### Return Object

The method returns an object containing various configuration parameters and settings related to the Tezos blockchain. Here's a description of the top-level objects within the returned object:

- `data-dir` (string): The data directory path for the Tezos node.

- `rpc` (object): An object with RPC (Remote Procedure Call) related configuration details.

- `p2p` (object): An object with peer-to-peer (P2P) related configuration details.

- `shell` (object): An object with shell-related configuration details.

(Note: The exact fields in the return object might vary based on the Tezos blockchain's implementation and version.)