# getEffects

### How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, Stellar, Network } from "@tatumio/tatum";

// Initialize the Tatum SDK for Stellar
const tatum = await TatumSDK.init<Stellar>({ network: Network.STELLAR });

// Define parameters (Replace placeholders with actual values and remove redundant)
const params = {
  cursor: "YOUR_CURSOR",
  order: "asc",
  limit: 10,
};

// List all effects
const effects = await tatum.rpc.getEffects(params);

// Always destroy the Tatum SDK instance when done to stop any background processes
await tatum.destroy();
```

### Overview

The `getEffects` method allows you to list all effects in the Stellar blockchain. Effects represent events or actions that have occurred on the network, such as payments, offers, and trustline changes.

### Example use cases:

1. **Effect Monitoring:**
   Developers and applications can use this method to monitor and retrieve information about all effects on the Stellar network.

2. **Streaming Effects:**
   Users can use streaming mode to listen for real-time updates to effects as they are added to the Stellar ledger.

### Request Parameters

The `getEffects` method accepts a `params` object with the following properties:

- `cursor` (string, optional):
  An optional cursor to start listing effects from a specific point.

- `order` (string, optional):
  An optional parameter to specify the order of listing (asc or desc). If not provided, it defaults to 'asc'.

- `limit` (number, optional):
  An optional parameter to specify the maximum number of effects to return. The limit can range from 1 to 200.

### Return Object

The `getEffects` method returns an array of effects from the Stellar blockchain. Each effect object contains information about the effect type, details, and related transaction.

(Note: The exact fields in the return object might vary based on the Stellar blockchain's implementation and version.)
