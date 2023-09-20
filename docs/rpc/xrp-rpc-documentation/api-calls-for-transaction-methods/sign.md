# sign

### How to use it

```javascript
// yarn add @tatumio/tatum

import { TatumSDK, Xrp, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Xrp>({network: Network.XRP})

const txJson = { /*...*/ }  // Your TxJson object here

const options = {
  secret: 's████████████████████████████', // Your secret key here
  // Additional options...
}

const res = await tatum.rpc.sign(txJson, options)

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```

### Overview

The `sign` method takes a transaction in JSON format and a seed value, and returns a signed binary representation of the transaction. This is particularly useful for performing transactions on the XRP Ledger. It is strongly recommended to perform local signing using a client library instead of using this command unless you run the `rippled` server yourself.

**Caution:** Do not send your secret to untrusted servers or through unsecured network connections.

### Parameters

The `sign` method accepts two parameters: `txJson` and `options`.

`txJson` (object): The transaction definition in JSON format. See [Ripple's official documentation](https://developers.ripple.com/transaction-formats.html) for a detailed structure of `TxJson`.

`options` (object): This optional parameter contains the following properties:

* `secret` (string): The secret seed of the account supplying the transaction, used to sign it. Cannot be used with `keyType`, `seed`, `seedHex`, or `passphrase`.
* `seed` (string): The secret seed of the account in the XRP Ledger's base58 format. Cannot be used with `secret`, `seedHex`, or `passphrase`.
* `seedHex` (string): The secret seed of the account in the hexadecimal format. Cannot be used with `secret`, `seed`, or `passphrase`.
* `passphrase` (string): The secret seed of the account as the string passphrase. Cannot be used with `secret`, `seed`, or `seedHex`.
* `keyType` (string): The signing algorithm of the cryptographic key pair provided (secp256k1 or ed25519). Cannot be used with `secret`.
* `offline` (boolean): If true, when constructing the transaction, do not try to automatically fill in or validate values.
* `buildPath` (boolean): If true, the server auto-fills the Paths field of a Payment transaction before signing.
* `feeMultMax` (number): The maximum value of fee multiplier.
* `feeDivMax` (number): The divisor value of fee.

### Return Object

Upon successful invocation, the `sign` method returns a Promise that resolves to `XrpResult` object which contains the following properties:

* `tx_blob` (string): Binary representation of the fully-qualified, signed transaction, as hexadecimal string.
* `tx_json` (object): JSON specification of the complete transaction as signed, including any fields that were automatically filled in.

### JSON-RPC Request Example

```json
{
    "method": "sign",
    "params": [
        {
            "offline": false,
            "secret": "s████████████████████████████",
            "tx_json": {
                "Account": "rf1BiGeXwwQoi8Z2ueFYTEXSwuJYfV2Jpn",
                "Amount": {
                    "currency": "USD",
                    "issuer": "rf1BiGeXwwQoi8Z2ueFYTEXSw

uJYfV2Jpn",
                    "value": "1"
                },
                "Destination": "ra5nK24KXen9AHvsdFTKHSANinZseWnPcX",
                "TransactionType": "Payment"
            },
            "fee_mult_max": 1000
        }
    ]
}
```

### JSON-RPC Response Example

```json
{
    "result": {
        "status": "success",
        "tx_blob": "1200002280000000240000016861D4838D7EA4C6800000000000000000000000000055534400000000004B4E9C06F24296074F7BC48F92A97916C6DC5EA9684000000000000002710732103AB40A0490F9B7ED8DF29D246BF2D6269820A0EE7742ACDD457BEA7C7D0931EDB7446304402200E5C2DD81FDF0BE9AB2A8D797885ED49E804DBF28E806604D878756410CA98B102203349581946B0DDA06B36B35DBC20EDA27552C1F167BCF5C6ECFF49C6A46F858081144B4E9C06F24296074F7BC48F92A97916C6DC5EA983143E9D4A2B8AA0780F682D136F7A56D6724EF53754",
        "tx_json": {
            "Account": "rf1BiGeXwwQoi8Z2ueFYTEXSwuJYfV2Jpn",
            "Amount": {
                "currency": "USD",
                "issuer": "rf1BiGeXwwQoi8Z2ueFYTEXSwuJYfV2Jpn",
                "value": "1"
            },
            "Destination": "ra5nK24KXen9AHvsdFTKHSANinZseWnPcX",
            "Fee": "10000",
            "Flags": 2147483648,
            "Sequence": 360,
            "SigningPubKey": "03AB40A0490F9B7ED8DF29D246BF2D6269820A0EE7742ACDD457BEA7C7D0931EDB",
            "TransactionType": "Payment",
            "TxnSignature": "304402200E5C2DD81FDF0BE9AB2A8D797885ED49E804DBF28E806604D878756410CA98B102203349581946B0DDA06B36B35DBC20EDA27552C1F167BCF5C6ECFF49C6A46F8580",
            "hash": "4D5D90890F8D49519E4151938601EF3D0B30B16CD6A519D9C99102C9FA77F7E0"
        }
    }
}
```
