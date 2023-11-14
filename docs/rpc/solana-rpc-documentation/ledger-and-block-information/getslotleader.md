# getSlotLeader

### How to Use It

{% code overflow="wrap" lineNumbers="true" %}
```javascript
// yarn add @tatumio/tatum

import { TatumSDK, Solana, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Solana>({ network: Network.SOLANA })

const res = await tatum.rpc.getSlotLeader()

await tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}

### Overview

The `getSlotLeader` method returns the identity of the node that is currently the leader of the slot. In the Solana network, a slot leader is responsible for producing blocks for the network during their assigned slot time. This method could be used to monitor the network's operation or for analysis of network activity.

{% embed url="https://codepen.io/tatum-devrel/pen/WNYmGze" %}

### Parameters

* `options` (object, optional): A configuration object containing:
  * `commitment`(string, optional): Specifies the level of commitment to apply when fetching data.
    * Values: `finalized` `confirmed` `processed`
  * `minContextSlot` (number, optional): The minimum slot that the request can be evaluated at.

### Return Object

The method returns a string that represents the Node identity Pubkey as a base-58 encoded string.

### JSON-RPC Request Example

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "getSlotLeader"
}
```

### JSON-RPC Response Example

```json
{
  "jsonrpc": "2.0",
  "result": "ENvAW7JScgYq6o4zKZwewtkzzJgDzuJAFxYasvmEQdpS",
  "id": 1
}
```
