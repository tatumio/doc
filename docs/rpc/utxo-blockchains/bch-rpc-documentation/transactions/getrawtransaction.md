# getrawtransaction

### How to use it

{% tabs %}
{% tab title="TypeScript/JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, BitcoinCash, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<BitcoinCash>({network: Network.BITCOIN_CASH})

const result = await tatum.rpc.getRawTransaction("c7ad51e46a39d136adc2bb7536a236136cc206ab3c8dabcd4277d4cadcf674f2")

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Overview

The `getrawtransaction` RPC method retrieves a raw transaction from the blockchain or mempool. It returns the serialized (hex-encoded) transaction data. This method can be used to inspect a transaction's content before it's included in a block or to decode the transaction for further analysis.

{% embed url="https://codepen.io/tatum-devrel/pen/oNQmOYp" %}

### Parameters

* `txid`: (string, required) The transaction ID of the transaction to fetch.
* `verbose`: (bool, optional, default=false) If set to `true`, the method returns a JSON object containing information about the transaction.

### Return Object

If `verbose` is `false`, the method returns a hex-encoded string representing the serialized transaction data. If `verbose` is `true`, the method returns a JSON object with the following fields:

* `txid`: (string) The transaction ID.
* `hash`: (string) The transaction hash.
* `version`: (numeric) The transaction version.
* `size`: (numeric) The transaction size.
* `vsize`: (numeric) The virtual transaction size.
* `weight`: (numeric) The transaction's weight.
* `locktime`: (numeric) The transaction locktime.
* `vin`: (array) The transaction inputs. Each object within the array has the following properties:
  1. `txid`: A string representing the transaction ID of the output being spent. This refers to the transaction where the bitcoin spent in the current transaction was received.
  2. `vout`: An integer representing the index of the output in the transaction specified by `txid`. This is the position of the output in that transaction's `vout` array.
  3. `scriptSig`: An object containing two fields, `asm` and `hex`, which represent the unlocking script that satisfies the conditions of the spent output's locking script. `asm` contains the assembly representation of the script, while `hex` contains the hexadecimal representation.
  4. `sequence`: A number representing the sequence number of the input. It can be used to signal relative locktime constraints on the transaction.
* `vout`: (array) The transaction outputs. Each object within the array has the following properties:
  1. `value`: A decimal number representing the amount sent to the output's address.
  2. `n`: An integer representing the index of the output in the transaction's `vout` array.
  3. `scriptPubKey`: An object containing information about the locking script used to lock the output. The object has the following fields:
     * `asm`: The assembly representation of the locking script.
     * `hex`: The hexadecimal representation of the locking script.
     * `reqSigs`: The number of required signatures to unlock the output (relevant for multisig addresses).
     * `type`: The type of the locking script (e.g., 'pubkeyhash', 'scripthash', 'multisig', etc.).
     * `addresses`: An array of addresses associated with the output.
* `hex`: (string) The serialized transaction data in hex format.
* `blockhash`: (string, optional) The block hash containing the transaction.
* `confirmations`: (numeric, optional) The number of confirmations the transaction has.
* `time`: (numeric, optional) The transaction time in UNIX timestamp format.
* `blocktime`: (numeric, optional) The block time in UNIX timestamp format.

### JSON Examples

Request example:

{% code overflow="wrap" lineNumbers="true" %}
```json
{
  "jsonrpc": "2.0",
  "method": "getrawtransaction",
  "params": ["c7ad51e46a39d136adc2bb7536a236136cc206ab3c8dabcd4277d4cadcf674f2", true],
  "id": 1
}
```
{% endcode %}

Response example:

{% code overflow="wrap" lineNumbers="true" %}
```json
{
    "result": {
        "txid": "c7ad51e46a39d136adc2bb7536a236136cc206ab3c8dabcd4277d4cadcf674f2",
        "hash": "c00fc27056ad4305dc65a40a78381a6c923b4311a460ceccd81401016f5c8984",
        "version": 2,
        "size": 284,
        "vsize": 203,
        "weight": 809,
        "locktime": 0,
        "vin": [
            {
                "txid": "aaeb16390ca5209d8c72a0090a9ca87e6ff6491f239b3496cdb5c99977643583",
                "vout": 9,
                "scriptSig": {
                    "asm": "",
                    "hex": ""
                },
                "txinwitness": [
                    "3044022070cc08500b2203b6ebe7c8285295bc1914a9d252504416e1cde4de4a7dc6c3c8022079af2be6db34efcf147e86a4cbf61cf9995106e5b5e95270d47c40b082052c8501",
                    "03c9f7cff5a1d1a5fc107f37609c99d2e0fd699cacdef9696753b626b7508921c0"
                ],
                "sequence": 4294967294
            }
        ],
        "vout": [
            {
                "value": 0.00112825,
                "n": 0,
                "scriptPubKey": {
                    "asm": "0 29a7007eabae2ac56f221aad9c983b77a9f96c3b",
                    "desc": "addr(bc1q9xnsql4t4c4v2mezr2keexpmw75ljmpm0we75k)#3al0qk8v",
                    "hex": "001429a7007eabae2ac56f221aad9c983b77a9f96c3b",
                    "address": "bc1q9xnsql4t4c4v2mezr2keexpmw75ljmpm0we75k",
                    "type": "witness_v0_keyhash"
                }
            },
            {
                "value": 0.0027,
                "n": 1,
                "scriptPubKey": {
                    "asm": "0 24007ed98749dbb504fdea2bd07715c94d4c7751",
                    "desc": "addr(bc1qysq8akv8f8dm2p8aag4aqac4e9x5ca63yq4c88)#2wxgfkqe",
                    "hex": "001424007ed98749dbb504fdea2bd07715c94d4c7751",
                    "address": "bc1qysq8akv8f8dm2p8aag4aqac4e9x5ca63yq4c88",
                    "type": "witness_v0_keyhash"
                }
            },
            {
                "value": 0.00104468,
                "n": 2,
                "scriptPubKey": {
                    "asm": "0 c4c04e31613e2c3dfadaedde383bbfdd7a107d8a",
                    "desc": "addr(bc1qcnqyuvtp8ckrm7k6ah0rswalm4apqlv2ku24fa)#5rw0gs2m",
                    "hex": "0014c4c04e31613e2c3dfadaedde383bbfdd7a107d8a",
                    "address": "bc1qcnqyuvtp8ckrm7k6ah0rswalm4apqlv2ku24fa",
                    "type": "witness_v0_keyhash"
                }
            },
            {
                "value": 0.41658346,
                "n": 3,
                "scriptPubKey": {
                    "asm": "0 b33b0a68aba1d4697d8329f2b7939fb2a46b7332",
                    "desc": "addr(bc1qkvas569t582xjlvr98et0yulk2jxkuejx27yh4)#savgw9p6",
                    "hex": "0014b33b0a68aba1d4697d8329f2b7939fb2a46b7332",
                    "address": "bc1qkvas569t582xjlvr98et0yulk2jxkuejx27yh4",
                    "type": "witness_v0_keyhash"
                }
            }
        ],
        "hex": "020000000001018335647799c9b5cd96349b231f49f66f7ea89c0a09a0728c9d20a50c3916ebaa0900000000feffffff04b9b801000000000016001429a7007eabae2ac56f221aad9c983b77a9f96c3bb01e04000000000016001424007ed98749dbb504fdea2bd07715c94d4c77511498010000000000160014c4c04e31613e2c3dfadaedde383bbfdd7a107d8aeaa77b0200000000160014b33b0a68aba1d4697d8329f2b7939fb2a46b733202473044022070cc08500b2203b6ebe7c8285295bc1914a9d252504416e1cde4de4a7dc6c3c8022079af2be6db34efcf147e86a4cbf61cf9995106e5b5e95270d47c40b082052c85012103c9f7cff5a1d1a5fc107f37609c99d2e0fd699cacdef9696753b626b7508921c000000000",
        "blockhash": "00000000000000000004c6125026f00b76e7b762e645a0b0b7ecfa7a7dafdba2",
        "confirmations": 7,
        "time": 1682503076,
        "blocktime": 1682503076
    },
    "error": null,
    "id": 1
}
```
{% endcode %}

\
