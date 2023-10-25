# status

### How to use it

```typescript
// Importing Tatum SDK for Beacon Chain
import { TatumSDK, Network, Bnb } from '@tatumio/tatum';

// Initializing SDK for Beacon Chain network
const tatum = await TatumSDK.init<Bnb>({ network: Network.BNB });

// Fetching and logging the status of the Beacon Chain
const statusData = await tatum.rpc.status();
console.log(statusData);

// Cleaning up resources used by Tatum SDK
tatum.destroy();
```

### Overview

The `status` method is used to obtain information about the current status of the BNB Beacon Chain.

### Return Object

The `status` method provides an object that contains details about the current state of the chain. The returned structure might differ, but commonly includes these fields:

- `nodeInfo` (object): Details about the node, like its ID, listen address, and version.
- `syncInfo` (object): Information about the node's synchronization status, like the latest block hash, height, and timestamp.
- `validator_info` (object): Information about the node as a validator, such as its address and voting power.

(Note: The exact fields in the return object can differ based on the BNB Beacon Chain's implementation and version.)