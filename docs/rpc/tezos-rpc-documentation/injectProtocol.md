# injectProtocol

### How to use it

```typescript code example
// Import required libraries and modules from Tatum SDK
import { TatumSDK, Tezos, Network } from '@tatumio/tatum';

// Initialize the Tatum SDK for Tezos
const tatum = await TatumSDK.init<Tezos>({ network: Network.TEZOS });

// Define the protocol information as an object
const protocolInfo = {
    expected_env_version: 'YOUR_ENV_VERSION',  // Replace with the expected environment version
    components: [
        {
            name: 'COMPONENT_NAME',           // Replace with the component name
            interface: 'COMPONENT_INTERFACE', // Replace with the component interface
            implementation: 'COMPONENT_IMPL'  // Replace with the component implementation
        }
    ]
    async: false  // Optional: Set to 'true' for asynchronous injection
};

// Inject a protocol into the node
const protocolId = await tatum.rpc.injectProtocol(protocolInfo);

// Log the protocol ID
console.log('Protocol ID:', protocolId);

// Always destroy the Tatum SDK instance when done to stop any background processes
tatum.destroy();
```

### Overview

The `injectProtocol` method allows you to inject a protocol into the Tezos node. It returns the ID of the injected protocol. By default, the RPC waits for the protocol to be validated before returning. However, setting `async` to 'true' makes the function return immediately.

### Example Use Cases

1. **Protocol Upgrade:**
   Developers can use this method to inject protocol upgrades and improvements into the Tezos network.

2. **Network Maintenance:**
   Validators and administrators can inject protocol updates to perform network maintenance and ensure the stability and security of the blockchain.

### Request Parameters

The `injectProtocol` method accepts the following parameter:

- `expected_env_version` (string, required): 
  The expected environment version of the protocol.

- `components` (array of objects, required): 
  An array of components that make up the protocol. Each component should include:
  - `name` (string): The name of the component.
  - `interface` (string): The interface of the component.
  - `implementation` (string): The implementation of the component.

- `async` (boolean, optional): 
  Set to 'true' to receive an asynchronous response. Default is 'false'.

### Return Object

The `injectProtocol` method returns an object containing the ID of the injected protocol:

- `protocolId` (string): 
  A Tezos protocol ID in Base58Check-encoded format.

(Note: The exact fields in the return object might vary based on the Tezos blockchain's implementation and version.)