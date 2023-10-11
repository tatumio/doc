# decodescript

### How to use it

{% tabs %}
{% tab title="TypeScript/JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, ZCash, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<ZCash>({network: Network.ZCASH})

const result = await tatum.rpc.decodeScript("3044022070cc08500b2203b6ebe7c8285295bc1914a9d252504416e1cde4de4a7dc6c3c8022079af2be6db34efcf147e86a4cbf61cf9995106e5b5e95270d47c40b082052c8501")

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Overview

The `decodescript` RPC method decodes a serialized (hex-encoded) script and provides information about the script in a human-readable format. This method is useful for inspecting scripts for debugging purposes or for understanding their structure.

{% embed url="https://codepen.io/tatum-devrel/pen/QWJYPpL" %}

### Parameters

* `hex_string`: (string, required) The serialized script in hex format.

### Return Object

An object containing the decoded script information:

* `asm`: (string) The assembly representation of the script.
* `hex`: (string) The hex-encoded script.
* `type`: (string) The type of the script (e.g., 'pubkeyhash', 'multisig').
* `reqSigs`: (numeric, optional) The required number of signatures if the script is a multisig script.
* `addresses`: (array, optional) An array of addresses associated with the script if applicable.
* `p2sh`: (string, optional) The P2SH address for this script if applicable.

### JSON Examples

Request example:

{% code overflow="wrap" lineNumbers="true" %}
```json
{
  "jsonrpc": "2.0",
  "method": "decodescript",
  "params": ["3044022070cc08500b2203b6ebe7c8285295bc1914a9d252504416e1cde4de4a7dc6c3c8022079af2be6db34efcf147e86a4cbf61cf9995106e5b5e95270d47c40b082052c8501"],
  "id": 1
}
```
{% endcode %}

Response example:

{% code overflow="wrap" lineNumbers="true" %}
```json
{
    "result": {
        "asm": "44022070cc08500b2203b6ebe7c8285295bc1914a9d252504416e1cde4de4a7dc6c3c8022079af2be6db34efcf147e86 OP_MAX OP_UNKNOWN OP_UNKNOWN [error]",
        "desc": "raw(3044022070cc08500b2203b6ebe7c8285295bc1914a9d252504416e1cde4de4a7dc6c3c8022079af2be6db34efcf147e86a4cbf61cf9995106e5b5e95270d47c40b082052c8501)#3x5hf724",
        "type": "nonstandard"
    },
    "error": null,
    "id": 1
}
```
{% endcode %}

\
