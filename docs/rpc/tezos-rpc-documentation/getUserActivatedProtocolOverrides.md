# getUserActivatedProtocolOverrides

### How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, Tezos, Network } from '@tatumio/tatum';

// Initialize the Tatum SDK for Tezos
const tatum = await TatumSDK.init<Tezos>({ network: Network.TEZOS });

// Fetch user-activated protocol overrides in the Tezos network configuration
const overrides = await tatum.rpc.getUserActivatedProtocolOverrides();

// Log the user-activated protocol overrides
console.log(`User-Activated Protocol Overrides:`, overrides);

// Always destroy the Tatum SDK instance when done to stop any background processes
tatum.destroy();
```

### Overview

The `getUserActivatedProtocolOverrides` method is used to retrieve user-activated protocol overrides in the Tezos network configuration. These overrides may include specific settings or modifications to the protocol activated by the network's users.

### Example Use Cases:

1. **Protocol Customization:** Developers and node operators can use this method to check if there are any user-activated protocol overrides that affect the behavior of the Tezos network. This information can be crucial when customizing or interacting with the protocol.

2. **Protocol Compliance:** Users and service providers can ensure that their actions on the Tezos network comply with any user-activated protocol overrides that may be in effect.

### Request Parameters

The `getUserActivatedProtocolOverrides` method doesn't require specific parameters in the request body.

### Return Object

The method returns an object containing information about user-activated protocol overrides in the Tezos network configuration. 

These user-activated protocol overrides may include settings, parameters, or rules that deviate from the standard protocol behavior, allowing users to collectively influence the network's operation.

Here's the updated structure of the return object, with descriptions:

- `replaced_protocol` (string): A Tezos protocol ID (Base58Check-encoded) representing the protocol that has been replaced or modified by the user-activated override.

- `replacement_protocol` (string): A Tezos protocol ID (Base58Check-encoded) representing the protocol that serves as the replacement or modification in the user-activated override.

(Note: The exact fields in the return object might vary based on the Tezos blockchain's implementation and version.)