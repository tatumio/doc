# getHealth

### How to Use It

{% code overflow="wrap" lineNumbers="true" %}
```javascript
// yarn add @tatumio/tatum

import { TatumSDK, Solana, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Solana>({ network: Network.SOLANA })

const res = await tatum.rpc.getHealth()

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}

### Overview

The `getHealth` method is used to monitor the current health of the node. This method can be beneficial for maintenance and troubleshooting purposes. For instance, you may use this method to check the health status of your node periodically or to validate if a newly set up node is functioning correctly.

Please note that if one or more `--known-validator` arguments are provided to `solana-validator`, "ok" is returned when the node is within `HEALTH_CHECK_SLOT_DISTANCE` slots of the highest known validator; otherwise, an error is returned. If no known validators are provided, "ok" is always returned.

{% embed url="https://codepen.io/tatum-devrel/pen/QWJoKVb" %}

### Parameters

This method does not require any parameters.

### Return Object

If the node is healthy, it returns "ok". If the node is unhealthy, a JSON RPC error response is returned. The specifics of the error response are unstable and may change in the future.

### JSON-RPC Request Example

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "getHealth"
}
```

### JSON-RPC Response Examples

*   Healthy node response:

    ```json
    { "jsonrpc": "2.0", "result": "ok", "id": 1 }
    ```
*   Unhealthy node response (generic):

    ```json
    {
      "jsonrpc": "2.0",
      "error": {
        "code": -32005,
        "message": "Node is unhealthy",
        "data": {}
      },
      "id": 1
    }
    ```
*   Unhealthy node response (if additional information is available):

    ```json
    {
      "jsonrpc": "2.0",
      "error": {
        "code": -32005,
        "message": "Node is behind by 42 slots",
        "data": {
          "numSlotsBehind": 42
        }
      },
      "id": 1
    }
    ```
