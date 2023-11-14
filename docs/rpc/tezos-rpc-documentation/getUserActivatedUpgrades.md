# getUserActivatedUpgrades

### How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, Tezos, Network } from '@tatumio/tatum';

// Initialize the Tatum SDK for Tezos
const tatum = await TatumSDK.init<Tezos>({ network: Network.TEZOS });

// Fetch user-activated upgrades in the Tezos network configuration
const upgrades = await tatum.rpc.getUserActivatedUpgrades();

// Log the user-activated upgrades
console.log(`User-Activated Upgrades:`, upgrades);

// Always destroy the Tatum SDK instance when done to stop any background processes
await tatum.destroy();
```

### Overview

The `getUserActivatedUpgrades` method is used to retrieve information about user-activated upgrades in the Tezos network configuration. These upgrades represent changes to the Tezos protocol that have been activated by the network's users.

### Example Use Cases:

1. **Protocol Analysis:** Developers, analysts, and researchers can use this method to access information about user-activated upgrades in the Tezos network. This information can be valuable for understanding protocol changes and their implications.

2. **Node Configuration:** Node operators and service providers can ensure that their Tezos nodes are configured to support user-activated upgrades to stay compatible with the network.

### Request Parameters

The `getUserActivatedUpgrades` method doesn't require specific parameters in the request body.

### Return Object

The method returns an array of objects, each containing information about user-activated upgrades in the Tezos network configuration. Here's the updated structure of the return object with descriptions:

- `level` (integer, required): An integer representing the level at which the user-activated upgrade takes effect. The level can vary within the range from -2147483648 to 2147483647.

- `replacement_protocol` (string, required): A Tezos protocol ID (Base58Check-encoded) representing the protocol that serves as the replacement or modification in the user-activated upgrade.

(Note: The exact fields in the return object might vary based on the Tezos blockchain's implementation and version.)