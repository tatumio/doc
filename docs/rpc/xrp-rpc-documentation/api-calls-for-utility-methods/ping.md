# ping

### How to use it

```javascript
// yarn add @tatumio/tatum

import { TatumSDK, Xrp, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Xrp>({network: Network.XRP})

const res = await tatum.rpc.ping()

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```

### Overview

The `ping` method is a simple RPC method provided by the Ripple (XRP) blockchain, used primarily to check the connection status and latency to the XRP blockchain node. It's a useful tool in debugging and network troubleshooting scenarios, as it provides an easy way to verify the connection and round-trip time between the client and the server.

{% embed url="https://codepen.io/tatum-devrel/pen/oNQOJdw" %}

### Parameters

The `ping` method accepts no parameters.

### Return Object

The `ping` method returns a simple object with the following field:

* `status`: The status of the request, typically "success". The presence of this field in the response indicates a successful round trip.

The client can measure the round-trip time from the request to the response as latency.

### JSON-RPC Request Example

```json
{
    "method": "ping",
    "params": [
        {}
    ]
}
```

### JSON-RPC Response Example

```json
{
    "result": {
        "status": "success"
    }
}
```

This response signifies a successful connection to the XRP node. The time it takes to receive this response can be used to measure network latency.
