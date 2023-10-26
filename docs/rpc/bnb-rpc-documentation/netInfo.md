# netInfo

### How to Use It

```typescript
// Importing Tatum SDK for Beacon Chain
import { TatumSDK, Network, Bnb } from '@tatumio/tatum';

// Initializing SDK for Beacon Chain network
const tatum = await TatumSDK.init<Bnb>({ network: Network.BEACON_CHAIN });

// Retrieve network information
const networkInfo = await tatum.rpc.netInfo();
console.log(networkInfo);

// Destroy Tatum SDK - needed for stopping background jobs
tatum.destroy();
```

### Overview

The `netInfo` method is used to retrieve network information from the Beacon Chain.

### Parameters

This method does not require any parameters.

### Return Object

The method returns a Promise that resolves to a JSON-RPC response containing the following fields:

- `listening` (boolean): Indicates whether the BNB Beacon Chain node is currently listening for incoming connections. If it is listening, the value will be `true`, otherwise, it will be `false`.

- `listeners` (array): An array of listener objects. Listener objects typically represent information about nodes or entities that are actively connected to the BNB Beacon Chain node, such as peers or clients.

- `n_peers` (number): Represents the number of peers that the BNB Beacon Chain node is currently connected to. It provides a count of how many other nodes or entities the node is actively communicating with.

- `peers` (array): An array of peer objects. Peer objects typically represent information about the peers or other nodes that the BNB Beacon Chain node is connected to. It may include details about these peers, such as their addresses, identities, or status.


(Note: The exact fields in the return object might vary based on the BNB Beacon Chain's implementation and version.)