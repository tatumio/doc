# getNetworkDal

### How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, Tezos, Network } from '@tatumio/tatum';

// Initialize the Tatum SDK for Tezos
const tatum = await TatumSDK.init<Tezos>({ network: Network.TEZOS });

// Get the configuration for the DAL (Data Access Layer)
const dalConfig = await tatum.rpc.getNetworkDal();

// Log the DAL configuration
console.log(`DAL Configuration:`, dalConfig);

// Always destroy the Tatum SDK instance when done to stop any background processes
tatum.destroy();
```

### Overview

The `getNetworkDal` method allows you to retrieve the configuration for the Data Access Layer (DAL) on the Tezos blockchain network. The DAL configuration includes various parameters related to network settings.

### Example Use Cases:

1. **Network Configuration:** Developers and node operators can use this method to access and review the current network configuration, including parameters like redundancy factor, page size, slot size, and the number of shards.

2. **Testing Environments:** The `use_mock_srs_for_testing` parameter can be used in testing environments to simulate certain network settings.

### Return Object

The method returns an object that represents the configuration for the DAL:

- `activated` (boolean): Indicates whether the DAL is activated.

- `use_mock_srs_for_testing` (object or null): An optional object used for testing purposes. This object includes the following properties:
  - `redundancy_factor` (integer, 0-255): The redundancy factor for testing.
  - `page_size` (integer, 0-65535): The page size for testing.
  - `slot_size` (integer, -1073741824 to 1073741823): The slot size for testing.
  - `number_of_shards` (integer, 0-65535): The number of shards for testing.

- `bootstrap_peers` (array of strings): An array of bootstrap peers for the DAL.

Please note that the presence and structure of the `use_mock_srs_for_testing` object may vary based on the network's configuration.

You can use this information to understand and configure the DAL settings on the Tezos network.

(Note: The exact fields in the return object might vary based on the Tezos blockchain's implementation and version.)