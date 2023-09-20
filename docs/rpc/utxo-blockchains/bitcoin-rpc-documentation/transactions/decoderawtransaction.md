# decoderawtransaction

### How to use it

{% tabs %}
{% tab title="TypeScript/JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Bitcoin, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Bitcoin>({network: Network.BITCOIN})

const result = await tatum.rpc.decodeRawTransaction("02000000013412cdab3412cdab3412cdab3412cdab3412cdab3412cdab3412cdab3412cdab0000000000fdffffff0140420f00000000001976a91462e907b15cbf27d5425399ebf6f0fb50ebb88f1888ac00000000")

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Overview

The `decoderawtransaction` RPC method decodes a serialized (hex-encoded) raw transaction and displays its information in a human-readable format. This method is useful for inspecting raw transactions before broadcasting them to the Bitcoin network or for debugging purposes.

{% embed url="https://codepen.io/tatum-devrel/pen/xxQMegr" %}

### Parameters

* `hex_string`: (string, required) The serialized raw transaction in hex format.

### Return Object

An object containing the decoded raw transaction information:

* `txid`: (string) The transaction ID.
* `hash`: (string) The transaction hash.
* `version`: (numeric) The transaction version.
* `size`: (numeric) The transaction size in bytes.
* `vsize`: (numeric) The virtual transaction size in bytes.
* `weight`: (numeric) The transaction weight.
* `locktime`: (numeric) The lock time for the transaction.
* `vin`: (array) An array of objects, each representing an input of the transaction.
  * `txid`: (string) The transaction ID of the previous transaction output to spend.
  * `vout`: (numeric) The index of the output to spend from the previous transaction.
  * `scriptSig`: (object) The script used to redeem the previous transaction output.
    * `asm`: (string) The assembly representation of the script.
    * `hex`: (string) The hex-encoded script.
  * `sequence`: (numeric) The sequence number.
* `vout`: (array) An array of objects, each representing an output of the transaction.
  * `value`: (numeric) The amount sent to the output in BTC.
  * `n`: (numeric) The index of the output.
  * `scriptPubKey`: (object) The script used to lock the output.
    * `asm`: (string) The assembly representation of the script.
    * `hex`: (string) The hex-encoded script.
    * `reqSigs`: (numeric) The required number of signatures.
    * `type`: (string) The type of the script (e.g., 'pubkeyhash').
    * `addresses`: (array) An array of Bitcoin addresses associated with the output.

### JSON Examples

Request example:

{% code overflow="wrap" lineNumbers="true" %}
```json
{
  "jsonrpc": "2.0",
  "method": "decoderawtransaction",
  "params": ["02000000013412cdab3412cdab3412cdab3412cdab3412cdab3412cdab3412cdab3412cdab0000000000fdffffff0140420f00000000001976a91462e907b15cbf27d5425399ebf6f0fb50ebb88f1888ac00000000"],
  "id": 1
}
```
{% endcode %}

Response example:

{% code overflow="wrap" lineNumbers="true" %}
```json
{
    "result": {
        "txid": "9f5f5e6d36b6a284f52626be505175e43900009e7aa1b88fce74fcd30f0dc258",
        "hash": "9f5f5e6d36b6a284f52626be505175e43900009e7aa1b88fce74fcd30f0dc258",
        "version": 2,
        "size": 85,
        "vsize": 85,
        "weight": 340,
        "locktime": 0,
        "vin": [
            {
                "txid": "abcd1234abcd1234abcd1234abcd1234abcd1234abcd1234abcd1234abcd1234",
                "vout": 0,
                "scriptSig": {
                    "asm": "",
                    "hex": ""
                },
                "sequence": 4294967293
            }
        ],
        "vout": [
            {
                "value": 0.01,
                "n": 0,
                "scriptPubKey": {
                    "asm": "OP_DUP OP_HASH160 62e907b15cbf27d5425399ebf6f0fb50ebb88f18 OP_EQUALVERIFY OP_CHECKSIG",
                    "desc": "addr(1A1zP1eP5QGefi2DMPTfTL5SLmv7DivfNa)#632p52jr",
                    "hex": "76a91462e907b15cbf27d5425399ebf6f0fb50ebb88f1888ac",
                    "address": "1A1zP1eP5QGefi2DMPTfTL5SLmv7DivfNa",
                    "type": "pubkeyhash"
                }
            }
        ]
    },
    "error": null,
    "id": 1
}
```
{% endcode %}

\
