# gettxout

### How to use it

{% tabs %}
{% tab title="TypeScript/JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Zcash, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Zcash>({network: Network.ZCASH})

const result = await tatum.rpc.getTxOut("c7ad51e46a39d136adc2bb7536a236136cc206ab3c8dabcd4277d4cadcf674f2", 1)

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Overview

The `gettxout` RPC method returns details about an unspent transaction output (UTXO). This method can be used to check if a specific transaction output is still unspent and obtain its details such as the value and scriptPubKey.

{% embed url="https://codepen.io/tatum-devrel/pen/gOQqyad" %}
Try this function
{% endembed %}

### Parameters

* `txid` (string, required): The transaction ID of the output.
* `n` (numeric, required): The index of the output within the transaction (vout).
* `include_mempool` (boolean, optional, default=true): Whether to include the mempool. Set to `false` to only check for outputs confirmed in the blockchain.

**Example**

* `txid`: `"a12345abcdef67890bcdef1234567890abcdef1234567890abcdef1234567890"`
* `n`: `1`
* `include_mempool`: `true`

### Return Object

The return object contains the following fields:

* `bestblock`: (string) The hash of the block at the tip of the blockchain.
* `confirmations`: (numeric) The number of confirmations for the transaction. -1 if the transaction is not yet confirmed and in the mempool.
* `value`: (numeric) The value of the output.
* `scriptPubKey`: (object) Information about the output's scriptPubKey.
  * `asm`: (string) The assembly representation of the script.
  * `hex`: (string) The hex representation of the script.
  * `type`: (string) The type of the script (e.g., `pubkeyhash`, `scripthash`).
  * `addresses`: (array) The Bitcoin addresses associated with this output.
* `coinbase`: (boolean) Whether the transaction is a coinbase transaction.
* `version`: (numeric) The transaction version.
* `height`: (numeric) The height of the block containing this output.

### JSON Examples

Request example:

{% code overflow="wrap" lineNumbers="true" %}
```json
{
  "jsonrpc": "2.0",
  "method": "gettxout",
  "params": ["c7ad51e46a39d136adc2bb7536a236136cc206ab3c8dabcd4277d4cadcf674f2", 1],
  "id": 1
}
```
{% endcode %}

Response example:

{% code overflow="wrap" lineNumbers="true" %}
```json
{
    "result": {
        "bestblock": "00000000000000000000bb252e11a381e2d9ee948dd8f2c9df9b7cb41adc40b2",
        "confirmations": 5,
        "value": 0.0027,
        "scriptPubKey": {
            "asm": "0 24007ed98749dbb504fdea2bd07715c94d4c7751",
            "desc": "addr(bc1qysq8akv8f8dm2p8aag4aqac4e9x5ca63yq4c88)#2wxgfkqe",
            "hex": "001424007ed98749dbb504fdea2bd07715c94d4c7751",
            "address": "bc1qysq8akv8f8dm2p8aag4aqac4e9x5ca63yq4c88",
            "type": "witness_v0_keyhash"
        },
        "coinbase": false
    },
    "error": null,
    "id": 1
}
```
{% endcode %}

\
