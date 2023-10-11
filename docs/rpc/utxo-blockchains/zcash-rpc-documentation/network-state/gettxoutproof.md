# gettxoutproof

### How to use it

{% tabs %}
{% tab title="TypeScript/JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, ZCash, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<ZCash>({network: Network.ZCASH})

const result = await tatum.rpc.getTxOutProof(["c7ad51e46a39d136adc2bb7536a236136cc206ab3c8dabcd4277d4cadcf674f2"], "00000000000000000004c6125026f00b76e7b762e645a0b0b7ecfa7a7dafdba2")

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Overview

The `gettxoutproof` RPC method returns a hex-encoded proof that the specified transaction(s) were included in a block. This method can be used to provide proof of inclusion for one or more transactions in the blockchain.

{% embed url="https://codepen.io/tatum-devrel/pen/BaGMEjv" %}
Try the function
{% endembed %}

### Parameters

* `txids` (array, required): An array of transaction IDs to create a proof for.
* `blockhash` (string, optional): The hash of the block that contains the transactions. If not provided, the method will search for the transactions in the most recent blocks.

**Example**

* `txids`: `["`c7ad51e46a39d136adc2bb7536a236136cc206ab3c8dabcd4277d4cadcf674f2`"]`
* `blockhash`: `"`00000000000000000004c6125026f00b76e7b762e645a0b0b7ecfa7a7dafdba2`"`

### Return Object

* `hex`: (string) The hex-encoded proof of the transaction(s) inclusion in the block.

### JSON Examples

Request example:

{% code overflow="wrap" lineNumbers="true" %}
```json
{
  "jsonrpc": "2.0",
  "method": "gettxoutproof",
  "params": [["c7ad51e46a39d136adc2bb7536a236136cc206ab3c8dabcd4277d4cadcf674f2"], "00000000000000000004c6125026f00b76e7b762e645a0b0b7ecfa7a7dafdba2"],
  "id": 1
}
```
{% endcode %}

Response example:

{% code overflow="wrap" lineNumbers="true" %}
```json
{
    "result": "00800020208d9c3576f57c3f0c35bd94440f37fe7971cf2b914001000000000000000000db47732e70243f1ae818f635ae4f5cacbacf1230f4dc226f0e62c0871d6e8692a4f5486439c705171a71df638e1100000e8c9aa54adefc4c7b9ccd760b4ee1369bdd5cc7cb8b3e426b4a3b490c2eee5473e8f8f4134d4035e4241a929b9cdac2c22b6d74e0cae88e9ad1f50eeba06ae52659f1c0be83c1705e6642336d47356c39632ca55d11c04f24d09132fd081f5144caf6c733deed2366cd75a4e5a355920cd31c889239e78e195fb15435451f82398b683b27258ff3523cf63a276f38ffe296dd541b99f80cc87ecb40f473e1af2656ac06a0d999105c71c293e571bb62bdd3f0509fe8d5be381d92a76d1659cafcfea20ac316c4cc72a4d81fd7e9d94227cf6457d5412e4ef0d0b32e195a092321e1ad6c16ff7c6a28b39104f3e38a21775f4ea730b25269de7a54eb4dee8752735fe3e7add927cb2f0813a5bddda182776a559d7ba91c3580fb55e49a0bef8186f274f6dccad47742cdab8d3cab06c26c1336a23675bbc2ad36d1396ae451adc759fa97499c565c252524eed6934be8f18f3784f1f7d74a1471c1778af5aa65b6e6ebb5c3625ce00ac09a644aaa8b0b86b679e65c9fa204582ac285368b97eaa7ef2c43019754f8a3e9442c9a6820a25b3d7037fe53ba9d89732f5835939225fa30b5d86694bb5fc5a384e799a22ae82017fb0cf95e70e7bb529725a81e0f96f704afaa5a00",
    "error": null,
    "id": 1
}
```
{% endcode %}

\
