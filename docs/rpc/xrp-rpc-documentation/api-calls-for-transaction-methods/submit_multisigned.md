# submit\_multisigned

### How to use it

```javascript
// yarn add @tatumio/tatum

import { TatumSDK, Xrp, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Xrp>({network: Network.XRP})

const txJson = { /* your transaction JSON here */ }
const options = { failHard: true } // optional

const res = await tatum.rpc.submitMultisigned(txJson, options)

await tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```

### Overview

The `submitMultisigned` method in the XRP RPC API allows you to apply a multi-signed transaction and send it to the network to be included in future ledgers. This method requires the MultiSign amendment to be enabled and was introduced in rippled 0.31.0.

This method is used when multiple parties are required to authorise a transaction, which can be a useful feature for securing high-value accounts, implementing distributed decision-making processes, or creating more complex authorisation structures for transactions.

{% embed url="https://codepen.io/tatum-devrel/pen/XWyQyao" %}

### Parameters

* `txJson` (TxJson): The transaction in JSON format with an array of Signers. To be successful, the weights of the signatures must be equal to or higher than the quorum of the SignerList.
* `options` (FailOption, optional): This parameter is optional. If `failHard` is true, and the transaction fails locally, it will not retry or relay the transaction to other servers. The default is false.

### Return Object

The `submit_multisigned` method returns an object that provides information about the result of the submitted multisigned transaction. The object contains the following fields:

* `engine_result`: A string that represents a code indicating the preliminary result of the transaction, for example, "tesSUCCESS".
* `engine_result_code`: An integer that represents a numeric code indicating the preliminary result of the transaction. This is directly correlated to the `engine_result`.
* `engine_result_message`: A string that represents a human-readable explanation of the preliminary transaction result.
* `tx_blob`: A string that represents the complete transaction in hexadecimal string format.
* `tx_json`: An object that represents the complete transaction in JSON format.

### JSON-RPC Request Example

```json
{
    "method": "submit_multisigned",
    "params": [
        {
            "tx_json": {
                "Account": "rEuLyBCvcw4CFmzv8RepSiAoNgF8tTGJQC",
                "Fee": "30000",
                /* ... rest of the transaction ... */
            },
            "fail_hard": true
        }
    ]
}
```

### JSON-RPC Response Example

```json
{
    "result": {
        "engine_result": "tesSUCCESS",
        "engine_result_code": 0,
        "engine_result_message": "The transaction was applied. Only final in a validated ledger.",
        "status": "success",
        "tx_blob": "120014220004000024000000046380000000000000000000000000000000000000005553440000000000B5F762798A53D543A014CAF8B297CFF8F2F937E868400000000000753073008114A3780F5CB5A44D366520FC44055E8ED44D9A2270F3E010732102B3EC4E5DD96029A647CFA20DA07FE1F85296505552CCAC114087E66B46BD77DF74473045022100CC9C56DF51251CB04BB047E5F3B5EF01A0F4A8A549D7A20A7402BF54BA744064022061EF8EF1BCCBF144F480B32508B1D10FD4271831D5303F920DE41C64671CB5B78114204288D2E47F8EF6C99BCC457966320D12409711E1E010732103398A4EDAE8EE009A5879113EAA5BA15C7BB0F612A87F4103E793AC919BD1E3C174473045022100FEE8D8FA2D06CE49E9124567DCA265A21A9F5465F4A9279F075E4CE27E4430DE022042D5305777DA1A7801446780308897699412E4EDF0E1AEFDF3C8A0532BDE4D0881143A4C02EA95AD6AC3BED92FA036E0BBFB712C030CE1F1",
        "tx_json": {
            "Account": "rEuLyBCvcw4CFmzv8RepSiAoNgF8tTGJQC",
            "Fee": "30000",
            "Flags": 262144,
            "LimitAmount": {
                "currency": "USD",
                "issuer": "rHb9CJAWyB4rj91VRWn96DkukG4bwdtyTh",
                "value": "0"
            },
            "Sequence": 4,
            "Signers": [
                {
                    "Signer": {
                        "Account": "rsA2LpzuawewSBQXkiju3YQTMzW13pAAdW",
                        "SigningPubKey": "02B3EC4E5DD96029A647CFA20DA07FE1F85296505552CCAC114087E66B46BD77DF",
                        "TxnSignature": "3045022100CC9C56DF51251CB04BB047E5F3B5EF01A0F4A8A549D7A20A7402BF54BA744064022061EF8EF1BCCBF144F480B32508B1D10FD4271831D5303F920DE41C64671CB5B7"
                    }
                },
                {
                    "Signer": {
                        "Account": "raKEEVSGnKSD9Zyvxu4z6Pqpm4ABH8FS6n",
                        "SigningPubKey": "03398A4EDAE8EE009A5879113EAA5BA15C7BB0F612A87F4103E793AC919BD1E3C1",
                        "TxnSignature": "3045022100FEE8D8FA2D06CE49E9124567DCA265A21A9F5465F4A9279F075E4CE27E4430DE022042D5305777DA1A7801446780308897699412E4EDF0E1AEFDF3C8A0532BDE4D08"
                    }
                }
            ],
            "SigningPubKey": "",
            "TransactionType": "TrustSet",
            "hash": "81A477E2A362D171BB16BE17B4120D9F809A327FA00242ABCA867283BEA2F4F8"
        }
    }
}
```
