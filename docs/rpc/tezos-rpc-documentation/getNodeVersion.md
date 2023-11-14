# version

### How to use it

```typescript
// Importing Tatum SDK for Tezos blockchain
import { TatumSDK, Network, Tezos } from '@tatumio/tatum';

// Initializing SDK for Tezos blockchain
const tatum = await TatumSDK.init<Tezos>({ network: Network.TEZOS });

// Fetching the version information
const versionInfo = await tatum.rpc.version();
console.log(versionInfo);

// Cleaning up resources used by Tatum SDK
await tatum.destroy();
```

### Overview

The `version` method is used to retrieve version information about the Tezos blockchain.

### Request Parameters

The `version` method doesn't require specific parameters in the request body.

### Return Object

The method returns an object with version information. Here are descriptions for the top-level objects within the returned object:

- `version` (object): An object with version details.
- `network_version` (object): An object with network version details.
- `commit_info` (object): An object with commit information.

(Note: The exact fields in the return object might vary based on the Tezos blockchain's implementation and version.)