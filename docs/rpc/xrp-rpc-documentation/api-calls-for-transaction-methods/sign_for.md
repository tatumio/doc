# sign\_for

### How to use it

```javascript
// yarn add @tatumio/tatum

import { TatumSDK, Xrp, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Xrp>({network: Network.XRP})

const txJson = {
  TransactionType: "TrustSet",
  Account: "rEuLyBCvcw4CFmzv8RepSiAoNgF8tTGJQC",
  Flags: 262144,
  LimitAmount: {
      currency: "USD",
      issuer: "rHb9CJAWyB4rj91VRWn96DkukG4bwdtyTh",
      value: "100"
  },
  Sequence: 2,
  SigningPubKey: "",
  Fee: "30000"
};

const res = await tatum.rpc.signFor('rLFd1FzHMScFhLsXeaxStzv3UC97QHGAbM', txJson)

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```

### Overview

The `sign_for` command in XRP RPC allows one to provide a signature for a multi-signed transaction. This method is particularly useful when you want to ensure the transaction is only valid if it is signed by multiple parties, for example, in a shared wallet scenario or when a transaction must be approved by multiple individuals or entities.

This method is available only if the server admin has enabled public signing and requires the MultiSign amendment to be enabled. It was introduced in `rippled` version 0.31.0.

### Parameters

The `sign_for` method takes the following parameters:

* `account`: (string) - The address which is providing the signature.
* `tx_json`: (object) - The Transaction to sign. All fields of the transaction must be provided, including Fee and Sequence. The transaction must include the field SigningPubKey with an empty string as the value. The object may optionally contain a Signers array with previously-collected signatures.
* `options`: (object) - This includes `secret`, `seed`, `seed_hex`, `passphrase`, `key_type` as optional parameters which are used to sign the transaction.

### Return Object

The `sign_for` method returns a Promise that resolves to an object of type `XrpResult`. This object contains:

* `tx_blob`: A hexadecimal representation of the signed transaction, including the newly-added signature.
* `tx_json`: The transaction specification in JSON format, with the newly-added signature in the Signers array.

### JSON-RPC Request Example

```json
{
    "id": "sign_for_example",
    "command": "sign_for",
    "account": "rLFd1FzHMScFhLsXeaxStzv3UC97QHGAbM",
    "seed": "s████████████████████████████",
    "key_type": "ed25519",
    "tx_json": {
        "TransactionType": "TrustSet",
        "Account": "rEuLyBCvcw4CFmzv8RepSiAoNgF8tTGJQC",
        "Flags": 262144,
        "LimitAmount": {
            "currency": "USD",
            "issuer": "rHb9CJAWyB4rj91VRWn96DkukG4bwdtyTh",
            "value": "100"
        },
        "Sequence": 2,
        "SigningPubKey": "",
        "Fee": "30000"
    }
}
```

### JSON-RPC Response Example

```json
{
   "result" : {
      "status" : "success",
      "tx_blob" : "1200142200040000240000000263D5038D7EA4C680000000000000000000000000005553440000000000B5F762798A53D543A014CAF8B297CFF8F2F937E868400000000000753073008114A3780F5CB5A44D366520FC44055E8ED44D9A2270F3E010732102B3EC4E5DD96029A647CFA20DA07FE1F85296505552CCAC114087E66B46BD77DF744730450221009C195DBBF7967E223D8626CA19CF02073667F2B22E206727BFE848FF42BEAC8A022048C323B0BED19A988BDBEFA974B6DE8AA9DCAE250AA82BBD1221787032A864E58114204288D2E47F8EF6C99BCC457966320D12409711E1F1",
      "tx_json" : {
         "Account" : "rEuLyBCvcw4CFmzv8RepSiAoNgF8tTGJQC",
         "Fee" : "30000",
         "Flags" : 262144,
         "LimitAmount" : {
            "currency" : "USD",
            "issuer" : "rHb9CJAWyB4rj91VRWn96DkukG4bwdtyTh",
            "value" : "100"
         },
         "Sequence" : 2,
         "Signers" : [
            {
               "Signer" : {
                  "Account" : "rsA2LpzuawewSBQXkiju3YQTMzW13pAAdW",
                  "SigningPubKey" : "02B3EC4E5DD96029A647CFA20DA07FE1F85296505552CCAC114087E66B46BD77DF",
                  "TxnSignature" : "30450221009C195DBBF7967E223D8626CA19CF02073667F2B22E206727BFE848FF42BEAC8A022048C323B0BED19A988BDBEFA974B6DE8AA9DCAE250AA82BBD1221787032A864E5"
               }
            }
         ],
         "SigningPubKey" : "",
         "TransactionType" : "TrustSet",
         "hash" : "A94A6417D1A7AAB059822B894E13D322ED3712F7212CE9257801F96DE6C3F6AE"
      }
   }
}
```

###
