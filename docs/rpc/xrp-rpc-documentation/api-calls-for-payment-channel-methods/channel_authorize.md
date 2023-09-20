# channel\_authorize

### How to use it

```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Xrp, Network, Secrets } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Xrp>({network: Network.XRP})

const res = await tatum.channelAuthorize(
  '1000000',
  '5DB01B7FFED6B67E6B0414DED11E051D2EE2B7619CE0EAA6286D67A3A4D5BDB3',
  { keyType: 'secp256k1', seed: 's████████████████████████████' }
)

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```

### Overview

The `channel_authorize` method creates a signature that can be used to redeem a specific amount of XRP from a payment channel. This method was added by the PayChan amendment and is available starting from the `rippled` 0.33.0 version.

This method can be used when an account wants to authorize a specific amount of XRP to be redeemed from a payment channel it has created. It generates a signature for a claim, which the receiving account can use to redeem a specific amount of XRP from the channel.

### Parameters

The `channel_authorize` method includes the following parameters:

* `amount`: Cumulative amount of XRP, in drops, to authorize. If the destination has already received a lesser amount of XRP from this channel, the signature created by this method can be redeemed for the difference.
* `channelId`: The unique ID of the payment channel to use.
* `options`: (Optional) An object that includes secrets for signing the claim:
  * `keyType`: (Optional) The signing algorithm of the cryptographic key pair provided. Valid types are `secp256k1` or `ed25519`. The default is `secp256k1`.
  * `seed`: (Optional) The secret seed to use to sign the claim. This must be the same key pair as the public key specified in the channel. Must be in the XRP Ledger's base58 format.

### Return Object

The `channel_authorize` method returns a result object that includes:

* `signature`: The signature for this claim, as a hexadecimal value. To process the claim, the destination account of the payment channel must send a PaymentChannelClaim transaction with this signature, the exact Channel ID, XRP amount, and public key of the channel.

### JSON-RPC Request Example

```json
{
    "method": "channel_authorize",
    "params": [
        {
            "channel_id": "5DB01B7FFED6B67E6B0414DED11E051D2EE2B7619CE0EAA6286D67A3A4D5BDB3",
            "seed": "s████████████████████████████",
            "key_type": "secp256k1",
            "amount": "1000000",
        }
    ]
}
```

### JSON-RPC Response Example

```json
{
    "id": "channel_authorize_example_id1",
    "status": "success",
    "result": {
        "signature": "304402204EF0AFB78AC23ED1C472E74F4299C0C21F1B21D07EFC0A3838A420F76D783A400220154FB11B6F54320666E4C36CA7F686C16A3A0456800

BBC43746F34AF50290064",
    }
}
```

> **Warning:** Do not send secret keys to untrusted servers or through unsecured network connections. (This includes the secret, seed, seed\_hex, or passphrase fields of this request.) You should only use this method on a secure, encrypted network connection to a server you run or fully trust with your funds. Otherwise, eavesdroppers could use your secret key to sign claims and take all the money from this payment channel and anything else using the same key pair. See Set Up Secure Signing for instructions.
