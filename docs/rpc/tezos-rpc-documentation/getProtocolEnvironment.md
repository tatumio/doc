# getProtocolEnvironmentByHash

### How to Use

```typescript
// Importing Tatum SDK for Tezos blockchain
import { TatumSDK, Network, Tezos } from '@tatumio/tatum';

// Initializing SDK for Tezos blockchain
const tatum = await TatumSDK.init<Tezos>({ network: Network.TEZOS });

// Define parameters for the query
const params = { protocolHash: 'YOUR_PROTOCOL_HASH' };

// Fetching the protocol environment
const environmentVersion = await tatum.rpc.getProtocolEnvironmentByHash(params);
console.log(environmentVersion);

// Cleaning up resources used by Tatum SDK
tatum.destroy();
```

### Overview

The `getProtocolEnvironmentByHash` method retrieves information about the environment version of a specific Tezos protocol based on its protocol hash. You can use this method to obtain details about the environment version, which is represented as an integer.

### Request Parameters

- `Protocol_hash` (string, required): The protocol hash (Base58Check-encoded) for which you want to retrieve environment information.

### Return Object

The method returns an integer representing the environment version of the specified Tezos protocol based on its protocol hash.

(Note: The exact fields in the return object might vary based on the Tezos blockchain's implementation and version.)