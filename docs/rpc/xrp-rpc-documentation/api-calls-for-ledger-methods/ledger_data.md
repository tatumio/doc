# ledger\_data

### How to use it

```javascript
// yarn add @tatumio/tatum

import { TatumSDK, Xrp, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Xrp>({network: Network.XRP})

const res = await tatum.rpc.ledgerData({
  ledger_hash: "842B57C1CC0613299A686D3E9F310EC0422C84D3911E5056389AA7E5808A93C8",
  limit: 5,
  binary: true
})

await tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```

### Overview

The `ledger_data` method retrieves the contents of the specified ledger. You can iterate through several calls to retrieve the entire contents of a single ledger version.

{% embed url="https://codepen.io/tatum-devrel/pen/eYQoPWW" %}

### Parameters

The `ledger_data` method takes the following parameters:

* `ledger_hash` (Hash): A 20-byte hex string identifying the ledger version to use. (Optional)
* `ledger_index` (Ledger Index): The ledger index of the ledger to use, or a shortcut string to choose a ledger automatically. (Optional)
* `binary` (Boolean): If true, return ledger entries as hexadecimal strings instead of JSON. The default is false. (Optional)
* `limit` (Number): Limit the number of ledger entries to retrieve. The server may return fewer than this number of entries. Cannot be more than 2048 (when requesting binary) or 256 (when requesting JSON). The default is the maximum. (Optional)
* `marker` (Marker): Value from a previous paginated response. Resume retrieving data where that response left off. (Optional)
* `type` (String): Filter results to a specific type of ledger entry. Valid types include account, amendments, amm, check, deposit\_preauth, directory, escrow, fee, hashes, nft\_offer, offer, payment\_channel, signer\_list, state (trust line), and ticket. (Optional)

### Return Object

The `ledger_data` response provides information about the state tree of a specific ledger version. It follows the standard format and a successful result contains the following fields:

* `ledger_index`: An unsigned integer representing the ledger index of this ledger version.
* `ledger_hash`: A string representing the unique identifying hash of this ledger version.
* `state`: An array of JSON objects containing data from the ledger's state tree. The format of these objects will depend on whether binary was set to true in the request.
* `marker`: A server-defined value indicating the response is paginated. This can be passed to the next call to resume where this call left off.

If a type field is mentioned in the request, the state array will be empty if the first set of array objects does not match the type requested. In such cases, the marker from this response can be used to paginate and retrieve further data.

Each object in the `state` array may include the following fields:

* `data`: A string representing the hex representation of the requested data. This field is included only if "binary" was set to true in the request.
* `LedgerEntryType`: A string indicating what type of ledger object this object represents. This field is included only if "binary" was set to false in the request.
* Additional fields describing the object, depending on which ledger object type it is. These fields are included only if "binary" was set to false in the request.
* `index`: A string representing the unique identifier for this ledger entry, in hexadecimal format.

### JSON-RPC Request Example

Here's an example of the `ledger_data` method request:

```json
{
   "id": 2,
   "ledger_hash": "842B57C1CC0613299A686D3E9F310EC0422C84D3911E5056389AA7E5808A93C8",
   "command": "ledger_data",
   "limit": 5,
   "binary": true
}
```

### JSON-RPC Response Example

Here's an example of a successful response:

```json
{
    "result": {
        "ledger_hash": "842B57C1CC0613299A686D3E9F310EC0422C84D3911E5056389AA7E5808A93C8",
        "ledger_index": "6885842",
        "marker": "0002A590029B53BE7857EFF9985F770EC792CE483720EB5E963C4D6A607D43DF",
        "state": [
            {
                "data": "11006122000000002400000001250062FEA42D0000000055C204A65CF2542946289A3358C67D991B5E135FABFA89F271DBA7A150C08CA0466240000000354540208114C909F42250CFE8F12A7A1A0DFBD3CBD20F32CD79",
                "index": "00001A2969BE1FC85F1D7A55282FA2E6D95C71D2E4B9C0FDD3D9994F3C00FF8F"
            },
            {
                "data": "11006F22000000002400000003250035788533000000000000000034000000000000000055555B93628BF3EC318892BB7C7CDCB6732FF53D12B6EEC4FAF60DD1AEE1C6101F501071633D7DE1B6AEB32F87F1A73258B13FC8CC32942D53A66D4F038D7EA4C6800064D4838D7EA4C68000000000000000000000000000425443000000000035DD7DF146893456296BF4061FBE68735D28F3286540000000000F42408114A4B8F5F7B644AEDC3447F9459C132EEB016A133B",
                "index": "000037C6659BB98F8D09F2F4CFEB27DE8EFEAFE54DD9E1C13AECDF5794B0C0F5"
            },
            {
                "data": "11006F2200020000240000000A250067395C33000000000000000034000000000000000055A160BC41A45B6BB118DF23D77E4FF23C723431B917F50DCB41319ECC2821F34C5010DFA3B6DDAB58C7E8E5D944E736DA4B7046C30E4F460FD9DE4C1AA535D3D0C00064D554C88B43EFA00000000000000000000000000055534400000000000A20B3C85F482532A9578DBB3950B85CA06594D165400000B59B9F780081148366FB9ACD2A0FD822E31112D2EB6F98C317C2C1",
                "index": "0000A8791F78CC9B39200E12A9BDAACCF40A72A512FA815525CFC9BA772990F7"
            },
            {
                "data": "1100612200000000240000000125003E742F2D0000000055286498B513710CFEB2D723A554C7557983D1952DF4DEE342C40DCB43067C9A21624000000306DC42008114225BAB89C4A4B94624BB069D6DB3C819F934991C",
                "index": "0000B717320558E2DE1A3B9FDB24E9A695BF05D1A44E4A4683212BB1DD0FBA23"
            },
            {
                "data": "110072220002000025000B65783700000000000000003800000000000000005587591A63051645F37B85D1FBA55EE69B1C96BFF16904F5C99F03FB93D42D03756280000000000000000000000000000000000000004254430000000000000000000000000000000000000000000000000166800000000000000000000000000000000000000042544300000000000A20B3C85F482532A9578DBB3950B85CA06594D167D4C38D7EA4C680000000000000000000000000004254430000000000C795FDF8A637BCAAEDAD1C434033506236C82A2D",
                "index": "000103996A3BAD918657F86E12A67D693E8FC8A814DA4B958A244B5F14D93E58"
            }
        ],
        "status": "success"
    }
}
```
