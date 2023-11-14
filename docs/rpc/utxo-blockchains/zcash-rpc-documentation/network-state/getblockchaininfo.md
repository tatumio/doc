# getblockchaininfo

### How to use it

{% tabs %}
{% tab title="TypeScript/JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, ZCash, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<ZCash>({network: Network.ZCASH})

const result = await tatum.rpc.getBlockChainInfo()

await tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Overview

`getblockchaininfo` is a method that provides general information about the current state of the blockchain. This method is useful for obtaining an overview of the blockchain, including the best block hash, chain height, difficulty, and network protocol version. It can be used for various purposes, such as monitoring the blockchain, tracking network upgrades, and assessing the current mining difficulty.

### Parameters

This method does not have any parameters.

### Return Object

The return object is a JSON object containing the following fields:

* `chain`: The current network name (e.g., "main", "test", or "regtest").
* `blocks`: The number of blocks in the local best block chain.
* `headers`: The number of headers the local node has validated.
* `bestblockhash`: The hash of the best (tip) block.
* `difficulty`: The current mining difficulty.
* `mediantime`: The median block time of the last 11 blocks in UNIX timestamp format.
* `verificationprogress`: The estimate of the verification progress of the local node as a percentage.
* `initialblockdownload`: A boolean indicating whether the node is in the initial block download mode.
* `chainwork`: The total work in the blockchain up to the best block.
* `size_on_disk`: The estimated size of the block and undo files on disk.
* `pruned`: A boolean indicating whether the block chain is pruned.
* `pruneheight`: The lowest-height complete block stored if the node is pruned (only present if `pruned` is true).
* `softforks`: An array of objects, each containing information about a softfork.
* `bip9_softforks`: An object containing the status of BIP9 softforks in the blockchain.
* `warnings`: Any network and blockchain warnings.

### JSON Examples

Request example:

{% code overflow="wrap" lineNumbers="true" %}
```json
{
  "id": 1,
  "jsonrpc": "2.0",
  "method": "getblockchaininfo"
}
```
{% endcode %}

Response example:

{% code overflow="wrap" lineNumbers="true" %}
```json
{
    "result": {
        "chain": "main",
        "blocks": 787066,
        "headers": 787066,
        "bestblockhash": "00000000000000000005233c5202951a85538b047e62f4c12c25d9ff65e62f07",
        "difficulty": 48712405953118.43,
        "time": 1682501447,
        "mediantime": 1682496904,
        "verificationprogress": 0.9999996042025764,
        "initialblockdownload": false,
        "chainwork": "000000000000000000000000000000000000000046b049efeeebefbd7f5e5cd6",
        "size_on_disk": 540374248868,
        "pruned": false,
        "warnings": ""
    },
    "error": null,
    "id": 1
}
```
{% endcode %}

\
