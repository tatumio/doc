# getStakeMinimumDelegation

### How to Use It

{% code overflow="wrap" lineNumbers="true" %}
```javascript
// yarn add @tatumio/tatum

import { TatumSDK, Solana, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Solana>({ network: Network.SOLANA })

const res = await tatum.rpc.getStakeMinimumDelegation()

await tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}

### Overview

The `getStakeMinimumDelegation` method is an essential component of Solana's staking process. It returns the minimum delegation amount, expressed in lamports, that is required to stake on the Solana network. The staking process is an integral part of Solana's Proof of Stake consensus mechanism, where stakeholders are rewarded for their participation in securing the network.

This method is commonly used by wallets and staking services to inform their users about the minimum amount required for staking. By delegating a certain amount of Solana tokens, participants can earn staking rewards and contribute to the network's security. The minimum delegation amount is set by the network to prevent spam and maintain a high level of network performance.

{% embed url="https://codepen.io/tatum-devrel/pen/YzRgGyY?editors=1010" %}

### Parameters

This method takes the following parameters:

* A configuration object (optional): This object can contain the following fields:
  * `commitment` (string, optional): The level of commitment desired for the query.

### Return Object

The return object contains a `bool` value of the minimum delegation amount for staking, in lamports.

### JSON-RPC Request Example

```json
{
  "jsonrpc":"2.0", 
  "id":1,
  "method": "getStakeMinimumDelegation"
}
```

### JSON-RPC Response Example

```json
{
  "jsonrpc": "2.0",
  "result": {
    "context": {
      "slot": 501
    },
    "value": 1000000000
  },
  "id": 1
}
```
