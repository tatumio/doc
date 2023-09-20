# submit

### How to use it

```javascript
// yarn add @tatumio/tatum
import { TatumSDK, Xrp, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Xrp>({network: Network.XRP})

const tx = {
  TransactionType: "Payment",
  Account: "rBPAQmwMrt7FDDPNyjwFgwSqbWZPf6GieV",
  Destination: "rPEPPER7kfTD9w2To4CQk6UCfuHM9c6GDY",
  Amount: "2000000",
  Flags: 2147483648
}

const res = await tatum.rpc.submit(tx, {
  secret: 's████████████████████████████'
})

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```

### Overview

The `submit` method is an RPC method in the XRP Ledger which is used to apply a transaction and send it to the network for confirmation and inclusion in future ledgers. It has two modes: Submit-only mode, where a signed and serialized transaction is submitted as-is, and Sign-and-submit mode, where a JSON-formatted transaction object is completed, signed, and then submitted. It is generally recommended to use the Submit-only mode for robustness.

Use cases for this method include submitting transactions to the XRP ledger, such as sending payments, managing trust lines, or deploying smart contracts.

{% embed url="https://codepen.io/tatum-devrel/pen/LYXvXLw" %}

### Parameters

The `submit` method takes the following parameters:

* `tx` (required): A string or JSON object representing the transaction to be submitted. This can be a hex representation of the signed transaction or a transaction definition in JSON format.
* `options` (optional): An object containing additional parameters. These can include:
  * `secret` (optional): The secret seed of the account.
  * `seed` (optional): The secret seed of the account in the XRP Ledger's base58 format.
  * `seedHex` (optional): The secret seed of the account in the hexadecimal format.
  * `passphrase` (optional): The secret seed of the account as the string passphrase.
  * `keyType` (optional): The signing algorithm of the cryptographic key pair provided (secp256k1 or ed25519).
  * `failHard` (optional): If true, and the transaction fails locally, do not retry or relay the transaction to other servers.
  * `offline` (optional): If true, when constructing the transaction, do not try to automatically fill in or validate values.
  * `buildPath` (optional): If true, the server auto-fills the Paths field of a Payment transaction before signing.
  * `feeMultMax` (optional): Sign-and-submit fails with the error rpcHIGH\_FEE if the auto-filled Fee value would be greater than the reference transaction cost × feeMultMax ÷ feeDivMax.
  * `feeDivMax` (optional): Sign-and-submit fails with the error rpcHIGH\_FEE if the auto-filled Fee value would be greater than the reference transaction cost × feeMultMax ÷ feeDivMax.

### Return Object

The `submit` method returns an object that provides information about the result of the submitted transaction. The object contains the following fields:

* `engine_result`: A string that represents a code indicating the preliminary result of the transaction, for example, "tesSUCCESS".
* `engine_result_code`: An integer that represents a numeric version of the result code. This is directly correlated to the `engine_result`.
* `engine_result_message`: A string that represents a human-readable explanation of the transaction's preliminary result.
* `tx_blob`: A string that represents the complete transaction in hexadecimal string format.
* `tx_json`: An object that represents the complete transaction in JSON format.
* `accepted`: A boolean value that indicates whether the transaction was accepted. This field is omitted in sign-and-submit mode.
* `account_sequence_available`: A number indicating the next Sequence Number available for the sending account after all pending and queued transactions. This field is omitted in sign-and-submit mode.
* `account_sequence_next`: A number indicating the next Sequence Number for the sending account after all transactions that have been provisionally applied, but not transactions in the queue. This field is omitted in sign-and-submit mode.
* `applied`: A boolean value indicating whether the transaction was applied to the open ledger. This field is omitted in sign-and-submit mode.
* `broadcast`: A boolean value indicating whether the transaction was broadcast to peer servers in the peer-to-peer XRP Ledger network. This field is omitted in sign-and-submit mode.
* `kept`: A boolean value indicating whether the transaction was kept to be retried later. This field is omitted in sign-and-submit mode.
* `queued`: A boolean value indicating whether the transaction was put in the Transaction Queue. This field is omitted in sign-and-submit mode.
* `open_ledger_cost`: A string indicating the current open ledger cost before processing this transaction. Transactions with a lower cost are likely to be queued. This field is omitted in sign-and-submit mode.
* `validated_ledger_index`: An integer indicating the ledger index of the newest validated ledger at the time of submission. This field is omitted in sign-and-submit mode.

### JSON-RPC Request Example - Submit Only

```json
{
    "method": "submit",
    "params": [
        {
            "tx_blob": "1200002280000000240000000361D4838D7EA4C6800000000000000000000000000055534400000000004B4E9C06F24296074F7BC48F92A97916C6DC5EA968400000000000000A732103AB40A0490F9B7ED8DF29D246BF2D6269820A0EE7742ACDD457BEA7C7D0931EDB74473045022100D184EB4AE5956FF600E7536EE459345C7BBCF097A84CC61A93B9AF7197EDB98702201CEA8009B7BEEBAA2AACC0359B41C427C1C5B550A4CA4B80CF2174AF2D6D5DCE81144B4E9C06F24296074F7BC48F92A97916C6DC5EA983143E9D4A2B8AA0780F682D136F7A56D6724EF53754"
        }
    ]
}
```

### JSON-RPC Request Example - Submit Only

```json
{
    "method": "submit",
    "params": [
        {
            "offline": false,
            "secret": "s████████████████████████████",
            "tx_json": {
                "Account": "rf1BiGeXwwQoi8Z2ueFYTEXSwuJYfV2Jpn",
                "Amount": {
                    "currency": "USD",
                    "issuer": "rf1BiGeXwwQoi8Z2ueFYTEXSwuJYfV2Jpn",
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
        "accepted" : true,
        "account_sequence_available" : 362,
        "account_sequence_next" : 362,
        "applied" : true,
        "broadcast" : true,
        "engine_result": "tesSUCCESS",
        "engine_result_code": 0,
        "engine_result_message": "The transaction was applied. Only final in a validated ledger.",
        "status": "success",
        "kept" : true,
        "open_ledger_cost": "10",
        "queued" : false,
        "tx_blob": "1200002280000000240000016961D4838D7EA4C6800000000000000000000000000055534400000000004B4E9C06F24296074F7BC48F92A97916C6DC5EA9684000000000002710732103AB40A0490F9B7ED8DF29D246BF2D6269820A0EE7742ACDD457BEA7C7D0931EDB74473045022100A7CCD11455E47547FF617D5BFC15D120D9053DFD0536B044F10CA3631CD609E502203B61DEE4AC027C5743A1B56AF568D1E2B8E79BB9E9E14744AC87F38375C3C2F181144B4E9C06F24296074F7BC48F92A97916C6DC5EA983143E9D4A2B8AA0780F682D136F7A56D6724EF53754",
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
            "Sequence": 361,
            "SigningPubKey": "03AB40A0490F9B7ED8DF29D246BF2D6269820A0EE7742ACDD457BEA7C7D0931EDB",
            "TransactionType": "Payment",
            "TxnSignature": "3045022100A7CCD11455E47547FF617D5BFC15D120D9053DFD0536B044F10CA3631CD609E502203B61DEE4AC027C5743A1B56AF568D1E2B8E79BB9E9E14744AC87F38375C3C2F1",
            "hash": "5B31A7518DC304D5327B4887CD1F7DC2C38D5F684170097020C7C9758B973847"
        }
    },
    "validated_ledger_index" : 21184416
}
```
